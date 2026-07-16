# Exercise 1 - Validate a minimal entity

## Goal

Validate a small Cohort entity and distinguish its schema from its data.

## Instructions

1. Open [Biovalidator](http://localhost:3020). Paste this into its schema input.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "name": { "type": "string" }
  },
  "required": ["name"],
  "additionalProperties": false
}
```

2. Paste this into its data input and validate it.

```json
{
  "name": "Rare disease cohort"
}
```

3. Paste this into its data input and validate it again.
```json
{
  "name": true
}
```

## Questions

1. Which part says that `name` **must** be present?
2. Why is one value valid but not the other?

> **In the real repository:** this is a simplified version of `schemas/entities/cohort/schema.json`.

<details>
<summary>Solution</summary>

1. `"required": ["name"]` is the part that makes ``name`` required.
2. The second is not valid because ``name`` is of ``"type": "string"``, and the second value was a boolean (``true``)

</details>
