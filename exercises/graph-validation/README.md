# Graph validation

These exercises use a simple analogy: a graph is a **box**. You can put different
types of named EGA entities in the box, and the `@graph` array is the box's
contents.

The bare graph schema checks that **all entities** in the box are individually
valid against the rules selected by each entity's `@type`. A profile is a
modular set of extra constraints that you can pass the same box through when
you need to check a particular submission pattern.

| Exercise | Topic |
| --- | --- |
| [1](01-put-entities-in-a-graph-box.md) | See how one graph can hold different entity types |
| [2](02-see-what-the-bare-graph-schema-checks.md) | Validate every entity with `graph/schema.json` |
| [3](03-apply-a-graph-profile.md) | Apply modular constraints to the whole box |

Prerequisite: [JSON Schema 4](../json-schema/04-resolve-a-relative-ref.md),
because graph schemas use the same online and relative file references. You
also need Biovalidator running and internet access so it can fetch the example
schemas.
