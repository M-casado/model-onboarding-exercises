# Exercise 6 - Expand JSON-LD

## Goal

Read expanded JSON-LD and connect it to simple RDF statements.

## Instructions

1. Open the [JSON-LD Playground](https://json-ld.org/playground/) and paste this document.

```json
{
  "@context": {
    "ega": "https://identifiers.org/ega:",
    "schema": "http://schema.org/",
    "name": "schema:name"
  },
  "@id": "ega:EGAH00001000001",
  "@type": "ega:cohort",
  "name": "Rare disease cohort"
}
```

2. Select the **Expanded** tab. Find the expanded identifier, type, and name property.
3. Select the **N-Quads** tab. Find the statement about the Cohort's name.

## Questions

1. Which expanded value identifies the Cohort?
2. In the name statement, what are the subject, predicate, and object? These form an RDF triple.

> **In the real repository:** the [minimal Cohort example](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/entities/cohort/examples/valid/cohort-valid-minimal-study-defined.json) uses the real schema as its JSON-LD context.

<details>
<summary>Solution</summary>

1. `https://identifiers.org/ega:EGAH00001000001` identifies the Cohort.
2. The subject is that Cohort identifier, the predicate is `http://schema.org/name`, and the object is `Rare disease cohort`. So you can interpret it as the following phrase:
    - "The cohort ``https://identifiers.org/ega:EGAC00001000001``" (subject)
    - "Has a ``https://schema.org/name``" (predicate)
    - "With value ``Rare disease cohort``" (object)

</details>
