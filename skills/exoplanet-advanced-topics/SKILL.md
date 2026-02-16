---
name: exoplanet-advanced-topics
description: Use this skill for consolidated advanced docs coverage (API inventory, multiprocessing, developer workflow, changelog context, and package-level routing).
---

# exoplanet: Advanced Topics

## High-Signal Playbook

### Route conditions
- Use this skill for requests about API surface inventory, multiprocessing behavior, contribution workflow, version-change context, or top-level package capabilities.
- Route to `exoplanet-getting-started` for first runnable inference models.
- Route to `exoplanet-build-and-install` for dependency/setup failures before runtime tuning.
- Route to `exoplanet-api-and-scripting` when the question is specific API behavior in orbit/light-curve code.
- Primary docs: `docs/user/api.rst`, `docs/user/multiprocessing.rst`, `docs/user/dev.rst`, `docs/changes.rst`, `docs/index.rst`.

### Quick workflow
1. For multiprocessing instability, start with a serial baseline:
```bash
python - <<'PY'
import pymc as pm
with pm.Model():
    pm.Normal("x")
    idata = pm.sample(draws=200, tune=200, chains=2, cores=1, progressbar=False)
print(idata.posterior["x"].shape)
PY
```
2. For API inventory checks, inspect objects directly:
```bash
python - <<'PY'
import exoplanet as xo
print(xo.orbits.KeplerianOrbit)
print(xo.orbits.TTVOrbit)
print(xo.orbits.SimpleTransitOrbit)
print(xo.LimbDarkLightCurve)
PY
```
3. For regressions, run targeted behavior tests before broad changes.

### Validation checkpoints
- Baseline sampling succeeds with `cores=1` before trying `mp_ctx`/`pickle_backend` changes.
- Version/regression triage compares `docs/changes.rst` with current tests:
```bash
python -m pytest -q tests/orbits/ttv_test.py tests/orbits/simple_test.py
python -m pytest -q tests/light_curves_test.py -k "in_transit or contact_bug"
python -m pytest -q tests/estimators_test.py
```
- Contributor changes run `python -m pytest -v tests` before handoff.

### Common failure modes
- Multiprocessing hangs or broken pipes can mimic model bugs; stabilize first with `cores=1`.
- `mp_ctx="forkserver"` can improve stability but may be significantly slower on some platforms.
- `docs/user/api.rst` is inventory-focused; use topic tutorial skills for end-to-end modeling guidance.
- For changelog-related questions, confirm against both `docs/changes.rst` and `HISTORY.rst`.

## Scope
- Handle advanced documentation themes consolidated from single-doc topics.
- Provide routing and quick operational guidance without duplicating full tutorials.

## Primary documentation references
- `docs/user/api.rst`
- `docs/user/multiprocessing.rst`
- `docs/user/dev.rst`
- `docs/index.rst`
- `docs/changes.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `skills/exoplanet-advanced-topics/references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `skills/exoplanet-advanced-topics/references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/exoplanet/orbits/ttv.py` (`compute_expected_transit_times`, `TTVOrbit._warp_times`)
- `src/exoplanet/orbits/simple.py` (`SimpleTransitOrbit.get_relative_position`, `SimpleTransitOrbit.in_transit`)
- `src/exoplanet/orbits/keplerian.py` (`KeplerianOrbit` constraints, velocity and transit APIs)
- `src/exoplanet/estimators.py` (`lomb_scargle_estimator`, `autocorr_estimator`, `bls_estimator`)
- `src/exoplanet/compat.py` (`USING_PYMC3` backend selection branch)
- `tests/orbits/ttv_test.py`, `tests/orbits/simple_test.py`, `tests/estimators_test.py`, `tests/light_curves_test.py`
- `HISTORY.rst` (release history used by `docs/changes.rst`)
