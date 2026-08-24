# Exercise 4 - Resolve a relative `$ref`

## Goal

You will see how a real EGA schema finds a rule in another file. Its `$id` tells the validator where relative paths start.

## Prerequisites

- Complete [Exercise 3](03-follow-an-internal-ref.md).
- Keep Biovalidator running and ensure GitHub access.

## Instructions

1. Open the [Cohort schema](https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/entities/cohort/schema.json).
2. Find (use **Ctrl+F**) its `$id`. This is the schema's own unique identifier, which _coincidentally_ is also a resolvable URL. Also find a relative reference like this:

   ```text
   ../../common/schema.json#/$defs/relationshipItemRestrictionCohort
   ```

3. Work out the full **raw URL** for that reference. In essence, if you were Biovalidator, and you saw that reference inside the [Cohort schema](https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/entities/cohort/schema.json), where would you go to fetch the definition named `relationshipItemRestrictionCohort`?

   (_Hint_: start from the `$id` URL, go up two folders, then open `common/schema.json`.)

4. In Biovalidator, choose **Fetch examples**, select `cohort-valid-minimal-study-defined.json`, and choose **Load example**. The example is also available [here](https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/entities/cohort/examples/valid/cohort-valid-minimal-study-defined.json).
   
   Then validate it.

## Questions

1. Why does the **Schema** input contain only a `$ref` instead of the full Cohort schema?
2. What does Biovalidator download and turn into a validator when you choose **Validate**?
3. Which field tells the validator what a relative path starts from?
4. If you click **Validate** again, does Biovalidator download the schema again, or does it use a saved copy?

> **To see the full version:** open the [Cohort schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json) and its [common schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/common/schema.json).

<details>
<summary>Solution</summary>

1. The `$ref` points to the raw Cohort schema on GitHub. It keeps the request short and avoids pasting a large schema into the UI.
2. Biovalidator fetches (i.e., downloads) the [Cohort schema](https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/entities/cohort/schema.json), follows its other references (e.g., `../../common/schema.json`), builds one validator from all those rules, and only then, with all the pieces compiled, checks if the data complies with the schema.
3. The Cohort schema's absolute `$id` is the starting URL. From it, `../../common/schema.json` becomes `https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/common/schema.json`.
4. Biovalidator downloads the schema once and saves it for a while, to avoid unnecessary downloads. A later check can use the saved copy, so the process is much faster.

</details>

## Concept summary

You can use relative references to make several schema files work like folders and files on your computer. `$id` tells the validator how to turn a short path into a full URL.

The part after `#` then picks a rule inside that file.

If the file is not already registered or saved, Biovalidator downloads it, checks its `$id`, saves it, and then follows any references inside it for you.

Do not confuse `$id` with `@id` in the data. The former is a schema property, while the latter is a data property. The `$id` is used to give the schemas their identity, while `@id` is used to identify a specific entity in the data.
