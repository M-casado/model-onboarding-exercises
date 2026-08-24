# EGA v2 metadata onboarding materials

These materials introduce the EGA v2 metadata model one small step at a time. You will use JSON Schema, Biovalidator, graph bundles, JSON-LD, and SHACL.

The exercises are grouped by topic. You can follow the suggested path or go straight to a topic you need.


## Setup

> [!IMPORTANT]
> To run the exercises you will need a Biovalidator server. See how to set it up [**here**](https://github.com/EGA-archive/fega-metadata-schema/tree/main#setup).

You do not need to give Biovalidator a local copy of the schemas. If you installed it globally, copy this command to start the server:
```bash
node "$(npm root -g)/biovalidator/src/biovalidator.js"
```

If you are already inside the Biovalidator repository, use this command instead:

```bash
node src/biovalidator
```

## Tools

- Biovalidator: [http://localhost:3020](http://localhost:3020)
- JSON-LD Playground: <https://json-ld.org/playground/>
- Real EGA v2 schema repository: <https://github.com/EGA-archive/fega-metadata-schema>

## Suggested routes

1. [JSON Schema](exercises/json-schema/)
2. [Biovalidator](exercises/biovalidator/)
3. [Graph validation](exercises/graph-validation/)
4. [JSON-LD](exercises/json-ld/)

[SHACL](exercises/shacl/) and [open-source navigation](exercises/open-source/) are rather optional.

If you are running tight on time, prioritise the core topics above. It is fine not to finish all exercises.

Every exercise has a **solution** below its questions, followed by a short **concept summary**. _Don't be cheeky: try to do it yourself first._

## Topic index

| Topic | What it covers |
| --- | --- |
| [JSON Schema](exercises/json-schema/) | Data types, required fields, reusable rules, identifiers, and versions |
| [Biovalidator](exercises/biovalidator/) | The browser page, health check, validation API, saved work, and ontology terms |
| [Graph validation](exercises/graph-validation/) | Checking graph items and complete bundles |
| [JSON-LD](exercises/json-ld/) | Giving names shared meanings, expanding data, and showing linked data |
| [SHACL](exercises/shacl/) | Optional RDF checks with SHACL rules |
| [Open-source navigation](exercises/open-source/) | Finding and checking source material with an online language model |

## Concepts

As you work through the exercises, keep these ideas in mind:

- An **entity** is one item, such as a _Cohort_ or _Biomaterial_.
- A **JSON Schema** is a list of rules for allowed JSON data.
- A JSON-LD **context** tells your computer what JSON names mean.
- A JSON-LD **frame** picks and arranges data from a graph.
- A **graph profile** adds extra rules for a complete bundle of entities.
- A **URL** is a web address.
- An **API** lets another program ask a service to do something.
- A **cache** is saved work that can be reused.
- An **ontology** is a shared list of concepts and links between them.
- **RDF** is a way to write linked facts. **SHACL** is a set of rules for checking those facts.

Please note that the [schema repository](https://github.com/EGA-archive/fega-metadata-schema) is under active development.
