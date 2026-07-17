# EGA v2 schema mini-workshop

This short workshop introduces simplified EGA v2 entity schemas, JSON Schema validation, identifiers, JSON-LD, RDF, and framing. It is designed for you to do on your own, and it takes around 30 minutes.

> To run the exercises you will need a Biovalidator server. See how to set it up [**here**](https://github.com/M-casado/fega-metadata-schema#setup).

You don't need to run Biovalidator with local schemas. Just run the instance from M-casado's fork. Something like the following:
```bash
node "$(npm root -g)/biovalidator/src/biovalidator.js"
# or, if you are in the Biovalidator repository
node src/biovalidator
```

## Tools

- Biovalidator: [http://localhost:3020](http://localhost:3020)
- JSON-LD Playground: <https://json-ld.org/playground/>
- Real EGA v2 schema repository: <https://github.com/M-casado/fega-metadata-schema>

An **entity** is the smallest unit represented independently, such as a _Cohort_. A **JSON Schema** describes which JSON values are allowed. A JSON-LD **context** gives JSON names shared meanings (mainly for machines to understand). A JSON-LD **frame** selects and arranges data from a graph.

The small schemas used in the exercises are simplified versions of the real schemas. Remember that the EGA v2 model is still under development.

## Exercises

| Exercise | Topic |
| --- | --- |
| [1](exercises/01-validate-a-minimal-entity.md) | Validate a minimal entity |
| [2](exercises/02-break-and-repair-data.md) | Break and repair data |
| [3](exercises/03-follow-a-ref.md) | Follow a `$ref` |
| [4](exercises/04-test-identifiers.md) | Test identifiers |
| [5](exercises/05-add-json-ld-meaning.md) | Add JSON-LD meaning |
| [6](exercises/06-expand-json-ld.md) | Expand JSON-LD |
| [7](exercises/07-frame-json-ld.md) | Frame JSON-LD |
| [8](exercises/08-load-a-real-cohort-example.md) | Load a real Cohort example |

If you are running tight on time, prioritise Exercises 1-6. It is fine not to finish every exercise.

In each exercise you have the solution at the bottom, but don't be cheeky: try to do it yourself first.

Exercise 8 needs network access because Biovalidator fetches the current example and schema from GitHub.
