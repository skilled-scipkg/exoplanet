# exoplanet source map: API and Scripting

Generated from source roots:
- `src`
- `tests`

Use this map only after exhausting the topic docs in `skills/exoplanet-api-and-scripting/references/doc_map.md`.

## Topic query tokens
- `light_delay`
- `get_light_curve`
- `secondary_eclipse`
- `unit_disk`
- `quad_limb_dark`
- `angle`
- `get_radial_velocity`
- `citations`
- `docs_setup`
- `ttv`

## Fast source navigation
- `rg -n "_get_retarded_position|get_planet_position|get_radial_velocity|in_transit" src/exoplanet/orbits/keplerian.py`
- `rg -n "get_light_curve|use_in_transit|light_delay" src/exoplanet/light_curves/limb_dark.py src/exoplanet/light_curves/secondary_eclipse.py`
- `rg -n "angle|unit_disk|quad_limb_dark" src/exoplanet/distributions/distributions.py`
- `rg -n "add_citations_to_model|get_citations_for_model" src/exoplanet/citations.py`
- `python -m pytest -q tests/orbits/keplerian_test.py -k "light_delay or radial_velocity"`
- `python -m pytest -q tests/light_curves_test.py -k "in_transit or variable_texp or secondary_eclipse"`
- `python -m pytest -q tests/citations_test.py`
- If a tutorial snippet fails, search the exact method name and inspect call signatures first.

## Suggested source entry points
- `src/exoplanet/orbits/keplerian.py` | score: 10 | symbols: `get_planet_position`, `_get_retarded_position`, `get_radial_velocity`, `in_transit` | behavior checks: `tests/orbits/keplerian_test.py::test_light_delay`, `tests/orbits/keplerian_test.py::test_radial_velocity`
- `src/exoplanet/light_curves/limb_dark.py` | score: 10 | symbols: `LimbDarkLightCurve.get_light_curve`, `LimbDarkLightCurve.get_ror_from_approx_transit_depth` | behavior checks: `tests/light_curves_test.py::test_in_transit`, `tests/light_curves_test.py::test_variable_texp`
- `src/exoplanet/light_curves/secondary_eclipse.py` | score: 8 | symbols: `SecondaryEclipseLightCurve.get_light_curve` | behavior checks: `tests/light_curves_test.py::test_secondary_eclipse`
- `src/exoplanet/distributions/distributions.py` | score: 9 | symbols: `angle`, `unit_disk`, `quad_limb_dark` | behavior checks: `tests/distributions_test.py::TestUnitDisk`, `tests/distributions_test.py::TestAngle`
- `src/exoplanet/orbits/ttv.py` | score: 7 | symbols: `compute_expected_transit_times`, `TTVOrbit._warp_times` | behavior checks: `tests/orbits/ttv_test.py::test_compute_expected_transit_times`
- `src/exoplanet/citations.py` | score: 8 | symbols: `add_citations_to_model`, `get_citations_for_model` | behavior checks: `tests/citations_test.py::test_basic`
- `tests/orbits/keplerian_test.py` | score: 8 | target behavior tests for light-delay and RV conventions
- `tests/light_curves_test.py` | score: 8 | target behavior tests for transit/eclipses and exposure handling
- `tests/citations_test.py` | score: 7 | target behavior tests for citation extraction
- `src/exoplanet/__init__.py` | fallback entry point
