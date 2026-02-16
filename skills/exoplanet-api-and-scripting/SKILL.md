---
name: exoplanet-api-and-scripting
description: Use this skill for programmatic exoplanet usage patterns (orbit/light-curve APIs, helper distributions, light-delay toggles, and citation automation).
---

# exoplanet: API and Scripting

## High-Signal Playbook

### Route conditions
- Use this skill when the user needs concrete code patterns with `exoplanet` APIs and PyMC model plumbing.
- Route to `exoplanet-getting-started` for first-time model setup and baseline inference workflow.
- Route to `exoplanet-build-and-install` for dependency/setup failures before code execution.
- Route to `exoplanet-advanced-topics` for multiprocessing, contributor workflow, and changelog-level upgrade questions.
- Primary docs: `docs/tutorials/light-delay.md`, `docs/tutorials/reparameterization.md`, `docs/tutorials/citation.md`, `docs/tutorials/about.md`.

### Quick simulation start
1. Compare no-delay and delay transit timing:
```bash
python - <<'PY'
import numpy as np
import exoplanet as xo

orbit = xo.orbits.KeplerianOrbit(
    period=365.25, t0=0.0, incl=0.5*np.pi, ecc=0.0, omega=0.0,
    m_planet=0.0, m_star=1.0, r_star=1.0
)
t = np.linspace(-0.01, 0.01, 9999)
x0, _, _ = orbit.get_planet_position(t, light_delay=False)
x1, _, _ = orbit.get_planet_position(t, light_delay=True)
dt_min = (t[np.argmin(np.abs(x1.eval()))] - t[np.argmin(np.abs(x0.eval()))]) * 24 * 60
print(f"delay_minutes={dt_min:.6f}")
PY
```
2. Verify citation plumbing on a model graph:
```bash
python - <<'PY'
import pymc as pm
import exoplanet as xo

with pm.Model():
    u = xo.distributions.quad_limb_dark("u")
    orbit = xo.orbits.KeplerianOrbit(period=10.0, t0=0.0)
    xo.LimbDarkLightCurve(u[0], u[1]).get_light_curve(r=0.1, orbit=orbit, t=[0.0, 0.1])
    txt, bib = xo.citations.get_citations_for_model()
print(bool(txt), bool(bib))
PY
```

### Validation checkpoints
- Delay and no-delay outputs are both finite and not identically equal near transit.
- Citation text and BibTeX are non-empty once an exoplanet model component is added.
- Targeted behavior checks:
```bash
python -m pytest -q tests/orbits/keplerian_test.py -k "light_delay or radial_velocity"
python -m pytest -q tests/light_curves_test.py -k "in_transit or variable_texp or secondary_eclipse"
python -m pytest -q tests/citations_test.py
```

### Common failure modes
- `KeplerianOrbit.in_transit` does not implement `light_delay=True`; avoid `use_in_transit=True` when forcing delay.
- `SimpleTransitOrbit` does not support light-delay paths.
- `LimbDarkLightCurve` supports quadratic limb darkening only; use `starry` for higher-order profiles.
- For eccentric/angle-heavy posteriors, prefer `angle`/`unit_disk` parameterizations over direct raw-angle priors.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Focus on executable patterns and behavior-level interpretation.

## Primary documentation references
- `docs/tutorials/light-delay.md`
- `docs/tutorials/about.md`
- `docs/tutorials/reparameterization.md`
- `docs/tutorials/citation.md`
- `docs/tutorials/autodiff.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `skills/exoplanet-api-and-scripting/references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `skills/exoplanet-api-and-scripting/references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs/tutorials`

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/exoplanet/orbits/keplerian.py` (`get_planet_position`, `_get_retarded_position`, `get_radial_velocity`, `in_transit`)
- `src/exoplanet/light_curves/limb_dark.py` (`get_light_curve`, `use_in_transit` handling, exposure integration)
- `src/exoplanet/light_curves/secondary_eclipse.py` (`SecondaryEclipseLightCurve.get_light_curve`)
- `src/exoplanet/distributions/distributions.py` (`angle`, `unit_disk`, `quad_limb_dark`)
- `src/exoplanet/citations.py` (`add_citations_to_model`, `get_citations_for_model`)
- `tests/orbits/keplerian_test.py` (`test_light_delay`, `test_radial_velocity`)
- `tests/light_curves_test.py` (`test_variable_texp`, `test_secondary_eclipse`, `test_in_transit`)
- `tests/citations_test.py` (`test_basic`)
