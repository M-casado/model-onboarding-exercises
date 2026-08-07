# EGA v2 metadata onboarding materials

These materials introduce the EGA v2 metadata model through JSON Schema, Biovalidator, graph bundles, JSON-LD, and a small optional SHACL exercise. The exercises are grouped by topic so you can follow the core route or jump to the concept you need.


## Setup

> [!IMPORTANT]
> To run the exercises you will need a Biovalidator server. See how to set it up [**here**](https://github.com/EGA-archive/fega-metadata-schema/tree/dev#setup).

You don't need to run Biovalidator with local schemas. Just run the instance, something like the following:
```bash
node "$(npm root -g)/biovalidator/src/biovalidator.js"
# or, if you are in the Biovalidator repository
node src/biovalidator
```

## Tools

- Biovalidator: [http://localhost:3020](http://localhost:3020)
- JSON-LD Playground: <https://json-ld.org/playground/>
- Real EGA v2 schema repository: <https://github.com/M-casado/fega-metadata-schema>

## Suggested routes

The core route takes approximately 60–90 minutes, depending on how much time you spend inspecting the real schemas:

1. [JSON Schema](exercises/json-schema/README.md)
2. [Biovalidator](exercises/biovalidator/README.md)
3. [Graph validation](exercises/graph-validation/README.md)
4. [JSON-LD](exercises/json-ld/README.md)

The [optional extensions](exercises/json-schema/README.md#optional-extensions) cover standards reuse and versioned URLs. [SHACL](exercises/shacl/README.md) and [open-source navigation](exercises/open-source/README.md) are also optional.

If you are running tight on time, prioritise the core topics above. It is fine not to finish all exercises.

Every exercise has its **solution** below the questions, followed by a short **concept** explanation. But don't be cheeky: try to do it yourself first.

## Topic index

| Topic | What it covers |
| --- | --- |
| [JSON Schema](exercises/json-schema/README.md) | Types, required properties, `$ref`, `$id`, openness, identifiers, standards, and release URLs |
| [Biovalidator](exercises/biovalidator/README.md) | UI, `/health`, `/validate`, `/cache`, asynchronous validation, and OLS |
| [Graph validation](exercises/graph-validation/README.md) | Validating graph items and applying modular bundle profiles |
| [JSON-LD](exercises/json-ld/README.md) | Contexts, expansion, RDF triples, and framing |
| [SHACL](exercises/shacl/README.md) | Optional RDF/SHACL validation against a HealthDCAT-AP shape set |
| [Open-source navigation](exercises/open-source/README.md) | Finding primary sources and using network-enabled LLMs responsibly |

## Concepts

An **entity** is an independently represented unit such as a Cohort or Biomaterial. A **JSON Schema** describes which JSON values are allowed. A JSON-LD **context** gives JSON names shared meanings. A JSON-LD **frame** selects and arranges data from a graph. A **graph profile** adds requirements to a complete bundle of entities.

Please note that the schema repository is under active development.