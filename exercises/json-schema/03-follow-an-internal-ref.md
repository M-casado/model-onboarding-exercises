# Exercise 3 - Follow an internal `$ref`

## Goal

You will reuse one identifier rule with an internal `$ref`.

## Prerequisites

Start Biovalidator from the [workshop setup](../../README.md#setup) and open <http://localhost:3020>.

## Instructions

1. Paste these rules into Biovalidator:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "@id": { "$ref": "#/$defs/cohortIdentifier" }
  },
  "required": ["@id"],
  "additionalProperties": false,
  "$defs": {
    "cohortIdentifier": {
      "type": "string",
      "pattern": "^ega:EGAH[0-9]{11}$"
    }
  }
}
```

2. Validate both documents:

```json
{
  "@id": "ega:EGAH00001000001"
}
```

```json
{
  "@id": "ega:EGAD00001000001"
}
```

## Questions

1. Which property uses the reusable rule?
2. Where does the rule say that `EGAH` is allowed but `EGAD` is not?
3. What does the `#` at the start of `$ref` tell Biovalidator?

> **In the real repository:** see the [Cohort identifier definition](https://github.com/EGA-archive/fega-metadata-schema/blob/ad5ba2a7ebc2b42c6f4a5cf54aa697e6e8a1a713/schemas/common/schema.json#L4757-L4787). The exercise keeps the definition inline so it can be pasted as one document. Continue with [Exercise 4](04-resolve-a-relative-ref.md) for a reference to another file.

<details>
<summary>Solution</summary>

1. `@id` has `"$ref": "#/$defs/cohortIdentifier"`, so it uses (i.e., it inherits) the `cohortIdentifier` rule that is defined within `$defs`.
2. The `pattern` in that rule requires `ega:EGAH` followed by 11 digits.
3. `#` means "look inside this same schema". `/$defs/cohortIdentifier` is the path to the rule in that schema, so essentially we are referencing a rule that is defined in the same file somewhere else.

</details>

## Concept summary

You can use `$ref` to reuse a rule instead of copying it. When its value starts with only `#`, the rule is in the current schema, so Biovalidator does not need to fetch another file to know what rule is being referenced. The path after `#` is a JSON pointer to the rule, so you can reference rules that are nested in `$defs` or other objects.
