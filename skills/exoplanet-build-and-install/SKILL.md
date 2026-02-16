---
name: exoplanet-build-and-install
description: Use this skill for installation, editable/development setup, backend compatibility checks, and test validation of exoplanet environments.
---

# exoplanet: Build and Install

## High-Signal Playbook

### Route conditions
- Use this skill when the request is about installation method, dependency extras, source installs, or environment validation.
- Route to `exoplanet-getting-started` after environment setup to build the first model.
- Route to `exoplanet-api-and-scripting` when install succeeds but model behavior is unclear.
- Route to `exoplanet-advanced-topics` for multiprocessing tuning and contributor workflow details.
- Primary docs: `docs/user/install.rst`, `docs/user/multiprocessing.rst`, `docs/tutorials/citation.md`, `docs/tutorials/autodiff.md`.

### Quick setup workflow
1. Install runtime and optional extras:
```bash
python -m pip install -U "exoplanet[pymc]"
python -m pip install -U "exoplanet[extras]"
```
2. For local development and tests:
```bash
python -m pip install -e ".[test]"
python -m pytest -v tests
```
3. Smoke-test backend and citation wiring:
```bash
python - <<'PY'
import exoplanet as xo
from exoplanet.compat import USING_PYMC3, pm
print("USING_PYMC3", USING_PYMC3)
with pm.Model():
    u = xo.distributions.quad_limb_dark("u")
    orbit = xo.orbits.KeplerianOrbit(period=10.0, t0=0.0)
    xo.LimbDarkLightCurve(u[0], u[1]).get_light_curve(r=0.1, orbit=orbit, t=[0.0, 0.1])
    txt, bib = xo.citations.get_citations_for_model()
print(bool(txt), bool(bib))
PY
```

### Validation checkpoints
- `USING_PYMC3` matches the intended backend path.
- Citation smoke test returns `True True` once an exoplanet object is added to the model.
- Fast package checks:
```bash
python -m pytest -q tests/citations_test.py
python -m pytest -q tests/estimators_test.py
python -m pytest -q tests/orbits/simple_test.py
```

### Common failure modes
- Docs require Python 3.8+ (`docs/user/install.rst`); `setup.py` metadata is broader, so follow docs for support policy.
- Installing plain `exoplanet` can miss intended backend extras; use `exoplanet[pymc]` or `exoplanet[pymc3]`.
- Missing `.[test]` dependencies causes avoidable pytest failures.
- Apparent install failures can actually be multiprocessing startup issues; test `cores=1` before deeper debug.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Focus on reproducible, testable environment outcomes.

## Primary documentation references
- `docs/tutorials/autodiff.md`
- `docs/user/install.rst`
- `docs/tutorials/citation.md`
- `docs/user/multiprocessing.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `skills/exoplanet-build-and-install/references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `skills/exoplanet-build-and-install/references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs/tutorials`

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `setup.py` (`EXTRA_REQUIRE`, `python_requires`, package extras for `pymc`/`pymc3`/`test`)
- `pyproject.toml` (build backend and setuptools-scm configuration)
- `src/exoplanet/compat.py` (runtime backend selection and import fallback path)
- `src/exoplanet/citations.py` (`get_citations_for_model`, model citation registration)
- `noxfile.py` (`test_pymc`, `test_pymc3` automation sessions)
- `tests/citations_test.py` (`test_basic`)
- `tests/estimators_test.py` (fast scientific smoke checks for estimator helpers)
