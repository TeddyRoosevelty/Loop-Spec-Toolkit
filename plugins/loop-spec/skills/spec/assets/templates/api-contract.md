# API Contract Template

The artifact api-contract writes: a precise contract for an interface — the operations, their request and response shapes, errors, and auth — that consumers build against and the producer must honor.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{interface_name}}
last_updated: {{YYYY-MM-DD}}
---

# {{interface_name}} — Interface Contract

## Overview

{{What the interface is and what it's for, and who consumes it — the callers that depend on it.}}

## Conventions

{{The rules shared across all operations: the authentication scheme, request and response formats, the common error model, and how the contract is versioned and evolved.}}

## Operations

{{Each operation the interface exposes — an endpoint, method, or event. For each: its name and how it's invoked, its purpose, the request (parameters and body, with types and which are required), the success response (shape and status), the errors it returns (conditions and codes), and any auth or permissions specific to it.}}

## Data types

{{The shared object shapes the operations reference — each with its fields, their types, and which are required.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Invariants & guarantees

{{Behavior callers can rely on across operations — idempotency, ordering, consistency, side effects, retry semantics.}}

## Rate limits & quotas

{{The limits callers must respect, and what happens when they're exceeded.}}

## Examples

{{Sample request and response pairs for operations where they clarify a tricky shape.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the interface name, and `last_updated` to today's date on every write.
- Match depth to the interface. A small interface gets a short contract — a section may be a single line. Drop a conditional section with nothing real to say; never leave an empty header or pad one with placeholder prose.
- Specify types concretely — named shapes, fields, required versus optional — not vague descriptions an implementer would have to guess at.
- Document the real interface where one exists; mark proposed operations as proposed, kept distinct from what's live.
- Adapt the operation shape to the interface kind — HTTP endpoints, RPC methods, library functions, or event payloads — while keeping the request, response, errors, and auth for each.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
