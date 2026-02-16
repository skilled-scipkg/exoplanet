# exoplanet source map: Advanced Topics

Generated from source roots:
- `src`
- `tests`
- `.` (for release history and automation files)

Use this map only after exhausting the topic docs in `skills/exoplanet-advanced-topics/references/doc_map.md`.

## Topic query tokens
- `api`
- `developer`
- `multiprocessing`
- `forkserver`
- `orbit`
- `ttv`
- `simpletransitorbit`
- `light_curve`
- `distribution`
- `estimator`
- `citation`
- `compat`

## Fast source navigation
- `rg -n "KeplerianOrbit|TTVOrbit|SimpleTransitOrbit|get_light_curve" src`
- `rg -n "compute_expected_transit_times|_warp_times|in_transit|get_radial_velocity" src/exoplanet/orbits`
- `rg -n "lomb_scargle_estimator|autocorr_estimator|bls_estimator" src/exoplanet/estimators.py`
- `python -m pytest -q tests/orbits/ttv_test.py tests/orbits/simple_test.py`
- `python -m pytest -q tests/estimators_test.py`
- `python -m pytest -q tests/light_curves_test.py -k "in_transit or contact_bug"`
- If docs are terse, search exact API names listed in `docs/user/api.rst` and inspect the defining module/tests.

## Suggested source entry points
- `src/exoplanet/orbits/ttv.py` | score: 10 | symbols: `compute_expected_transit_times`, `TTVOrbit._warp_times` | behavior checks: `tests/orbits/ttv_test.py::test_compute_expected_transit_times`, `tests/orbits/ttv_test.py::test_consistency`
- `src/exoplanet/orbits/simple.py` | score: 9 | symbols: `SimpleTransitOrbit.get_relative_position`, `SimpleTransitOrbit.in_transit` | behavior checks: `tests/orbits/simple_test.py::test_simple`, `tests/orbits/simple_test.py::test_simple_light_curve_compare_kepler`
- `src/exoplanet/orbits/keplerian.py` | score: 9 | symbols: `KeplerianOrbit.get_radial_velocity`, `KeplerianOrbit.in_transit`, `_get_consistent_inputs` | behavior checks: `tests/orbits/keplerian_test.py::test_radial_velocity`, `tests/orbits/keplerian_test.py::test_in_transit`
- `src/exoplanet/estimators.py` | score: 9 | symbols: `estimate_semi_amplitude`, `estimate_minimum_mass`, `lomb_scargle_estimator`, `autocorr_estimator`, `bls_estimator` | behavior checks: `tests/estimators_test.py`
- `src/exoplanet/compat.py` | score: 8 | symbols: backend selection via `USING_PYMC3`
- `src/exoplanet/light_curves/limb_dark.py` | score: 8 | symbols: `LimbDarkLightCurve.get_light_curve` | behavior checks: `tests/light_curves_test.py::test_in_transit`
- `tests/orbits/ttv_test.py` | score: 8 | target behavior tests for TTV modeling
- `tests/orbits/simple_test.py` | score: 8 | target behavior tests for simple transit approximations
- `tests/estimators_test.py` | score: 8 | target behavior tests for estimator stability
- `HISTORY.rst` | score: 7 | release history for changelog/regression triage
- `src/exoplanet/__init__.py` | fallback entry point
