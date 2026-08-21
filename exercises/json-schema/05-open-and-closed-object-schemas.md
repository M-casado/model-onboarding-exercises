# Exercise 5 - Open and closed object schemas

## Goal

You will see why leaving out `additionalProperties: false` allows both useful extra fields and accidental typos.

## Prerequisites

Start Biovalidator from the [workshop setup](../../README.md#setup) and open <http://localhost:3020>.

## Instructions

1. Start with these open rules. They do not mention `additionalProperties`:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "biologicalSex": { "type": "string" }
  }
}
```

2. Try these documents:

**Document A**:
```json
{
  "biologicalSex": "male"
}
```
**Document B**:
```json
{
  "biologicalSex": "male",
  "phenotypeExtension": {
    "height": 180,
    "weight": 75,
    "notes": "..."
  }
}
```
**Document C**:
```json
{
  "biologicaSlex": 123
}
```

3. Replace the rules with this closed version, then check the same three documents again:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "biologicalSex": { "type": "string" }
  },
  "required": ["biologicalSex"],
  "additionalProperties": false
}
```

## Questions

1. Why does the typo (i.e., `biologicaSlex` instead of `biologicalSex`) of document C pass when the object is open?
2. What changes when `additionalProperties` is set to `false`? What happens to document B, which has an extra field `phenotypeExtension` and document C, which has a typo in the field name?
3. What are the advantages and disadvantages of each approach (closed vs open)?

> **In the real repository:** EGA v2 entity schemas such as [Cohort](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json) generally do not set `additionalProperties` to `false`.

<details>
<summary>Solution</summary>

1. Object rules check the fields they list, but extra fields are allowed by default. The validator cannot know that `biologicaSlex` was meant to be `biologicalSex`, and thus it inadvertantly allows the typo, because for the validator, the wrong string is simply a complete different property.
2. `additionalProperties: false` rejects both `biologicaSlex` and `phenotypeExtension` because the rules do not list them.
3. The advantage of a closed object is that it catches typos and unknown fields. The disadvantage is that it does not allow extensions. An open object allows extensions, but it does not catch typos.

</details>

## Concept summary

When you use an **open object** (i.e., without `additionalProperties: false`), you are saying, "check the fields I describe, and allow other fields". A **closed object** (i.e., with `additionalProperties: false`) says, "only the listed fields are allowed".

Open schemas are easier for you to extend. Closed schemas catch unknown keys sooner. **Extensions are useful to EGA** because they allow the community to add new fields without waiting for the schema to be updated, and for EGA to reuse existing fields avoiding breaking incompatibilities across standards. For example, if an institution using the EGA schemas has the need to add some extra fields that are not pertinent to EGA, they can add them without needing the base EGA schema to be updated.

Neither choice knows what you intended. If you need typo detection at a boundary, you can add a stricter layer or use a tool that checks the vocabulary separately.
