# Data Model — spec card

The entities a system holds, their fields and types, the relationships between them, and the rules that govern the data. Describe the real schema where one exists, and mark proposed entities as proposed.

**Template:** [../templates/data-model.md](../templates/data-model.md) · **Saves as:** `data-model.md`

## Ground in

Any existing data model doc. Settle the scope — the whole system, one domain, or a feature — and what data is in play.

## Analysis method

Read the real data shape from the code: the entities, their fields and types, keys, relationships, and the constraints — from models, schema, and migrations. Hold what the schema actually defines apart from what's only proposed. On a large schema, dispatch parallel search agents to map the entities and relationships, then verify against the source yourself.

## Drafting notes

Fill the overview, the entities with their fields and keys, the relationships with cardinality, and the constraints and invariants. Use an ERD where it shows the structure better than prose. Validate by verifying entities, fields, types, and relationships against the source — nothing invented or missed. For a new model, confirm it's internally consistent: every relationship references a defined entity, and every entity has a key.

## Facilitation angles

- Whether the entities are split where they should be, or a concept is wrongly split or merged.
- Whether the relationships and cardinality match how the data is really used.
- Which invariants must always hold, and whether the model enforces them.

## Standards

- **Accurate to the schema** — entities, fields, types, and relationships match what's actually defined, verified rather than assumed.
- **Complete** — each entity has a key and typed fields; no entity is a bag of untyped attributes.
- **Relationships explicit** — cardinality and the linking keys are stated, not implied.
- **Constraints captured** — uniqueness, validation, referential integrity, and invariants that must always hold are named.
- **At the right altitude** — a logical model of entities and relationships, not migration SQL or ORM boilerplate.

## Verify focus

Where the entities, relationships, and constraints don't hold against the schema.
