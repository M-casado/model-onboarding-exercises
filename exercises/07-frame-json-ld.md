# Exercise 7 - Frame JSON-LD

## Goal

Use a frame to select a Cohort and show its related Biomaterial underneath it.

## Instructions

1. Open the [JSON-LD Playground](https://json-ld.org/playground/). Paste this graph into the JSON-LD input.

```json
{
  "@context": {
    "ega": "https://identifiers.org/ega:",
    "schema": "http://schema.org/",
    "prov": "https://www.w3.org/ns/prov#",
    "name": "schema:name",
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id",
      "@container": "@set"
    }
  },
  "@graph": [
    {
      "@id": "ega:EGAH00001000001",
      "@type": "ega:cohort",
      "name": "Rare disease cohort",
      "hadMember": ["ega:EGAN00000000001"]
    },
    {
      "@id": "ega:EGAN00000000001",
      "@type": "ega:biomaterial",
      "name": "Participant 1"
    }
  ]
}
```

2. Familiarise yourself with `@graph`, which contains two nodes: one Cohort and one Biomaterial.
3. Select the **Framed** tab. Paste this into the **JSON-LD Frame** input.

```json
{
  "@context": {
    "ega": "https://identifiers.org/ega:",
    "schema": "http://schema.org/",
    "prov": "https://www.w3.org/ns/prov#",
    "name": "schema:name",
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id",
      "@container": "@set"
    }
  },
  "@type": "ega:cohort",
  "@explicit": true,
  "name": {},
  "hadMember": [
    {
      "@embed": "@always",
      "@explicit": true,
      "@type": "ega:biomaterial",
      "name": {}
    }
  ]
}
```

4. Check the **Framed** tab. The flat graph is reconstructed around the Cohort, with the Biomaterial embedded under `hadMember`.
5. In the **JSON-LD Frame** input, replace this line:

```text
"@type": "ega:cohort",
```

with this line, then frame again:

```text
"@type": "ega:biomaterial",
```

## Questions

1. What decides which resource appears at the top of the result?
2. Does a successful frame prove that the data is valid against a JSON Schema?

> **In the real repository:** Cohort constrains [`hadMember`](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/entities/cohort/schema.json#L60-L69), maps it to [`prov:hadMember`](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/entities/cohort/context.jsonld#L21-L24), and includes it in the [Cohort frame](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/entities/cohort/frame.jsonld#L27-L31).

<details>
<summary>Solution</summary>

1. The frame's top-level `@type` selects the Cohort or Biomaterial.
2. No. Framing selects and arranges graph data. We need to validate it against a JSON Schema later if we want to assert compliance.

</details>
