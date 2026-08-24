# Exercise 2 - Expand JSON-LD

## Goal

You will read expanded JSON-LD and turn one value into a simple RDF statement. RDF (Resource Description Framework) is a way to write linked facts.

## Prerequisites

- Complete [Exercise 1](01-add-json-ld-meaning.md).
- Open the [JSON-LD Playground](https://json-ld.org/playground/).

## Instructions

1. Open the [JSON-LD Playground](https://json-ld.org/playground/) and paste this exact document:

   ```json
   {
    "@context": {
      "ega": "https://identifiers.org/ega:",
      "schema": "http://schema.org/",
      "name": "schema:name"
    },
    "@id": "ega:EGAN00004248884",
    "name": "AngH325"
   }
   ```

2. Select **Expanded**. Find the full (i.e., expanded) identifier (``@id``) and ``name`` fields.
3. Select **N-Quads** tab, you should see something similar to the line below. What does that line imply?

    ```
    <https://identifiers.org/ega:EGAN00004248884> <http://schema.org/name> "AngH325" .
    ```

    _Hint_: N-Quads writes one graph fact per line in the format of ``subject-predicate-object`` triplets (e.g., ``potato-is-aVegetable``).

## Questions

1. Which full value identifies the sample record ``EGAN00004248884``?
2. In the N-quads line, which part is the subject, which is the predicate, and which is the object?

> **To see the full version:** open the [minimal Cohort example](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/examples/valid/cohort-valid-minimal-study-defined.json).

<details>
<summary>Solution</summary>

1. The identifier expands to `https://identifiers.org/ega:EGAN00004248884`. 

    If you try to resolve that link (i.e., click on it), you will see that it leads first to identifiers.org, and then it redirects to EGA's metadata API, which finally provides the sample record for ``EGAN00004248884``.

2. The **subject** is the sample record's identifier `https://identifiers.org/ega:EGAN00004248884`, the **predicate** is `http://schema.org/name`, and the **object** is the text `AngH325`. Together they make one RDF statement (also called a triple) that _computers_ can easily understand as a graph fact.

    For us humans, this statement can be read as "the particular record ``EGAN00004248884`` - has as ``name`` - the value ``AngH325``".

</details>

## Concept summary

When you expand JSON-LD, short names are replaced with full names so the graph is clear to a computer. N-Quads then writes each fact as subject–predicate–object, one line at a time.
