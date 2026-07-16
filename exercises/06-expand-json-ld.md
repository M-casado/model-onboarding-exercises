# Exercise 6 - Expand JSON-LD

## Goal

Read expanded JSON-LD and connect it to simple RDF statements.

## Instructions

1. Open the [JSON-LD Playground](https://json-ld.org/playground/) and paste this document.

```json
{
  "@context": {
    "ega": "https://identifiers.org/ega:",
    "schema": "https://schema.org/",
    "Cohort": "https://example.org/fega/Cohort",
    "name": "schema:name"
  },
  "@id": "ega:EGAC00001000001",
  "@type": "Cohort",
  "name": "Rare disease cohort"
}
```

2. Select **Expanded** tab. Check how the expanded identifier, type, and name properties look like when expanded.
3. Select **N-Quads** tab. Knowing how the expanded terms look like, find the statement about the Cohort's name in this format.

## Questions

1. Which expanded value identifies the Cohort?
2. In the name statement, what are the subject, predicate, and object? These are the typical RDF triplets.

> **In the real repository:** the [minimal Cohort example](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/entities/cohort/examples/valid/cohort-valid-minimal-study-defined.json) can also be expanded through its JSON-LD context.

<details>
<summary>Solution</summary>

1. `https://identifiers.org/ega:EGAC00001000001` identifies the Cohort.
2. The subject is that Cohort identifier (as above), the predicate is `https://schema.org/name`, and the object is `Rare disease cohort`. So you can interpret it as the following phrase:
  - "The cohort ``https://identifiers.org/ega:EGAC00001000001``" (subject)
  - "Has a ``https://schema.org/name``" (predicate)
  - "With value ``Rare disease cohort``" (object)

</details>
