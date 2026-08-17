---
name: Route a chat completion through the Edgee AI Gateway
description: Pick a model from Edgee's live catalog and send an OpenAI-format chat completion through the gateway, with tagging, compression and cost attribution wired in.
api: openapi/edgee-openapi-original.json
base_url: https://edgee.io
operations:
  - listModels
  - createChatCompletion
generated: '2026-08-17'
method: generated
source: openapi/edgee-openapi-original.json + https://www.edgee.ai/docs/api-reference
---

# Route a chat completion through the Edgee AI Gateway

Edgee is a drop-in replacement for an LLM provider endpoint. You do not change your request shape —
you change the host and the model ID.

## Before you start

- Base URL is `https://edgee.io`. That is a different host and a different credential from the Edgee
  Console API at `https://api.edgee.app`. Do not mix the two keys.
- Authenticate with `Authorization: Bearer <api_key>`. HTTPS is required; plain HTTP fails.
- Model IDs on this endpoint use the `provider/model` form, e.g. `anthropic/claude-sonnet-4.5`.
  A bare model name is a `bad_model_id` 400.

## Step 1 — resolve a model with `listModels`

`GET /v1/models` returns the catalog as `{"object":"list","data":[{id, object, owned_by, created}]}`.
Read the `id` field and use it verbatim as `model`. Never hard-code a model string you have not seen
in this response — the catalog moves (230 models on 2026-08-17, and the changelog adds providers
regularly).

The optional `provider` query parameter is declared in the spec but the spec itself marks it
"currently not implemented". Filter client-side on `owned_by` instead.

## Step 2 — send the request with `createChatCompletion`

`POST /v1/chat/completions` with the OpenAI Chat Completions body: `model`, `messages[]`, and
optionally `tools[]`, `tool_choice`, `stream`.

Attach Edgee's own headers on the same request:

- `X-Edgee-Tags` — comma-separated tags. This is the only way to get per-project, per-repo or
  per-environment cost attribution; the same tags drive tag-spend alerts and the Console API log
  export filter. Set them on every call, not just some.
- `X-Edgee-Compression-Model` — the compression bundle to apply. Tune it for the agentic style of
  the caller.
- `X-Edgee-Debug` — set only while diagnosing. It enlarges the response.

## Step 3 — read what actually happened

The `ChatCompletionResponse` carries more than the completion:

- `usage` → `prompt_tokens_details` / `completion_tokens_details` for the real token accounting.
- `compression` → how many tokens Edgee removed before the provider saw the request.
- `edgee_tools_executed` → tools the gateway itself ran.

Two response headers tell you whether you got what you asked for:

- `X-Edgee-Provider` — which upstream provider actually served the request.
- `X-Edgee-Fallback-Used` — whether the gateway rerouted away from your requested model.

If `X-Edgee-Fallback-Used` is set, the completion came from a different model than the one you named.
Log it. Do not treat the response as evidence that your requested model was reachable.

## Streaming

Set `"stream": true` and read `text/event-stream`. Chunks arrive as `ChatCompletionChunk` with
`choices[].delta`.

## Retry rules — read this before writing a retry loop

**Edgee publishes no idempotency contract.** There is no `Idempotency-Key` header anywhere in the
docs or the spec. A retried `createChatCompletion` is a second inference and a second charge. Retry
only on `429` and `5xx`, with exponential backoff, and never retry a request you cannot afford twice.

Error handling, by `error.code`:

| Code | Status | Do this |
|---|---|---|
| `bad_model_id`, `model_not_found`, `provider_not_supported` | 400 | Re-resolve from `listModels`; do not retry the same string |
| `unauthorized` | 401 | Fix the key or the header; do not retry |
| `forbidden` | 403 | The key is inactive/expired, or the model is blocked for this key |
| `usage_limit_exceeded` | 429 | Back off; the budget or credit balance is exhausted, not the rate |
| `internal_error`, `provider_error` | 500/502 | Back off and retry |

The full envelope and code registry are in `errors/edgee-error-codes.yml`.
