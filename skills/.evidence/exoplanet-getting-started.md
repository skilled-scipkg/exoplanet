# Evidence: exoplanet-getting-started

## Primary docs
- `docs/tutorials/intro-to-pymc.md`
- `docs/tutorials/data-and-models.md`
- `docs/tutorials/intro-to-pymc3.md`

## Primary source entry points
- `skills/exoplanet-getting-started/references/doc_map.md`
- `src/exoplanet/__init__.py`
- `src/exoplanet/orbits/__init__.py`
- `src/exoplanet/light_curves/__init__.py`
- `src/exoplanet/distributions/__init__.py`
- `src/exoplanet/utils.py`
- `src/exoplanet/units.py`
- `src/exoplanet/interp.py`
- `src/exoplanet/estimators.py`
- `src/exoplanet/compat.py`
- `src/exoplanet/citations.py`
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
- A quick intro to PyMC
- Hello world (AKA fitting a line to data)
- Define the priors on each parameter:
- Define the likelihood. A few comments:
- 1. For mathematical operations like "exp", you can't use
- numpy. Instead, use the mathematical operations defined
- in "pm.math".
- 2. To condition on data, you use the "observed" keyword
- argument to any distribution. In this case, we want to
- use the "Normal" distribution (look up the docs for
- Data & models
- Overview

## Executable command hints
- $$

## Warnings and pitfalls
- The first is the classic fitting a line to data with unknown error bars, and the second is a more relevant example where we fit a radial velocity model to the public radial velocity observations of [51 Peg](https://en.wikipedia.org/wiki/51_Pegasi).
- **Exercise:** Try changing the initial guesses for the parameters (as specified by the `initval` argument) and see how sensitive the results are to these values. Are there some parameters that are less important? Why is this?
- As above, the top plot shows the raw observations as black error bars and the RV trend model is overplotted in blue.
- This is a good parameterization for exoplanetary systems and binary stars, but it is sometimes not sufficient for systems with multiple massive bodies where the interactions will be important to the dynamics.
- The third physical parameter can always be computed using the other two so `exoplanet` will throw an error if three are given (even if they are numerically self-consistent).
- # Compute the convergence stats
