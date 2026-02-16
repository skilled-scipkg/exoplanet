---
name: exoplanet-index
description: Use this router skill to select the correct exoplanet topic skill first, then escalate to source inspection only when docs are insufficient.
---

# exoplanet Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer docs-first answers and keep responses workflow-oriented.
- Escalate to source only when the routed skill docs and doc map are insufficient.
- For immediate execution from this folder, start with `skills/START_HERE.md`.

## Generated topic skills
- `exoplanet-getting-started`: first runnable models, starter parameterizations, and baseline diagnostics.
- `exoplanet-build-and-install`: dependency setup, backend compatibility, editable installs, and test validation.
- `exoplanet-api-and-scripting`: API usage patterns, light-delay behavior, scripting helpers, and citation automation.
- `exoplanet-advanced-topics`: consolidated one-doc advanced areas (API inventory, multiprocessing, developer workflow, changelog, package overview).

## Quick routing hints
- "My model does not converge / how do I start fitting RV or transits?" -> `exoplanet-getting-started`
- "Install/import errors or backend mismatch" -> `exoplanet-build-and-install`
- "How does `light_delay`/`get_light_curve`/`unit_disk` work in code?" -> `exoplanet-api-and-scripting`
- "Broken pipe, contributor process, changelog/version behavior" -> `exoplanet-advanced-topics`

## Documentation-first inputs
- `docs`

## Tutorials and examples roots
- `docs/tutorials`

## Test roots for behavior checks
- `tests`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, open that topic skill's doc map (for example: `skills/exoplanet-getting-started/references/doc_map.md`).
- If documentation still leaves ambiguity, open that topic skill's source map (for example: `skills/exoplanet-getting-started/references/source_map.md`) and inspect suggested source entry points.
- Use targeted symbol search while inspecting source (for example: `rg -n "<symbol_or_keyword>" src tests`).

## Source directories for deeper inspection
- `src`
