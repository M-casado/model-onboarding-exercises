# Exercise 7 - Frame JSON-LD

## Goal

Use a frame to select a Cohort and show its related Biomaterial underneath it.

## Instructions

1. Open the [JSON-LD Playground](https://json-ld.org/playground/). Paste this graph into the JSON-LD input.

```json
{
  "@context": {
    "ega": "https://identifiers.org/ega:",
    "schema": "https://schema.org/",
    "Cohort": "https://example.org/fega/Cohort",
    "Biomaterial": "https://example.org/fega/Biomaterial",
    "name": "schema:name",
    "member": {
      "@id": "https://example.org/fega/member",
      "@type": "@id"
    }
  },
  "@graph": [
    {
      "@id": "ega:EGAC00001000001",
      "@type": "Cohort",
      "name": "Rare disease cohort",
      "member": "ega:EGAN00000000001"
    },
    {
      "@id": "ega:EGAN00000000001",
      "@type": "Biomaterial",
      "name": "Participant 1"
    }
  ]
}
```

2. Familiarise yourself with the ``@graph``, which has two nodes (one cohort and one biomaterial).
3. Select **Framed** output. Paste this into the frame input (``JSON-LD Frame``).

```json
{
  "@context": {
    "ega": "https://identifiers.org/ega:",
    "schema": "https://schema.org/",
    "Cohort": "https://example.org/fega/Cohort",
    "Biomaterial": "https://example.org/fega/Biomaterial",
    "name": "schema:name",
    "member": {
      "@id": "https://example.org/fega/member",
      "@type": "@id"
    }
  },
  "@type": "Cohort",
  "@explicit": true,
  "name": {},
  "member": {
    "@embed": "@always",
    "@explicit": true,
    "@type": "Biomaterial",
    "name": {}
  }
}
```

4. See the framing. Now the JSON data is no longer a flat ``@graph``, but instead a "reconstructed" JSON-LD data representing the cohort. Furthermore, now the Cohort should contain the Biomaterial as a member.
5. Change the frame's top-level `@type` from `Cohort` to `Biomaterial`, then frame again.

## Questions

1. What decides which resource appears at the top of the result?
2. Does a successful frame prove that the data is valid against a JSON Schema?

> **In the real repository:** Cohort has a [`frame.jsonld`](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/entities/cohort/frame.jsonld). The repository validates framed data again afterwards.

<details>
<summary>Solution</summary>

1. The frame's top-level `@type` selects the Cohort or Biomaterial.
2. No. Framing arranges graph data; it does not validate it against a JSON Schema.

</details>
