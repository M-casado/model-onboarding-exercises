# Exercise 5 - Validate an ontology term with OLS

## Goal

You will use Biovalidator's custom `graphRestriction` rule to check an ontology term against the real hierarchy in OLS4 (the Ontology Lookup Service).

## Prerequisites

- Start Biovalidator using the [setup instructions](../../README.md#setup).
- Ensure the server can reach OLS4.

## Instructions

1. Paste these rules into the Biovalidator page:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$async": true,
  "type": "object",
  "required": ["term"],
  "properties": {
    "term": {
      "type": "string",
      "graphRestriction": {
        "ontologies": ["obo:efo"],
        "classes": ["PATO:0001894"],
        "includeSelf": false
      }
    }
  }
}
```

2. Replace the **DATA** input with each of these values, one at a time, and choose **Validate** after each replacement:

   Term [``PATO:0000383``](http://purl.obolibrary.org/obo/PATO_0000383) corresponds to [``female``](https://www.ebi.ac.uk/ols4/ontologies/efo/classes/http%253A%252F%252Fpurl.obolibrary.org%252Fobo%252FPATO_0000383) in EFO's ontology.
   ```json
   {"term": "PATO:0000383"}
   ```
   Term [``MONDO:0005148``](http://purl.obolibrary.org/obo/MONDO_0005148) corresponds to [``type 2 diabetes mellitus``](https://www.ebi.ac.uk/ols4/ontologies/efo/classes/http%253A%252F%252Fpurl.obolibrary.org%252Fobo%252FMONDO_0005148?lang=en) in EFO's ontology.
   ```json
   {"term": "MONDO:0005148"}
   ```

   The first is a child term of ``phenotypic sex`` (``PATO:0001894``), which is the parent that we defined in ``classes`` within the schema. The second term is not a descendant of that parent term, and thus validation fails.

   _Note:_ If OLS is unavailable, record a service failure. Just because the service could not answer does not mean that our term did not belong to the ontology hierarchy.

3. Replace the **SCHEMA** content with the following:
    ```json
    {
      "allOf": [
        {
          "$ref": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/common/schema.json#/$defs/ontologyTerm"
        },
        {
          "properties": {
            "id": {
              "$ref": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/entities/biomaterial/schema.json#/$defs/commonBiomaterialDefs/properties/sex/properties/phenotypicSex/properties/id"
            }
          }
        }
      ]
    }
    ```

4. Replace the **DATA** input with each of these values, one at a time, and choose **Validate** after each replacement:
    ```json
    {
      "id": "PATO:0000383"
    }
    ```

    ```json
    {
      "id": "MONDO:0005148"
    }
    ```

    Notice how the **modularity** of JSON Schemas is highlighted here, where we can choose what to validate (a property within a property, within a definition set...) with great granularity.


## Questions

1. What do `classes`, `ontologies`, and `includeSelf` tell the rule to do?
2. Why is `$async: true` included?
3. Why is checking a hierarchy easier to maintain than a very long list of allowed terms?
4. What outside service does this check need?

> **In the real repository:** compare the [Biomaterial ontology restriction](https://github.com/EGA-archive/fega-metadata-schema/blob/4d8909ec67e8a1435aee13de93ac7b9a14d53cb1/schemas/entities/biomaterial/schema.json#L285-L330) with Biovalidator's [`graphRestriction` documentation](https://github.com/EbiEga/biovalidator/blob/31f66a593f048a1f70631358ac14c4aa77f2cd94/README.md#graphrestriction) and the [OLS4 help/API documentation](https://www.ebi.ac.uk/ols4/help).

<details>
<summary>Solution</summary>

1. `classes` names the parent concept. `ontologies` chooses the ontology. `includeSelf: false` means that the parent itself is not accepted—only a child below it.
2. Biovalidator asks OLS a question while it is checking the data. `$async: true` tells the validator that it may need to wait for that answer.
3. The ontology can gain new child terms without someone copying every term into a long list. The rule stays connected to the shared ontology. And therefore, we do not need to maintain an endless list of terms in controlled vocabularies within our model!
4. The check needs OLS and the current contents of the ontology. If OLS is down, that is a service problem, not proof that the term is wrong.

</details>

## Concept summary

You can think of an ontology as a shared list of concepts and links between them. `graphRestriction` asks OLS whether the term we give as a value is below an allowed parent.

This lets the rules use the shared list instead of listing every child by hand.
