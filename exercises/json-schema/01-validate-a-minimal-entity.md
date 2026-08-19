# Exercise 1 - Validate a minimal entity

## Goal

Validate a small Cohort-like object and distinguish a schema from its data.

## Prerequisites

Start Biovalidator from the [workshop setup](../../README.md#setup) and open <http://localhost:3020>.

## Instructions

1. Paste this schema into the ``SCHEMA`` input:

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

2. Paste this data into the ``DATA`` input (a.k.a. document) and then click ``Validate``:

```json
{
  "name": "Rare disease cohort"
}
```
> It should look something like the following:
![Biovalidator exercise 1](../../img/biovalidator-ex1.png)

3. Replace the ``DATA`` input with the following and validate again:

```json
{
  "name": true
}
```

## Questions

1. Which part says that `name` must be present?
2. Why is one value valid and the other invalid?

> **In the real repository:** this is a simplified teaching version of the [Cohort schema at the EGA Archive](https://github.com/EGA-archive/fega-metadata-schema/blob/ad5ba2a7ebc2b42c6f4a5cf54aa697e6e8a1a713/schemas/entities/cohort/schema.json).

<details>
<summary>Solution</summary>

1. `"required": ["name"]` makes `name` mandatory.
2. The first value is a string, as required by the `type` constraint. `true` is a Boolean, so the second document does not satisfy the schema.

</details>

## Concept in plain English

JSON is a notation for data. A JSON Schema is a separate set of rules that says what shape and value types that data may have. A document can be valid JSON while still failing a schema.
