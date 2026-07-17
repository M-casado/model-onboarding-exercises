# Exercise 8 - Load a real Cohort example

## Goal

See how Biovalidator fetches an example and resolves its schema from the EGA v2 GitHub repository.

## Instructions

1. Open [Biovalidator](http://localhost:3020).
2. Select **Fetch examples**. Biovalidator asks GitHub for the current minimal examples in our ``fega-metadata-schema`` repository.
3. Select `cohort: cohort-valid-minimal-study-defined.json`, then select **Load example**.
4. Look at the Schema input. It should contain this small `$ref` object rather than the complete schema.

```json
{
  "$ref": "https://raw.githubusercontent.com/M-casado/fega-metadata-schema/main/schemas/entities/cohort/schema.json"
}
```

5. Look at the Data input. It should contain the Cohort fetched from GitHub.

```json
{
  "@context": "https://raw.githubusercontent.com/M-casado/fega-metadata-schema/main/schemas/entities/cohort/schema.json",
  "@id": "ega:EGAH00000000001",
  "@type": "ega:cohort",
  "id": "ega:EGAH00000000001",
  "name": "Barcelona adult genomics cohort",
  "cohortType": "study-defined"
}
```

6. Select **Validate**. The result should be **VALID**.

## Questions

1. Why does the Schema input contain only a `$ref` instead of the full Cohort schema?
2. What does Biovalidator fetch and compile when you select **Validate**?

> **In the real repository:** the fetched [minimal Cohort wrapper](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/entities/cohort/examples/valid/cohort-valid-minimal-study-defined.json#L1-L13) pairs its data with the [Cohort schema](https://github.com/M-casado/fega-metadata-schema/blob/f59d931f0db9eb4c6cc2e556d00dafcce14281f6/schemas/entities/cohort/schema.json). The UI deliberately uses `main` URLs so that it loads the current development version.

<details>
<summary>Solution</summary>

1. The `$ref` is a pointer to the raw Cohort schema on GitHub. It keeps the request small and avoids copying the schema into the UI.
2. Biovalidator resolves that URL over the network, fetches the Cohort schema and its referenced schemas, compiles them, and validates the loaded data against the result.

</details>
