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
    "@id": { "$ref": "#/$defs/cohortIdentifier" }
  },
  "required": ["@id"],
  "additionalProperties": false,
  "$defs": {
    "cohortIdentifier": {
      "type": "string",
      "pattern": "^ega:EGAH[0-9]{11}$"
    }
  }
}
```

2. Paste and validate this data.

```json
{
  "@id": "ega:EGAH00001000001"
}
```

3. Now paste and validate this data.

```json
{
  "@id": "ega:EGAD00001000001"
}
```

## Questions

1. Which property uses the shared definition?
2. Where is the rule that accepts `EGAH` but rejects `EGAD`?

> **In the real repository:** [`egaStableIdentifierCohort`](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/common/schema.json#L4061-L4074) defines the Cohort identifier pattern. This exercise uses `$defs` so everything can be pasted into Biovalidator at once.

<details>
<summary>Solution</summary>

1. `@id` uses the shared definition ``cohortIdentifier``.
2. `@id` points to `#/$defs/cohortIdentifier`. Its `pattern` requires `ega:EGAH` followed by 11 digits. `EGAD` identifies a Dataset, not a Cohort.

</details>
