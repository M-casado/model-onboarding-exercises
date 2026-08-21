# Exercise 9 - Choose a schema version

## Goal

You will choose a URL that matches the stability you need: a feature branch for work in progress, `main` for the latest merged snapshot, or an immutable release tag for a repeatable integration.

## Prerequisites

Complete [Exercise 4](04-resolve-a-relative-ref.md) and have a browser with internet access.

## Instructions

1. Open the current [**`main`** Cohort schema](https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/main/schemas/entities/cohort/schema.json). It returns JSON for the latest merged snapshot. The URL is convenient for current work, but its **contents can change** after another merge.
2. Open the repository's [Branches page](https://github.com/EGA-archive/fega-metadata-schema/branches). If you see any other branch other than `main`, then those are feature branches: temporary working copies of `main` where new developments are being tested.
3. Open the [v1.0.0-draft.1 Cohort schema](https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/v1.0.0-draft.1/schemas/entities/cohort/schema.json). This is the existing versioned pre-release URL. Its contents are immutable and tied to the tag (`.../v1.0.0-draft.1/...`) rather than to later changes on `main`.

   In other words, a tagged release URL is a **permanent reference** to a specific snapshot of the schema, while a branch URL is a **moving target** that can change over time.
4. Within the release guide, take a look at the [Git History Example](https://github.com/EGA-archive/fega-metadata-schema/blob/main/docs/releases/README.md#git-history-example) diagram. Can you see how the `main` branch moves forward with each merge? Why is it important that during the release update process we update (e.g., ``.../main/...`` -> ``.../v1.0.0-draft.1/...``) the `$id`, `$ref`, and `@context` URLs inside the schema?

## Questions

1. Why is a feature- or main-branch URL (e.g., `.../main/schemas/entities/cohort/schema.json`) unsuitable as a permanent production dependency?
2. What is the difference between the `main` URL and the `v1.0.0-draft.1` URL?
3. Why is a raw URL needed by Biovalidator instead of a GitHub `blob/...` URL (e.g., [this](https://raw.githubusercontent.com/EGA-archive/fega-metadata-schema/refs/heads/main/schemas/entities/cohort/schema.json) vs [that](https://github.com/EGA-archive/fega-metadata-schema/blob/main/schemas/entities/cohort/schema.json))?
4. Why must internal schema pointers and context URLs be changed when a release is cut?

<details>
<summary>Solution</summary>

1. Both branches are moving targets: they are work in progress and, as such, their rules can change, be rebased, or be deleted. This makes them unsuitable for a permanent dependency, because a future change could break your integration or audit.
2. `main` follows the **latest** merged snapshot and may change as the project evolves. `v1.0.0-draft.1` names **one** unique, immutable, and permanent published snapshot, so it is the reproducible choice for a production dependency.
3. A raw URL returns the JSON document itself. A `blob/...` URL returns a GitHub web page for people, not the schema document a validator must parse.
4. A schema can contain absolute `$id`, `$ref`, and `@context` URLs. If they still point at a moving branch, a supposedly versioned outer URL could pull in moving rules or contexts. Rewriting them makes the whole release self-consistent and stable.

   In other words, if our cohort schema is at `v1.0.0-draft.1`, then all `$id`, `$ref`, and `@context` URLs inside it must also point to `v1.0.0-draft.1` rather than to `main` or a feature branch. Because, as we saw in [exercise 4](./04-resolve-a-relative-ref.md), these references and identifiers are used to resolve and fetch the schema and context, so they must be consistent with the release version. If a `v1.0.0-draft.1` cohort schema pointed to a `main` common schema, then a future change to `main` could break the validation of the released schema without you noticing.

</details>

## Concept summary

- Main branch URLs answer "what is the latest merged snapshot?"
- Feature branch URLs answer "what is being developed now?"
- Release URLs answer "which exact rules did we use at this point in time?"

Use a moving branch only when you want changes; use an immutable tag when repeatability matters.
