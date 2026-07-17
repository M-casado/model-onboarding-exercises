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
    "@id": { "$ref": "#/$defs/cohortIdentifier" },
    "externalIdentifier": { "type": "string", "format": "uri" }
  },
  "required": ["@id", "externalIdentifier"],
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
  "@id": "ega:EGAH00001000001",
  "externalIdentifier": "https://example.org/cohorts/rare-disease-1"
}
```

3. Now paste and validate these two alternatives.

```json
{
  "@id": "ega:EGAD00001000001",
  "externalIdentifier": "https://example.org/cohorts/rare-disease-1"
}
```

```json
{
  "@id": "https://example.org/cohorts/rare-disease-1",
  "externalIdentifier": "https://example.org/cohorts/rare-disease-1"
}
```

## Questions

1. Why does the external URL work in `externalIdentifier` but not in `@id`?
2. What tells the validator that `EGAD` is not a Cohort accession?

> **In the real repository:** [`externalIdentifier`](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/common/schema.json#L10-L36) accepts external URI or CURIE values, while [`egaStableIdentifierCohort`](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/common/schema.json#L4061-L4074) restricts Cohort identities to `EGAH`.

<details>
<summary>Solution</summary>

1. `externalIdentifier` accepts a URI (because of its ``"format": "uri"``), while `@id` has to match the EGA Cohort pattern in this schema (``"pattern": "^ega:EGAH[0-9]{11}$"``).
2. The pattern in `cohortIdentifier` specifically requires `ega:EGAH`. `EGAD` is a valid EGA Dataset prefix, but it is wrong for a Cohort.

</details>
