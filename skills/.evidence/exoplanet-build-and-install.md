# Evidence: exoplanet-build-and-install

## Primary docs
- `docs/tutorials/autodiff.md`
- `docs/user/install.rst`
- `docs/tutorials/citation.md`

## Primary source entry points
- `skills/exoplanet-build-and-install/references/doc_map.md`
- `src/exoplanet/citations.py`
- `src/exoplanet/__init__.py`
- `src/exoplanet/orbits/__init__.py`
- `src/exoplanet/light_curves/__init__.py`
- `src/exoplanet/distributions/__init__.py`
- `src/exoplanet/utils.py`
- `src/exoplanet/units.py`
- `src/exoplanet/interp.py`
- `src/exoplanet/estimators.py`
- `src/exoplanet/compat.py`
- `src/exoplanet/orbits/ttv.py`
- `src/exoplanet/orbits/simple.py`
- `src/exoplanet/orbits/keplerian.py`
- `src/exoplanet/orbits/dur_to_ecc.py`
- `src/exoplanet/orbits/constants.py`
- `src/exoplanet/light_curves/secondary_eclipse.py`
- `src/exoplanet/light_curves/limb_dark.py`
- `src/exoplanet/light_curves/interpolated.py`
- `src/exoplanet/distributions/eccentricity.py`

## Extracted headings
- Automatic differentation & gradient-based inference
- Automatic differentiation in PyTensor
- Define the relationship between two variables x and y=f(x)
- Here pytensor will compile a function to evaluate y
- Request the gradient of y with respect to x
- Note the call to `sum`. This is a bit of a cheat since by
- default pytensor only computes gradients of a *scalar* function
- Plot the function and its derivative
- Overplot the symbolic derivative for comparison
- Gradient-based inference
- Citing exoplanet & its dependencies

## Executable command hints
- $$
- python -m pip install -U "exoplanet[pymc]"
- python -m pip install -U "exoplanet[extras]"
- python -m pip install -U "exoplanet[pymc3]"
- python -m pip install -U exoplanet
- python -m pip install -e .
- python -m pip install -e ".[test]"
- python -m pytest -v tests

## Warnings and pitfalls
- There are times when providing your AD framework with a custom implementation and/or differentation rule for a particular function is beneficial in terms of cost and stability.
- logger.setLevel(logging.ERROR)
- In a situation like this, it can be easy to forget about the important infrastructure upon which our science is built.
