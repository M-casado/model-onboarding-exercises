# Exercise 8 - Compare with the real repository

## Goal

Find the real resources that the simplified Cohort exercises represent.

## Instructions

1. Open the real [Cohort directory](https://github.com/M-casado/fega-metadata-schema/tree/main/schemas/entities/cohort).
2. Open its [`schema.json`](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json), [`context.jsonld`](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/entities/cohort/context.jsonld), and [`frame.jsonld`](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/entities/cohort/frame.jsonld).
3. Compare the [minimal valid example](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/entities/cohort/examples/valid/cohort-valid-minimal-study-defined.json) with an [invalid example](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/entities/cohort/examples/invalid/cohort-invalid-type-hadMember.json).
4. In `schema.json`, find a `$ref` into the [shared schema](https://github.com/M-casado/fega-metadata-schema/blob/main/schemas/common/schema.json). If Biovalidator accepts a schema URL, try the real minimal example there.

## Questions

1. Which file gives the Cohort JSON-LD terms their meanings?
2. What is one rule in the real schema that the teaching schemas leave out?

> **In the real repository:** this exercise compares the simplified examples with [`schemas/entities/cohort/`](https://github.com/M-casado/fega-metadata-schema/tree/main/schemas/entities/cohort). The model is still under development, so files and rules may change.

<details>
<summary>Solution</summary>

1. `context.jsonld` provides the JSON-LD mappings.
2. The real Cohort schema combines JSON-LD, shared, and Beacon v2 constraints through `$ref`, while the teaching schemas show only one idea at a time.

</details>
