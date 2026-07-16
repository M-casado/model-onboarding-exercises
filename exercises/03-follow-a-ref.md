# Exercise 3 - Follow a `$ref`

## Goal

Use a shared identifier rule through `$ref`.

## Instructions

1. In [Biovalidator](http://localhost:3020), paste this schema.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "id": { "$ref": "#/$defs/cohortIdentifier" }
  },
  "required": ["id"],
  "additionalProperties": false,
  "$defs": {
    "cohortIdentifier": {
      "type": "string",
      "pattern": "^ega:EGAC[0-9]{11}$"
    }
  }
}
```

2. Paste and validate this data.

```json
{
  "id": "ega:EGAC00001000001"
}
```

3. Now validate this data.

```json
{
  "id": "ega:EGAD00001000001"
}
```

## Questions

1. Which property uses the shared definition?
2. Where is the rule that accepts `EGAC` but rejects `EGAD`?

> **In the real repository:** entity schemas use shared definitions from [`schemas/common/schema.json`](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/common/schema.json). This exercise uses `$defs` so everything can be pasted into Biovalidator at once.

<details>
<summary>Solution</summary>

1. `id` uses the shared definition.
2. The `id` property points to `#/$defs/cohortIdentifier`. Its `pattern` requires `ega:EGAC` followed by 11 digits.

</details>
