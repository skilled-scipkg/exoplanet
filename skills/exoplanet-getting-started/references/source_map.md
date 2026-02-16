# exoplanet source map: Getting Started

Generated from source roots:
- `src`
- `tests`

Use this map only after exhausting the topic docs in `skills/exoplanet-getting-started/references/doc_map.md`.

## Topic query tokens
- `intro`
- `pymc`
- `keplerianorbit`
- `light_curve`
- `unit_disk`
- `quad_limb_dark`
- `impact_parameter`
- `find_map`
- `sample`
- `rhat`
- `ess`

## Fast source navigation
- `rg -n "KeplerianOrbit|get_radial_velocity|in_transit|_get_consistent_inputs" src/exoplanet/orbits/keplerian.py`
- `rg -n "unit_disk|quad_limb_dark|impact_parameter|angle" src/exoplanet/distributions/distributions.py`
- `rg -n "get_light_curve|get_ror_from_approx_transit_depth" src/exoplanet/light_curves/limb_dark.py`
- `python -m pytest -q tests/orbits/keplerian_test.py -k "radial_velocity or in_transit or get_consistent_inputs"`
- `python -m pytest -q tests/light_curves_test.py -k "in_transit or approx_transit_depth"`
- `python -m pytest -q tests/distributions_test.py -k "TestUnitDisk or TestAngle or TestPhysical"`

## Suggested source entry points
- `src/exoplanet/orbits/keplerian.py` | score: 10 | symbols: `KeplerianOrbit.__init__`, `get_relative_position`, `get_radial_velocity`, `in_transit`, `_get_consistent_inputs` | behavior checks: `tests/orbits/keplerian_test.py::test_radial_velocity`, `tests/orbits/keplerian_test.py::test_in_transit`, `tests/orbits/keplerian_test.py::test_get_consistent_inputs`
- `src/exoplanet/distributions/distributions.py` | score: 9 | symbols: `angle`, `unit_disk`, `quad_limb_dark`, `impact_parameter` | behavior checks: `tests/distributions_test.py::TestUnitDisk`, `tests/distributions_test.py::TestAngle`, `tests/distributions_test.py::TestPhysical`
- `src/exoplanet/light_curves/limb_dark.py` | score: 9 | symbols: `LimbDarkLightCurve.get_light_curve`, `LimbDarkLightCurve.get_ror_from_approx_transit_depth` | behavior checks: `tests/light_curves_test.py::test_in_transit`, `tests/light_curves_test.py::test_approx_transit_depth`
- `src/exoplanet/orbits/simple.py` | score: 7 | symbols: `SimpleTransitOrbit.get_relative_position`, `SimpleTransitOrbit.in_transit` | behavior checks: `tests/orbits/simple_test.py::test_simple`, `tests/orbits/simple_test.py::test_simple_light_curve_compare_kepler`
- `src/exoplanet/compat.py` | score: 6 | symbols: `USING_PYMC3` branch selection | behavior check: `python -c "import exoplanet.compat as c; print(c.USING_PYMC3)"`
- `tests/orbits/keplerian_test.py` | score: 8 | target behavior tests for orbit dynamics and constraints
- `tests/light_curves_test.py` | score: 8 | target behavior tests for limb-darkened transit models
- `tests/distributions_test.py` | score: 8 | target behavior tests for prior/reparameterization helpers
- `src/exoplanet/__init__.py` | fallback entry point
