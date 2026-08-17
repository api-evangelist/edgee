---
name: Estimate and compress a payload before you spend on it
description: Use Edgee's token counting and standalone compression endpoints to measure and shrink a request before any LLM provider is called or billed.
api: openapi/edgee-openapi-original.json
base_url: https://edgee.io
operations:
  - countTokens
  - compress
  - createChatCompletion
generated: '2026-08-17'
method: generated
source: openapi/edgee-openapi-original.json + https://www.edgee.ai/docs/api-reference/compress
---

# Estimate and compress a payload before you spend on it

Edgee separates measurement, compression and inference into three endpoints, so you can do the first
two without paying a provider for either.

## Step 1 — measure with `countTokens`

`POST /v1/count_tokens` estimates the token count for a set of messages **without making an LLM
call**. Use it to decide whether a payload fits a context window, and to establish a baseline before
compression.

For Anthropic-format payloads use `countTokensMessages` (`POST /v1/messages/count_tokens`) instead —
same purpose, Anthropic request shape.

An invalid tokenizer selection returns a 400 with `error.code` = `invalid_tokenizer`.

## Step 2 — compress with `compress`

`POST /v1/compress` compresses a request payload and returns it, **without calling any provider**.
The request body is polymorphic: it accepts a `ChatCompletionRequest`, a `CreateMessageRequest` or a
`ResponsesRequest`. The response mirrors the input shape and adds `metadata`.

This is the endpoint to use when you want compression as a step you control rather than as something
the gateway does invisibly in the request path. Compression is defined by Edgee as surgical removal
of redundancy, not summarization, in two layers:

- **input** — system prompts, tool results, codebase context, conversation history, MCP tool
  definitions (about 99% of token volume)
- **output** — filler, repetitive scaffolding, preambles, markdown overhead (about 1% of volume, 10%
  of cost)

## Step 3 — verify the saving, then send

Re-run `countTokens` on the compressed payload and compare. Only then send the compressed body to
`createChatCompletion`.

If you instead let the gateway compress in-line, read `compression` on the `ChatCompletionResponse`
to see what it removed. Either way, measure — do not assume a percentage.

## Notes and limits

- `compress` and `countTokens` are cheap relative to inference, but they are still authenticated
  calls against `https://edgee.io` with your gateway API key.
- Both return the standard Edgee error envelope: `{"error":{"message","type","code","param"}}`.
  `compress` documents 400 / 401 / 403 only.
- `X-Edgee-Compression-Model` selects the compression bundle on the inference endpoints; use it to
  match the compressor to the agentic style of the caller.
- There is no idempotency key on any of these operations. They are safe to repeat in the sense that
  nothing is persisted, but each call is a billed request.
