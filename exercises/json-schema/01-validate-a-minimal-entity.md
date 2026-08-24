# Exercise 1 - Validate a minimal entity

## Goal

You will validate a small JSON object and tell the rules apart from the data.

## Prerequisites

- Start Biovalidator using the [setup instructions](../../README.md#setup).
- Open <http://localhost:3020>.

## Instructions

1. Paste these rules into the **SCHEMA** input:

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

2. Paste this data into the **DATA** input (the document to check), then click **Validate**:

```json
{
  "name": "Rare disease cohort"
}
```
> It should look something like the following:
![Biovalidator exercise 1](../../img/biovalidator-ex1.png)

3. Replace the **DATA** input with the following and validate it again:

```json
{
  "name": true
}
```

## Questions

1. Which line says that `name` is required?
2. Why does the first document (i.e., **DATA**) pass and the second one fail?

> **In the real repository:** this is a simplified teaching version of the [Cohort schema at the EGA Archive](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json).

<details>
<summary>Solution</summary>

1. `"required": ["name"]` makes `name` mandatory.
2. The first value is a string, as required by the `type` constraint. `true` is a Boolean, so the second document does not satisfy the schema.

</details>

## Concept summary

Think of JSON as a way to write data. A JSON Schema is a separate set of rules about that data.

For example, it can say which fields you need and what type each value must have.

Note that you can write a document correctly as JSON and still fail these rules.
