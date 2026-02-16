# exoplanet Skills: Start Here

Use this file when you begin inside `skills/` and need a fast path to real simulation work.

## 1) Pick the right topic skill
- First runnable model or diagnostics: `skills/exoplanet-getting-started/SKILL.md`
- Install/build/backend issues: `skills/exoplanet-build-and-install/SKILL.md`
- API behavior, light-delay, citations: `skills/exoplanet-api-and-scripting/SKILL.md`
- Multiprocessing, changelog, contributor workflow: `skills/exoplanet-advanced-topics/SKILL.md`

## 2) Run a preflight check
```bash
python -c "import exoplanet, pymc; print(exoplanet.__version__)"
```

## 3) Run a fast simulation smoke test
```bash
python - <<'PY'
import numpy as np
import exoplanet as xo

orbit = xo.orbits.KeplerianOrbit(period=5.0, t0=0.0, b=0.4, m_star=1.0, r_star=1.0)
t = np.linspace(-0.3, 0.3, 500)
lc = xo.LimbDarkLightCurve(0.3, 0.2).get_light_curve(orbit=orbit, r=0.1, t=t).eval()
print("lc_shape", lc.shape, "finite", np.isfinite(lc).all())
PY
```

## 4) Validate with focused tests
```bash
python -m pytest -q tests/orbits/keplerian_test.py -k "radial_velocity or in_transit"
python -m pytest -q tests/light_curves_test.py -k "in_transit or secondary_eclipse"
python -m pytest -q tests/citations_test.py
```

If any checkpoint fails, route to the corresponding topic skill and then open its map files:
- `skills/exoplanet-getting-started/references/doc_map.md` and `skills/exoplanet-getting-started/references/source_map.md`
- `skills/exoplanet-build-and-install/references/doc_map.md` and `skills/exoplanet-build-and-install/references/source_map.md`
- `skills/exoplanet-api-and-scripting/references/doc_map.md` and `skills/exoplanet-api-and-scripting/references/source_map.md`
- `skills/exoplanet-advanced-topics/references/doc_map.md` and `skills/exoplanet-advanced-topics/references/source_map.md`
