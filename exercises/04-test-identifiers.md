# Exercise 4 - Test identifiers

## Goal

See that an identifier can be valid in general but not valid for a particular property.

## Instructions

1. In [Biovalidator](http://localhost:3020), paste this schema.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "id": { "$ref": "#/$defs/cohortIdentifier" },
    "sameAs": { "type": "string", "format": "uri" }
  },
  "required": ["id", "sameAs"],
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
  "id": "ega:EGAC00001000001",
  "sameAs": "https://example.org/cohorts/rare-disease-1"
}
```

3. Now validate these two alternatives.

```json
{
  "id": "ega:EGAD00001000001",
  "sameAs": "https://example.org/cohorts/rare-disease-1"
}
```

```json
{
  "id": "https://example.org/cohorts/rare-disease-1",
  "sameAs": "https://example.org/cohorts/rare-disease-1"
}
```

## Questions

1. Why does the external URL work in `sameAs` but not in `id`?
2. What tells the validator that `EGAD` is not a Cohort accession?

> **In the real repository:** entity and relationship rules are shared through [`schemas/common/schema.json`](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/common/schema.json).

<details>
<summary>Solution</summary>

1. `sameAs` accepts any URI, while `id` has to match the EGA Cohort pattern.
2. The pattern in `cohortIdentifier` specifically requires `ega:EGAC` (with a C, not with a D).

</details>
