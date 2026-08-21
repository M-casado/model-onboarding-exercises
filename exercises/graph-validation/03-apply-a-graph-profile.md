# Exercise 3 - Pass the graph box through a profile

## Goal

See a profile as a **small, modular set of extra constraints** for the whole _box_ (i.e., the `@graph` array). You can apply any profile to a graph at any point; the profile does not replace the individual entity schemas.

In an EGA workflow, someone can add entities to a box and validate each one with its individual schema while building it. In practice, this tool would be used most times by EGA to validate the relevant EGA profile when a submitter marks the submission as complete.

## Prerequisites

Complete [Exercise 2](02-see-what-the-bare-graph-schema-checks.md). Leave Biovalidator running.

## Instructions

1. Open the [valid Organism Lab Data graph example](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/graph/examples/valid/graph-valid-organism-lab-data.json).
2. Copy the [example's ``schema`` content](https://github.com/EGA-archive/fega-metadata-schema/blob/4d8909ec67e8a1435aee13de93ac7b9a14d53cb1/schemas/graph/examples/valid/graph-valid-organism-lab-data.json#L2-L4) into the **SCHEMA** input field of Biovalidator:
   ```
   {
      "$ref": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/graph/profiles/organism-lab-data.schema.json"
   }
   ```

   Now copy the [example's whole `data` content](https://github.com/EGA-archive/fega-metadata-schema/blob/4d8909ec67e8a1435aee13de93ac7b9a14d53cb1/schemas/graph/examples/valid/graph-valid-organism-lab-data.json#L5-L95) (_not just the snippet below!_) into the **DATA** input field:

   ```
   {
      "@context": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/graph/context.jsonld",
      "@id": "ega:EGAG00000000004",
      "@type": "ega:graph",
      "@graph": [
         {
         "@id": "ega:EGAN00000000004",

      ...
   }
   ```

3. Choose **Validate**. The complete four-entity graph should pass.
4. Open the [profile schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/graph/profiles/organism-lab-data.schema.json) that we are referencing above and find its `allOf` block. Notice how it is combining the bare graph schema with some other reusable requirements (e.g., `../schema.json#/$defs/hasOrganismBiomaterial` requires at least one biomaterial in the graph):

   ```json
   "allOf": [
     { "$ref": "../schema.json" },
     { "$ref": "../schema.json#/$defs/hasOrganismBiomaterial" },
     ...
   ]
   ```

5. In **DATA**, find the biomaterial's node. The one that starts like this:

   ```text
    {
      "@id": "ega:EGAN00000000004",
      "@type": [
        "ega:biomaterial",
   ...
   ```

   And ends like this:

   ```text
   ...
      "inSubmission": {
        "@id": "ega:EGAB00000000004",
        "@type": "ega:submission"
      }
    },
   ```
   Delete that item from the `@graph` array, so that the box no longer has a biomaterial.
6. Choose **Validate**. The validation should fail because the profile requirements are not met by the data.
7. For comparison, in **SCHEMA** replace only the `$ref` value with the bare graph schema URL below. Leave the changed **DATA** unchanged:

   ```json
   {
     "$ref": "https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/graph/schema.json"
   }
   ```

   Choose **Validate** again. The bare graph schema should pass. Why?

## Questions

1. Why can the modified DATA (without the biomaterial node) pass validation of the [bare graph schema](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/graph/schema.json) but fail the schema that was pointing to the [profile](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/graph/profiles/organism-lab-data.schema.json)?
2. When is it useful to apply a profile? Can you apply one before a graph bundle is marked complete?
3. How does `allOf` keep profile rules modular? How is this useful for the EGA and other stakeholders?

<details>
<summary>Solution</summary>

1. The bare schema checks the items in the `@graph` array as individual entities. Additionally to that minimum promise, the profile also requires a node in the graph whose type is a biomaterial.
2. A profile can be applied whenever a check is useful. At any point in time, one can validate the bundle of items in the graph with any profile. That can be at the beginning of a submission, half-way through, or at the end. Most commonly, these profiles would be used at the end of a metadata submission to assert that all the items in a submission, both individually and as a group, are complete and meets the requirements of a particular workflow.
3. `allOf` composes the reusable base graph rules and `has...` requirements. This way, the profile adds constraints without copying the entity definitions. This is extremely useful for EGA to easily make profiles, and for other stakeholders (e.g., an EGA submitter with particular submission requirements) to either reuse similar profiles or to build their own.

</details>

## Concept summary

A profile is a _filter_ you can pass the graph _box_ through when you need to ask, "is this box compatible with these particular requirements?"

You can keep adding and individually validating entities first, then apply the profile when you want the whole-box answer.

```mermaid
---
config:
  theme: neutral
  look: neo
  layout: dagre
  flowchart:
    defaultRenderer: elk
---
flowchart LR
    %% FEGA graph "box" analogy.
    %% Entity colours/shapes follow Figure 5 of the FEGA Metadata Technical Report.

    subgraph BASE["📦 BASE GRAPH BOX"]
        direction LR
        B0["@type: ega:graph"]
        B1["Minimum promise:<br/>each item is a supported EGA entity and is valid against its own schema"]

        subgraph ITEMS1["Contents can be any grouping"]
            direction LR
            D1["<b>Dataset</b><br/>✓ individually valid"]
            F1["<b>Datafile</b><br/>✓ individually valid"]
            P1["<b>Protocol</b><br/>✓ individually valid"]
            M1["<b>Biomaterial</b><br/>✓ individually valid"]
        end

        B0 --> B1
    end

    TAG["🏷️ Add profile<br/><b>Dataset + Datafile profile</b>"]

    subgraph PROFILED["📦 SAME GRAPH BOX + PROFILE"]
        direction TB
        P0["Base rule still applies:<br/>every entity must be individually valid"]
        P1R["Profile adds group-level requirements:<br/><b>≥ 1 Dataset AND ≥ 1 Datafile</b>"]

        subgraph ITEMS2["Current grouping"]
            direction LR
            D2["<b>Dataset</b><br/>✓ entity-valid"]
            F2["<b>Datafile</b><br/>✓ entity-valid"]
            P2["<b>Protocol</b><br/>✓ individually valid"]
            M2["<b>Biomaterial</b><br/>✓ entity-valid"]
        end

        OK["✓ Group satisfies this profile"]
        P0 --> P1R --> ITEMS2 --> OK
    end

    BASE -->|"same grouping"| TAG -->|"validate through profile"| PROFILED

    NOTE2["Profiles are reusable lenses over a grouping:<br/>apply a profile (or set of profiles) when you want additional constraints across the box's contents."]
    PROFILED -.-> NOTE2

    %% Figure 5 entity shapes
    D1@{ shape: diam }
    D2@{ shape: diam }

    F1@{ shape: doc }
    F2@{ shape: doc }

    P1@{ shape: rect }
    P2@{ shape: rect }

    M1@{ shape: dbl-circ }
    M2@{ shape: dbl-circ }

    %% Figure 5 entity colour classes
    D1:::dataManagement
    D2:::dataManagement

    F1:::datafile
    F2:::datafile

    P1:::protocol
    P2:::protocol

    M1:::biomaterial
    M2:::biomaterial

    classDef biomaterial fill:#B3D9FF,stroke:#4C8BF5,stroke-width:1px
    classDef datafile fill:#D5E8D4,stroke:#6FB96C,stroke-width:1px
    classDef protocol fill:#FFE5CC,stroke:#F5A45D,stroke-width:2px,stroke-dasharray:0
    classDef dataManagement fill:#FFD600,stroke:#000000,color:#000000

    %% Diagram-specific styling, deliberately separate from entity semantics
    classDef graphBox fill:#F8FAFC,stroke:#64748B,stroke-width:2px,color:#0F172A
    classDef explanation fill:#FFFFFF,stroke:#94A3B8,stroke-width:1px,color:#334155
    classDef profileTag fill:#EDE9FE,stroke:#7C3AED,stroke-width:2px,color:#4C1D95
    classDef profileRule fill:#F5F3FF,stroke:#8B5CF6,stroke-width:2px,color:#4C1D95
    classDef success fill:#ECFDF5,stroke:#059669,stroke-width:2px,color:#064E3B
    classDef note fill:#FFFFFF,stroke:#94A3B8,stroke-width:1px,stroke-dasharray:4 3,color:#475569

    B0:::graphBox
    B1:::explanation
    TAG:::profileTag
    P0:::explanation
    P1R:::profileRule
    OK:::success
    NOTE2:::note

    style BASE fill:#F8FAFC,stroke:#64748B,stroke-width:2px
    style ITEMS1 fill:#FFFFFF,stroke:#CBD5E1,stroke-width:1px,stroke-dasharray:4 3
    style PROFILED fill:#FAF5FF,stroke:#7C3AED,stroke-width:3px
    style ITEMS2 fill:#FFFFFF,stroke:#C4B5FD,stroke-width:1px,stroke-dasharray:4 3
```
