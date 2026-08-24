# Exercise 3 - Frame JSON-LD

## Goal

You will use a frame to show one Cohort together with its related Biomaterial.

## Prerequisites

Complete [Exercise 2](02-expand-json-ld.md) and open the [JSON-LD Playground](https://json-ld.org/playground/). This exercise will be easier to understand if you have finished the [``graph-validation``](../graph-validation/) exercises.

## Instructions

1. Paste this exact graph into the **JSON-LD Input** of the [JSON-LD Playground](https://json-ld.org/playground/):

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

2. Select the tab **Framed**. It will open a new input tab, which is called **JSON-LD Frame**. Paste the following into it:

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

3. Take a look at the result in **Framed**, and how the two individual nodes of the ``@graph`` are being "reshaped" (i.e., framed).

4. Swap the top-level object from `"ega:cohort"` to `"ega:biomaterial"`. To do so, replace the existing **JSON-LD Frame** content with the following:
    ```json
    {
      "@context": {
        "ega": "https://identifiers.org/ega:",
        "schema": "http://schema.org/",
        "name": "schema:name"
      },
      "@type": "ega:biomaterial"
    }
    ```

5. After pasting the new frame, observe the result in the **Framed** tab and check which of the two ``@graph`` nodes from the original input is being framed and which one is not.

## Questions

1. Which **line** in the **JSON-LD Frame** decides which item appears at the top of the framed result?
2. Does a successful frame prove that the data follows an EGA JSON Schema?

> **In the real repository:** see the Cohort's [context](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/context.jsonld) and [frame](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/frame.jsonld), which allow for us to reconstruct 'what EGA understands as an ega:cohort' from a graph of nodes.

<details>
<summary>Solution</summary>

1. The frame's top-level `@type` selects the item at the top. Changing it from Cohort to Biomaterial changes the focus of the framing process.
2. **No**. Framing only selects and rearranges graph data. You still need a separate JSON Schema check.

</details>

## Concept summary

You will often see linked data stored as a flat list of facts so relationships are clear. A frame is a _view_ of that graph: it selects the facts you want and nests them in a useful way.

Nevertheless, it changes the display, not the facts or whether they pass validation.
