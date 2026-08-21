# Exercise 6 - Test entity identifiers

## Goal

You will see that the same-looking identifier can be right for one field and wrong for another.

## Prerequisites

Start Biovalidator from the [workshop setup](../../README.md#setup) and open <http://localhost:3020>.

## Instructions

1. Use these simplified rules:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://mytest-github.com/schemas/entities/cohort/schema.json",
  "type": "object",
  "properties": {
    "@id": { "$ref": "#/$defs/cohortIdentifier" },
    "externalIdentifier": { "format": "uri" }
  },
  "required": ["@id", "externalIdentifier"],
  "additionalProperties": false,
  "$defs": {
    "cohortIdentifier": {
      "type": "string",
      "pattern": "^ega:EGAH[0-9]{11}$"
    }
  }
}
```

2. Replace the **DATA** input with each of these examples, one at a time, and choose **Validate** after each replacement:

```json
{
  "@id": "ega:EGAH00001000001",
  "externalIdentifier": "https://example.org/cohorts/rare-disease-1"
}
```

```json
{
  "@id": "https://example.org/cohorts/rare-disease-1",
  "externalIdentifier": "https://example.org/cohorts/rare-disease-1"
}
```

## Questions

1. Why does the external URL (``https://example.org/cohorts/rare-disease-1``) work in `externalIdentifier` but not in `@id`?
2. How is the schema's `$id` different from the data item's JSON-LD `@id`?
3. Why does the validation not fail if the `$id` in the schema is a made-up non-resolvable URL?
4. In what scenario(s) would the `$id` _**need**_ to be resolvable for the validation to work?

> **In the real repository:** see the [shared `externalIdentifier` definition](https://github.com/EGA-archive/fega-metadata-schema/blob/4d8909ec67e8a1435aee13de93ac7b9a14d53cb1/schemas/common/schema.json#L11-L39) and the shared [`egaStableIdentifierCohort`](https://github.com/EGA-archive/fega-metadata-schema/blob/4d8909ec67e8a1435aee13de93ac7b9a14d53cb1/schemas/common/schema.json#L4757-L4770) definition used to constraint the `@id` field for Cohort entities.

<details>
<summary>Solution</summary>

1. `externalIdentifier` accepts a web URL given its ``format: uri``. On the other hand, in these example rules, `@id` must match the Cohort identifier pattern (``ega:EGAH[0-9]{11}``) instead of a web URL.
2. JSON Schema `$id` names **the schema** and helps find other schema files (see [exercise 4](./04-resolve-a-relative-ref.md)). The data item's `@id` names **that item** in JSON-LD. They identify different things, and are used for different purposes.
3. The `$id` in the schema is a logical identifier for **the schema itself** and is used for resolving references within the schema. It does not need to be a resolvable URL for the validation to work if the references are resolved locally.

    If it is still not clear, think of ``$id`` as a license plate for your car and Biovalidator as a traffic police officer. If the officer has your car in front of them, they have all the information they need to identify your car's make and model. But if the license plate is all the officer has, then they would need to look it up in a database to find out what kind of car it is. In the same way, if Biovalidator has the schema file in front of it, it can validate data against it without needing to resolve the `$id` URL.

4. The `$id` of the schema would need to be resolvable if Biovalidator needs to fetch something through the network. For example: (1) if the schema had ``$ref`` references to other schemas using relative paths that depend on the `$id` for resolution; or (2) if the IDed schema is being referenced through a ``$ref`` that is an absolute URL.

</details>

## Concept summary
A JSON Schema format or pattern determines which values a field accepts. Similar-looking identifiers can be valid in one field and invalid in another: it all depends on the references that are used.

JSON Schema `$id` identifies the schema and supports reference resolution; JSON-LD `@id` identifies a data item. 

A schema can validate locally without its `$id` being a resolvable URL. The schema `$id` must be resolvable when validation needs to fetch the schema or resolve references through the network.

