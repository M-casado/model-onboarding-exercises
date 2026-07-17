# Exercise 2 - Break and repair data

## Goal

See the difference between valid JSON and JSON that satisfies a schema.

## Instructions

1. Open [Biovalidator](http://localhost:3020). Paste this schema into its schema input.

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

2. Paste each document below into the data input and validate it.

```json
{}
```

```json
{
  "name": 12
}
```

```json
{
  "name": "Rare disease cohort",
  "@id": "ega:EGAH00001000001"
}
```

3. After each failed validation, you can repair or reset the data by pasting this valid document.

```json
{
  "name": "Rare disease cohort"
}
```

## Questions

1. Are all three documents "valid JSON"?
2. Why does each document fail the schema?

> **In the real repository:** this is still a simplified version of [`schemas/entities/cohort/schema.json`](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/entities/cohort/schema.json).

<details>
<summary>Solution</summary>

1. Yes. All three are "valid JSON", as they follow JSON format. They are simply not valid against the given "schema" we are comparing them against.
2. The first has no required `name`; the second has a number instead of a string; and the third has an extra `@id` property.

</details>
