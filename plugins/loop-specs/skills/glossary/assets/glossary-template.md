# Glossary Template

The artifact glossary writes: the domain terms a project uses and their precise definitions.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{domain_or_repo}}
last_updated: {{YYYY-MM-DD}}
---

# {{domain_or_repo}} — Glossary

## Scope

{{The domain this vocabulary covers, in a line.}}

## Terms

{{Each term with a precise definition — and, where confusion is likely, its aliases and what it's distinct from. Group by area when the set is large.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Contested terms

{{Terms the code or team uses inconsistently, with the canonical meaning chosen and the conflicting usages noted.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the domain or repo, and `last_updated` to today's date on every write.
- Define every term so it's distinguished from its neighbors — a definition that just restates the term adds nothing.
- Name aliases and easily-confused terms where confusion is likely; for a term used inconsistently, rule on one canonical meaning.
- Keep every term grounded in real usage; leave out invented terms and nouns that carry no domain meaning.
- Group terms by area when the set is large enough to need it.
- Write plainly, for a reader who isn't looking at the code. Domain language is the subject here; define it, don't assume it.
