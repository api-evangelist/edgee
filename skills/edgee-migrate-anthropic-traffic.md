---
name: Move existing Anthropic Messages traffic onto Edgee
description: Repoint an application already written against the Anthropic Messages API at the Edgee gateway without changing the request shape, and understand exactly what does and does not carry over.
api: openapi/edgee-openapi-original.json
base_url: https://edgee.io
operations:
  - listModels
  - createMessage
  - countTokensMessages
generated: '2026-08-17'
method: generated
source: openapi/edgee-openapi-original.json + https://www.edgee.ai/docs/api-reference
---

# Move existing Anthropic Messages traffic onto Edgee

Edgee implements the Anthropic Messages shape natively, so an application already using the
Anthropic SDK moves by changing the base URL and the key — not the code that builds requests.

## Step 1 — repoint the client

- Base URL: `https://edgee.io`
- Auth: either `Authorization: Bearer <api_key>` **or** the Anthropic-style `x-api-key` header. Both
  are declared securitySchemes on this API, so the Anthropic SDK's default header works unchanged.
- A third header, `x-edgee-api-key`, exists for Claude CLI passthrough: when set, the gateway uses
  that key instead of the `Authorization` header. Use it only for that case.

## Step 2 — know the model-ID rule, it is different here

On `createMessage` (`POST /v1/messages`) the model ID is **bare**, Anthropic-style:
`claude-sonnet-4.5`. On the OpenAI-format endpoints the same model is `anthropic/claude-sonnet-4.5`.
Mixing the two forms is the most likely first failure and produces `bad_model_id` (400).

Resolve real IDs with `listModels` (`GET /v1/models`) rather than hard-coding.

## Step 3 — check streaming before you ship

`createMessage` supports `stream: true` over `text/event-stream`, **but only when the selected model
is served by the Anthropic provider**. Any other provider returns 400 with
`error.code` = `streaming_not_supported`. If your app streams and you plan to reroute across
providers, use `createChatCompletion` (`POST /v1/chat/completions`) instead, which streams for all
providers.

Note also that `createMessage` documents only 400 / 401 / 403 responses in the spec — it does not
declare the 429 and 500 that `createChatCompletion` and `createResponse` do. Handle them anyway.

## Step 4 — count tokens the Anthropic way

`countTokensMessages` (`POST /v1/messages/count_tokens`) is the Anthropic-format token estimator and
mirrors Anthropic's own count-tokens call. Use it, not `countTokens`, for this migration path.

## Step 5 — add what you did not have before

Repointing gets you three things the direct Anthropic API does not give you. Wire them on day one or
you will not be able to reconstruct them later:

- `X-Edgee-Tags` on every request — the only source of per-project cost attribution.
- `x-edgee-session-id` — groups all messages from a single CLI session. This is the identifier the
  four Edgee MCP session tools (`setSessionName`, `setSessionGitRepo`, `addSessionPullRequest`,
  `addSessionCommit`) operate on.
- `X-Edgee-Provider` and `X-Edgee-Fallback-Used` on the response — read them, because with fallback
  and reroute enabled the model that answered may not be the model you asked for.

## What does not carry over

- No idempotency. Anthropic has none here either, but Edgee adds retry/fallback/reroute on the
  server side, which means a single client call can become multiple provider calls. Do not layer an
  aggressive client retry on top.
- Response usage is `AnthropicUsage` on this endpoint, not the OpenAI `Usage` object — different
  field names. If you have a cost-accounting layer, it needs a branch per format.
