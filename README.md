# Robust estimation of the skew-normal distribution from MADs about the quartiles

Code and simulation results for

> E. Pinsky, *Robust Estimation of the Skew-Normal Distribution from Mean Absolute
> Deviations about the Quartiles*, submitted to *Mathematics* (MDPI), 2026.

The paper proposes the quartile-MAD (Q-MAD) estimator of the location, scale and
shape of the skew-normal distribution and its winsorized variant (WQ-MAD). It
compares them with maximum likelihood (MLE), L-moments (LM), the method of moments
(MoM) and quartile matching (QM).

## Contents

| Path | Description |
|---|---|
| `code/snmad.py` | Closed-form `E|X-a|` for the skew-normal, its derivatives, MLE fit, plug-in system |
| `code/qmad.py` | Q-MAD estimator, quartile matching, method of moments, MLE wrapper |
| `code/wqmad.py` | Winsorized Q-MAD (`WQMAD(c=1.0)`) |
| `code/lmom.py` | L-moment estimator |
| `code/madshape.py` | MAD skewness `G` and MAD kurtosis `K` (closed form and sample versions) |
| `code/asym.py`, `theory*.py`, `wtheory.py`, `ltheory.py` | Influence functions, asymptotic variances, bias functionals |
| `code/sim.py`, `sim_extra*.py` | Monte Carlo study (fixed seed per configuration) |
| `code/shapes.py` | Effect of contamination on shape measures |
| `code/ais.py`, `ais_example.py`, `ais_sn.csv` | AIS body-mass-index application |
| `code/fig_*.py`, `figstyle.py` | Figures (written to `figures/`) |
| `code/analyze.py` | Performance measures from the saved simulation output |
| `simulation_results.csv` | Summary results for all simulation configurations and methods |

The scripts `build.py`, `make_fill.py`, `fill_*.py` and `sim_text.py` were used to
assemble the LaTeX manuscript. They are included for completeness and are not needed
to reproduce the numerical results.

## Requirements

Python 3.10+ with `numpy`, `scipy`, `pandas` and `matplotlib`.

## Quick start

```python
import numpy as np
from scipy.stats import skewnorm
from qmad import qmad_fit          # returns (m, s, alpha, delta)
from wqmad import WQMAD

y = skewnorm.rvs(3, loc=1, scale=2, size=500, random_state=1)
print(qmad_fit(y))
print(WQMAD(1.0).fit(y))
```

Run the scripts from inside `code/`. Raw simulation output is written to
`code/results/` (`python sim.py main`, then `sim_extra.py`, `sim_extra2.py` and
`sim_extra3.py` with the same argument).

## Data

`ais_sn.csv` is the `ais` dataset from the R package
[`sn`](https://cran.r-project.org/package=sn) (Australian Institute of Sport data;
Telford and Cunningham, 1991).

## Licence

MIT (see `LICENSE`).
