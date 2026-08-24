# Exercise 1 - Load a real EGA v2 example

## Goal

You will use the Biovalidator web page to load a current EGA v2 example and check it with a schema stored online.

## Prerequisites

- Start Biovalidator using the [setup instructions](../../README.md#setup).
- Open <http://localhost:3020>.

## Instructions

1. Open <http://localhost:3020>.
2. Select **Fetch examples**.
3. Select `cohort: cohort-valid-minimal-study-defined.json`, then choose **Load example**.
4. Look at the **SCHEMA** input. It should be a small wrapper like this:

   ```json
   {
     "$ref": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/entities/cohort/schema.json"
   }
   ```

5. Look at the **DATA** input and select **Validate**.

6. Play around by selecting other examples, loading them, and validating them.

## Questions

1. Why does the **Schema** input contain only a `$ref`?
2. What does Biovalidator download and turn into a validator when you choose **Validate**?
3. Why are subsequent validation attempts much faster than the first one?

> **To see the full version:** open the [EGA v2 Cohort examples](https://github.com/EGA-archive/fega-metadata-schema/tree/main/schemas/entities/cohort/examples/valid) and the [Cohort schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json).

<details>
<summary>Solution</summary>

1. What we are telling Biovalidator is essentially "go to this URL, get the content, and use it as a schema". The `$ref` is a pointer to the real schema, which is stored online in the FEGA repository. The wrapper (``{ "$ref": "..." }``) is a small JSON object that contains only the `$ref` key, which is enough for Biovalidator to find and load the full schema.
2. Biovalidator gets the [Cohort schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json), follows its relative links (i.e., `$ref` pointers within it) to [common](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/common/schema.json) and [standard](https://github.com/EGA-archive/fega-metadata-schema/tree/main/standards) rules, builds a validator from them, and checks the example data.
3. The first time you validate, Biovalidator has to download the schema and all its dependencies, then build a validator. After that, it keeps the validator in memory, so subsequent validations can skip the download and build steps.

</details>

## Concept summary

Using `$ref` pointers, you can send a pointer to shared rules instead of copying all the rules into every request. Biovalidator follows the pointer and gathers the other needed rules. It then checks your data against the complete set.
