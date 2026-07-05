# API Contract — spec card

The operations an API, service, module, or event surface exposes, and for each the request and response shapes, the errors, and the auth that callers build against and the producer must honor. Document the real interface where one exists, and mark proposed operations as proposed.

**Template:** [../templates/api-contract.md](../templates/api-contract.md) · **Saves as:** `api-contract.md`

## Ground in

Any existing contract or interface definition — what the interface is for and the consumer needs it must serve. Settle the scope — which operations, which surface — and whether it's documenting an existing interface or specifying a new one.

## Analysis method

Map the real shape of the interface from the code, and what consumers depend on:

- **Read the shapes** — for each operation, its inputs, outputs, types, error paths, and auth — from routes, handlers, serializers, and type definitions.
- **Separate exposed from proposed** — hold what the code actually exposes apart from what's only proposed.
- **Note the consumers** — who depends on the interface and on what; it sets what a change can and can't break.

On a large or sprawling surface, dispatch parallel search agents to map the operations, then verify the load-bearing shapes against the source yourself.

## Drafting notes

Fill the overview and consumers, the shared conventions, each operation with its request, response, errors, and auth, and the data types they reference. Specify types concretely. Validate by verifying each operation and type against the source — fields, types, status codes, and error paths match the real implementation. For a new interface, confirm internal consistency: every referenced type defined, every operation whole. The honest account names any operation whose error paths or types couldn't be fully pinned down.

## Facilitation angles

- Whether the shapes fit what consumers actually need.
- Which changes would break existing consumers, and whether that's intended.
- Where the contract should guarantee behavior — idempotency, ordering, side effects — that the draft left implicit.

## Standards

- **Complete** — every operation states its request, response, errors, and auth; no operation is half-specified.
- **Precise** — types and shapes are concrete (named types, fields, required versus optional), not "an object with the data."
- **Anchored to consumers** — it captures what callers depend on, so a change can be judged against what it would break.
- **Accurate or consistent** — for an existing interface, every shape matches the code; for a new one, every referenced type is defined and every operation is whole.
- **Evolution-aware** — the versioning approach and what counts as a breaking change are stated.

## Verify focus

Where the operations, shapes, and claims don't hold against the code.
