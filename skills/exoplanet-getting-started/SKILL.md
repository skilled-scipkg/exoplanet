---
name: exoplanet-getting-started
description: Use this skill for first runnable PyMC/exoplanet models, starter parameterizations, and basic sampling diagnostics before moving to deeper API or internals work.
---

# exoplanet: Getting Started

## High-Signal Playbook

### Route conditions
- Use this skill when the user needs a first runnable model, a starter parameterization, or quick interpretation of chain diagnostics.
- Route to `exoplanet-build-and-install` for environment creation, dependency conflicts, or editable installs.
- Route to `exoplanet-api-and-scripting` for behavior details of light-delay modeling, helper distributions, or citation automation.
- Route to `exoplanet-advanced-topics` for multiprocessing failures, contribution workflow, changelog/regression checks, or deep API inventory.
- Primary docs: `docs/tutorials/intro-to-pymc.md`, `docs/tutorials/data-and-models.md`, `docs/tutorials/reparameterization.md`.

### Quick simulation start
1. Verify imports and backend:
```bash
python -c "import exoplanet, pymc; print(exoplanet.__version__)"
```
2. Run a minimal transit fit with explicit inputs:
```bash
python - <<'PY'
import numpy as np
import arviz as az
import pymc as pm
import pytensor.tensor as pt
import exoplanet as xo

t = np.arange(0.0, 20.0, 0.02)
with pm.Model():
    t0 = pm.Normal("t0", mu=5.0, sigma=0.5)
    period = pm.Normal("period", mu=5.0, sigma=0.2)
    u = xo.distributions.quad_limb_dark("u", initval=np.array([0.3, 0.2]))
    log_r = pm.Normal("log_r", mu=np.log(0.04), sigma=1.0)
    r = pm.Deterministic("r", pt.exp(log_r))
    b = xo.distributions.impact_parameter("b", r, initval=0.3)
    orbit = xo.orbits.KeplerianOrbit(period=period, t0=t0, b=b)
    lc = xo.LimbDarkLightCurve(u[0], u[1]).get_light_curve(orbit=orbit, r=r, t=t)[:, 0]
    pm.Normal("obs", mu=lc, sigma=5e-4, observed=np.zeros_like(t))
    idata = pm.sample(draws=500, tune=500, chains=2, cores=2, init="adapt_full", target_accept=0.9, progressbar=False)
print(az.summary(idata, var_names=["period", "t0", "r"])[["ess_bulk", "r_hat"]])
PY
```

### Validation checkpoints
- `az.summary` shows finite values and `r_hat < 1.01` for `period`, `t0`, and `r`.
- Quick behavior checks:
```bash
python -m pytest -q tests/orbits/keplerian_test.py -k "radial_velocity or in_transit or get_consistent_inputs"
python -m pytest -q tests/light_curves_test.py -k "in_transit or approx_transit_depth"
python -m pytest -q tests/distributions_test.py -k "TestUnitDisk or TestAngle or TestPhysical"
```

### Common failure modes
- Use `pm.math`/`pytensor` ops in-model; avoid `numpy` transforms on symbolic variables.
- Do not set both `t0` and `t_periastron`, or both `incl` and `b` (`src/exoplanet/orbits/keplerian.py`).
- Avoid defining all three of `m_star`, `r_star`, and `rho_star`; provide any two.
- `docs/tutorials/intro-to-pymc3.md` is a redirect page; use `docs/tutorials/intro-to-pymc.md`.

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses practical and workflow-oriented before escalating to deeper internals.

## Primary documentation references
- `docs/tutorials/intro-to-pymc.md`
- `docs/tutorials/data-and-models.md`
- `docs/tutorials/reparameterization.md`
- `docs/tutorials/intro-to-pymc3.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `skills/exoplanet-getting-started/references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `skills/exoplanet-getting-started/references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs/tutorials`

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/exoplanet/orbits/keplerian.py` (`KeplerianOrbit.__init__`, `get_relative_position`, `get_radial_velocity`, `in_transit`, `_get_consistent_inputs`)
- `src/exoplanet/distributions/distributions.py` (`angle`, `unit_disk`, `quad_limb_dark`, `impact_parameter`)
- `src/exoplanet/light_curves/limb_dark.py` (`get_light_curve`, `get_ror_from_approx_transit_depth`)
- `tests/orbits/keplerian_test.py` (`test_radial_velocity`, `test_in_transit`, `test_get_consistent_inputs`)
- `tests/light_curves_test.py` (`test_in_transit`, `test_approx_transit_depth`)
- `tests/distributions_test.py` (`TestUnitDisk`, `TestAngle`, `TestPhysical`)
