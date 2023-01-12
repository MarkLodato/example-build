# Example GitHub Actions contexts

This directory contains example dumps of GitHub Actions
[contexts](https://docs.github.com/en/actions/learn-github-actions/contexts).
The purpose is to understand precisely what the inputs to a GitHub Actions
workflow are, for the purposes of generating
[SLSA Provenance](https://slsa.dev/provenance).

## Description

In this example, there are two levels of workflows:

-   The [top-level workflow](../../.github/workflows/dump.yaml) from this repo:
    -   Has two optional input parameters (`inputs`):
        -   `toplevelInput` (unique)
        -   `shadowedInput` (same name as reusable workflow's)
    -   Has two repo-level variables ([setting](https://github.com/MarkLodato/example-build/settings/variables/actions), [screenshot](top_level_vars.png), [docs](https://docs.github.com/en/actions/learn-github-actions/variables)):
        -   `TOPLEVEL_VAR` (unique)
        -   `SHADOWED_VAR` (same name as reusable workflow repo's)
    -   Dumps all contexts as a JSON object.
    -   Calls the reusable workflow below setting both of its inputs.
-   The [reusable workflow](https://github.com/MarkLodato/example-reusable-workflow/blob/main/.github/workflows/dump.yaml):
    -   Has two optional input paramters (`inputs`):
        -   `resuableInput` (unique)
        -   `shadowedInput` (same name as top-level workflow's)
    -   Has two repo-level [variables](https://docs.github.com/en/actions/learn-github-actions/variables):
        -   `REUSABLE_VAR` (unique)
        -   `SHADOWED_VAR` (same name as reusable workflow repo's)
    -   Dumps all contexts as a JSON object.

## Instructions to reproduce

-   Go to https://github.com/MarkLodato/example-build/actions/workflows/dump.yaml
-   Execute the workflow ([screenshot](run.png)):
    -   Click **Run workflow**
    -   Set values for the two fields
    -   Click **Run workflow**
-   When it's finished go to the workflow, then copy the output of the two
    `dump-contexts` outputs.

## Example output

-   [top_level_context.json](top_level_context.json)
-   [reusable_context.json](reusable_context.json)

## Noteworthy properties

-   The reusable workflow's `inputs` context is a **combination** of the top-level
    inputs plus the reusable workflow inputs. In the case where both have the
    same name (`shadowedInput`), the reusable workflow's value is used.
-   The resuable workflow's `vars` context is the **same as the top-level's**
    `vars` context. In other words, the repository variables come from the
    top-level repo, not the reusable workflow's repo.
