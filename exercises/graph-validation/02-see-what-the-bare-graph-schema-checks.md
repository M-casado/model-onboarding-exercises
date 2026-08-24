# Exercise 2 - See what the bare graph schema checks

## Goal

See the minimum job of `graph/schema.json`: it checks that **all entities** in
the graph box are individually valid against the entity schema selected by
each entity's `@type`.

It does not say which combination of entities makes a complete submission.

## Prerequisites

- Complete [Exercise 1](01-put-entities-in-a-graph-box.md).
- Keep Biovalidator running.

## Instructions

1. In Biovalidator, choose **Fetch examples**, select
   `graph: graph-valid-minimal.json`, and choose **Load example**. Confirm that
   **SCHEMA** contains this bare graph schema reference:

   ```json
   {
     "$ref": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/graph/schema.json"
   }
   ```

2. Choose **Validate**. The one entity in the box is a DAC, so the example
   should pass.
3. In **DATA**, find this exact fragment:

   ```json
         "@type": "ega:DAC",
   ```

   Change the `@type` line to this:

   ```json
         "@type": "ega:datafile",
   ```

   Leave everything else unchanged.
4. Choose **Validate** again. What is the result? Why?

## Questions

1. Why does changing only `@type` make the entity fail?
2. What does the **bare graph schema** check for every entity in the box?

<details>
<summary>Solution</summary>

1. `@type` selects the entity rules. Changing `ega:DAC` to `ega:datafile`
   routes the object to the [Datafile schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/datafile/schema.json), while its DAC fields remain and the datafile fields are missing.
2. It checks that every item has a supported type and is individually valid
   against that type's schema.

</details>

## Concept summary

`graph/schema.json` is the basic tool for validating a bundle of EGA entities:
it opens the box, reads each item's `@type`, and checks that item against the
matching entity rules. It is not a submission-completeness checklist without profiles (see [exercise 03](./03-apply-a-graph-profile.md)).
