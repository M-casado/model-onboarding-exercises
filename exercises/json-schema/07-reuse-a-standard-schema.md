# Exercise 7 - Reuse one small definition

## Goal

You will use `$ref` to select one small definition from the shared EGA schema. A reference can point to a complete schema, but it can also point to a tiny part of one.

## Prerequisites

Complete [Exercise 3](03-follow-an-internal-ref.md). Keep Biovalidator open at <http://localhost:3020> and make sure it can reach GitHub.

## Instructions

1. Take a look at the [`label` shared definition](https://github.com/EGA-archive/fega-metadata-schema/blob/4d8909ec67e8a1435aee13de93ac7b9a14d53cb1/schemas/common/schema.json#L150-L196). Ignore `meta:sssomMappings`. This shared definition says that a label is a string (``"type": "string"``) with at least one character (``"minLength": 1``).
2. In Biovalidator, put this in the **SCHEMA** input:

   ```json
   {
     "$ref": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/common/schema.json#/$defs/label"
   }
   ```

3. Replace the **DATA** input with each value below and choose **Validate** after each one.

   **DATA 1**

   ```json
   "UK Biobank Cohort"
   ```

   **DATA 2**

   ```json
   ""
   ```

## Questions

1. Which part of the `$ref` tells Biovalidator which file to fetch?
2. Which part selects `label` rather than the whole common schema?
3. How do we know that the schema is actually being applied from the source?
4. What does this show about how small a target a `$ref` can identify?

> **In the real repository:** see the [common schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/common/schema.json) and its [`label` definition](https://github.com/EGA-archive/fega-metadata-schema/blob/7f8feced9e9fef579281bbc99a182d0b1f00fe20/schemas/common/schema.json#L150-L196).

<details>
<summary>Solution</summary>

1. The URL before `#`, which points to the file `schemas/common/schema.json` of the `main` branch of the `fega-metadata-schema` repository on GitHub.
2. `#/$defs/label` is a JSON Pointer into that document, so it selects only the reusable `label` definition.
3. Because the in the SCHEMA part we have not defined what the **DATA** must be, but `"UK Biobank Cohort"` passes, while `""` does not pass, because it is a string, but it has zero characters and violates `minLength: 1`. Therefore, we know that Biovalidator is applying the rules from the `label` definition in the common schema.
4. `$ref` can reuse a complete document, an object definition, or a small nested property rule. It does not need to point only to a top-level schema.

</details>

## Concept summary

`$ref` is a pointer, not a copy. Its fragment can select a small definition inside a fetched schema, which lets many schemas share exactly the rule they need. This can be very handy for partial validations, as it enables modular schemas that can be reused in different contexts (see [graph exercise](../graph-validation/03-apply-a-graph-profile.md) as an example)
