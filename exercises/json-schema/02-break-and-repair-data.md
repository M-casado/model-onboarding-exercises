# Exercise 2 - Break and repair data

## Goal

You will see the difference between correctly written JSON and JSON that follows a schema's rules.

## Prerequisites

- Start Biovalidator using the [setup instructions](../../README.md#setup).
- Open <http://localhost:3020>.

## Instructions

1. Use these rules as the **SCHEMA** in Biovalidator:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "name": { "type": "string" }
  },
  "required": ["name"],
  "additionalProperties": false
}
```

2. Validate each of the following documents as the **DATA**.

**Document A**

```json
{}
```

**Document B**

```json
{
  "name": 12
}
```

**Document C**

```json
{
  "name": "Rare disease cohort",
  "@id": "ega:EGAH00001000001"
}
```

3. After each (presumably) failed attempt, fix it with:

```json
{
  "name": "Rare disease cohort"
}
```

## Questions

1. Are all three documents (A, B and C) written in valid JSON?
2. Which rule does each document break?
3. Which rule rejects the extra `@id` in the third example? Do all EGA v2 schemas use that rule?

> **In the real repository:** compare this teaching schema with the [current EGA Cohort schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json), which is intentionally open to undeclared properties.

<details>
<summary>Solution</summary>

1. Yes. They all use valid JSON syntax. They are simply not valid against the given "schema" we are comparing them against.
2. The first (A) has no required `name`; the second (B) uses a number instead of text; the third (C) has an extra property that is not allowed.
3. `additionalProperties: false` rejects the property `@id` here. Current EGA v2 schemas leave out this setting, so an extra property is not rejected just because the schema does not list it.

</details>

## Concept summary

When you add something into the **DATA** or **SCHEMA** boxes in Biovalidator, you are essentially asking _"Can this be read as JSON?"_. When you click on **Validate**, you ask, _"Does this JSON data follow this JSON schema?"_.

This mock schema makes errors easy for you to see. Real models often leave room for extra fields. [Exercise 5](./05-open-and-closed-object-schemas.md) looks at that choice directly.
