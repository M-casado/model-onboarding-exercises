# Exercise 5 - Add JSON-LD meaning

## Goal

Use a context to give JSON names shared meanings.

## Instructions

1. Open the [JSON-LD Playground](https://json-ld.org/playground/). Paste this document into the JSON-LD input.

```json
{
  "@context": {
    "ega": "https://identifiers.org/ega:",
    "schema": "https://schema.org/",
    "name": "schema:name",
    "Cohort": "https://example.org/fega/Cohort"
  },
  "@id": "ega:EGAC00001000001",
  "@type": "Cohort",
  "name": "Rare disease cohort"
}
```

2. Select **Expanded** output.
3. IN the part that you pasted in JSON-LD Input, remove the `name` line (the whole line) from `@context`, then take a look at the Expanded tab again.

## Questions

1. Which entries in the context are prefixes?
2. What happens to `name` after its mapping is removed? How does that impact the readability of the data?

> **In the real repository:** Cohort has its own [`context.jsonld`](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/entities/cohort/context.jsonld), which builds on the [shared context](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/common/context.jsonld).

<details>
<summary>Solution</summary>

1. `ega` and `schema` are prefixes in `@context`, and they are replaced by their values when expanded: `name` becomes `schema:name`, which then becomes `https://schema.org/name`.
2. Without its mapping, `name` has no absolute meaning and does not appear in the expanded output. If there is no expanded `name`, then a _machine_ reading the code cannot understand that `name` is not just a string, but it has the semantic meaning of `https://schema.org/name`.

</details>
