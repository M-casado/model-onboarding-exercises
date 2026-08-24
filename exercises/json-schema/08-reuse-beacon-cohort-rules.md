# Exercise 8 - Reuse Beacon Cohort rules

## Goal

You will see how the EGA Cohort schema makes an EGA Cohort compatible with the Beacon Cohort schema, then validate the same example directly against Beacon's schema.

## Prerequisites

- Complete [Exercise 4](04-resolve-a-relative-ref.md).
- Open Biovalidator at <http://localhost:3020>.

## Instructions

1. Open the [EGA Cohort schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json) in your browser. Find `cohorts/defaultSchema.json`.
2. Read the surrounding `allOf` item:

   ```json
   {
     "title": "Compatibility with Beacon v2 JSON Schema",
     "$ref": "../../../standards/json-schema/beacon-v2/models/json/beacon-v2-default-model/cohorts/defaultSchema.json"
   }
   ```

   `allOf` means that the EGA Cohort must satisfy this Beacon schema as well as the _other_ EGA rules. Note that, since it's a relative path, the copied Beacon file is under `standards/` in the FEGA repository: it is not fetched from the upstream Beacon repository.
3. In Biovalidator, choose **Fetch examples**, select `cohort: cohort-valid-minimal-study-defined.json`, and choose **Load example**.
4. Leave the loaded value in **Data**, but replace the **Schema** input with this wrapper:

   ```json
   {
     "$ref": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/standards/json-schema/beacon-v2/models/json/beacon-v2-default-model/cohorts/defaultSchema.json"
   }
   ```

5. Choose **Validate**. The EGA example should pass.

## Questions

1. Where does the Cohort schema put the Beacon `$ref`, and what does `allOf` do with it?
2. Why are we using the ``beacon-v2-default-model/cohorts/defaultSchema.json`` from the `standards/` folder of the FEGA repository rather than the [upstream Beacon repository](https://github.com/ga4gh-beacon/beacon-v2/blob/main/models/json/beacon-v2-default-model/cohorts/defaultSchema.json)?
3. What does a successful validation in step 5 prove? What additional rules would you check by validating against the EGA Cohort schema too?

> **In the real repository:** see the [Cohort schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json) and the [vendored Beacon Cohort schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/standards/json-schema/beacon-v2/models/json/beacon-v2-default-model/cohorts/defaultSchema.json).

<details>
<summary>Solution</summary>

1. The Beacon reference is one item in the Cohort schema's top-level `allOf` list. `allOf` combines the constraints, so a valid EGA Cohort must also satisfy Beacon's constraints.
2. The FEGA copy (the one within ``standards/``) is a reviewed snapshot selected by the FEGA repository. It gives the EGA schema a known standard version and keeps validation reproducible. The upstream Beacon repository may change over time, which could break the EGA schema's validation if it were to fetch the latest version.
3. It proves that the loaded example DATA satisfies Beacon's Cohort rules. It does not, by itself, prove that the example satisfies every EGA and JSON-LD rule: the EGA Cohort schema adds those checks, not the bare Beacon schema we used in this exercise.

</details>

## Concept summary

An `allOf` reference can make one schema a compatible extension of another. You can also validate against the referenced schema alone to check the shared standard independently.
