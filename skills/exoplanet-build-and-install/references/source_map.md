# exoplanet source map: Build and Install

Generated from source roots:
- `src`
- `tests`
- `.` (packaging and automation files)

Use this map only after exhausting the topic docs in `skills/exoplanet-build-and-install/references/doc_map.md`.

## Topic query tokens
- `install`
- `extras`
- `pymc`
- `pymc3`
- `compat`
- `citation`
- `docs_setup`
- `backend`
- `importerror`
- `pytest`

## Fast source navigation
- `rg -n "EXTRA_REQUIRE|python_requires|pymc3|pymc" setup.py`
- `rg -n "USING_PYMC3|ImportError|EXOPLANET_FORCE_PYMC3" src/exoplanet/compat.py`
- `rg -n "get_citations_for_model|add_citations_to_model" src/exoplanet/citations.py`
- `rg -n "test_pymc|test_pymc3" noxfile.py`
- `python -m pytest -q tests/citations_test.py`
- `python -m pytest -q tests/estimators_test.py`
- For backend import failures, inspect `src/exoplanet/compat.py` first, then confirm extras in `setup.py`.

## Suggested source entry points
- `setup.py` | score: 10 | symbols: `EXTRA_REQUIRE`, `python_requires` | behavior checks: `rg -n "EXTRA_REQUIRE|python_requires" setup.py`
- `pyproject.toml` | score: 8 | symbols: build-system requirements, setuptools-scm config
- `src/exoplanet/compat.py` | score: 10 | symbols: `USING_PYMC3` branch logic and fallback `ImportError` | behavior check: `python -c "import exoplanet.compat as c; print(c.USING_PYMC3)"`
- `src/exoplanet/citations.py` | score: 8 | symbols: `get_citations_for_model` | behavior check: `tests/citations_test.py::test_basic`
- `noxfile.py` | score: 8 | symbols: `test_pymc`, `test_pymc3` session definitions
- `pytest.ini` | score: 7 | symbols: `testpaths`, `filterwarnings`
- `tests/citations_test.py` | score: 8 | target behavior tests for citation registry wiring
- `tests/estimators_test.py` | score: 7 | fast scientific smoke tests after environment setup
