# SocioSINDy

Sparse Identification of Nonlinear Dynamics (SINDy) applied to socio-technical safety barriers.

This repository accompanies the ESREL 2026 conference paper:

> A. Subedi, N. Flehmig, S. Yin, and N. Paltrinieri, *AI-based Exploration of Socio-technical Safety Barrier Dynamics*, Proceedings of the European Safety and Reliability Conference (ESREL 2026), pp. 788–795.

**Paper:** [esrel26-p26256.pdf](https://cmsweb.com.sg/rps2prod/esrel2026/epro/pdf/esrel26-p26256.pdf)

## Background

Safety barriers are increasingly understood as socio-technical systems that integrate human, organizational, and technical aspects — yet their dynamic influence is difficult to quantify with conventional assessment methods. This study demonstrates the feasibility of data-driven identification of socio-technical safety barrier dynamics using the SINDy algorithm ([Brunton et al., 2016](https://doi.org/10.1073/pnas.1517384113)).

A system dynamics (SD) model of a hydrogen refueling station maintenance procedure (emptying the hydrogen tank) is used to generate a synthetic dataset. Two socio-technical safety barriers are studied — *communication reliability* and *stable zero enforcement reliability* (split into enforcement time and enforcement effectiveness) — and their effect on residual gas accumulation and error generation is identified from data. Two models are trained:

1. a **coefficient-focused model** (sparsity threshold 0.5), optimized for interpretability, yielding compact governing equations that make barrier interactions explicit (test R² = 0.910), and
2. a **prediction-focused model** (sparsity threshold 0.4), optimized for predictive performance, evaluated with 200 bootstrap subsets (mean R² = 0.965, 95% CI [0.938, 0.979]).

Both models retain couplings to all barrier variables, indicating that the barriers are structurally relevant to the system dynamics.

## Repository contents

- `socio_sindy.ipynb` — Jupyter notebook with the full analysis: data loading and pre-processing, both SINDy models, and evaluation (including the bootstrap confidence-interval histogram).
- `safety_barriers.csv` — synthetic dataset generated from the SD model: 243 samples (27 parameter combinations × 9 time steps) of three control features (the safety barriers) and three input features (residual gas discovery pending vent, probability of error generation, residual gas in hydrogen tank).
- `SocioSINDy_R2_hist.png` — bootstrap distribution of R² scores with the 95% confidence interval (Figure 2 in the paper).

## Getting started

The notebook requires Python 3 with the following packages:

```bash
pip install pysindy numpy pandas scikit-learn matplotlib
```

(Developed with pysindy 2.1.0, numpy 2.4.0, pandas 2.3.3, scikit-learn 1.8.0, and matplotlib 3.10.8.)

Then open and run `socio_sindy.ipynb`. All random seeds are fixed, so the results are reproducible.

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
