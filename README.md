# Finding quantum error-correction thresholds

Monte Carlo experiments exploring how four surface-code memory configurations respond to phenomenological noise. The notebooks generate circuits with [Stim](https://github.com/quantumlib/Stim), run experiments with Sinter, decode with PyMatching, and plot logical error rate against physical error rate.

## What this project investigates

A quantum error-correction threshold is the physical error rate below which increasing a code's distance suppresses its logical error rate. Rather than deriving a threshold analytically, these experiments sample several code distances and noise levels. A crossing—or a clear change in how logical error rate scales with distance—indicates the threshold region.

This repository is an exploratory numerical study, not a precision threshold benchmark. The sampled physical error rates are fairly coarse, so the plots identify a region rather than a high-precision value.

## Experiments

| Notebook | Stim circuit | Logical memory basis | Rounds |
|---|---|---:|---:|
| [`rmx.ipynb`](rmx.ipynb) | Rotated surface code | X | `d` |
| [`rmz.ipynb`](rmz.ipynb) | Rotated surface code | Z | `3d` |
| [`urmx.ipynb`](urmx.ipynb) | Unrotated surface code | X | `3d` |
| [`urmz.ipynb`](urmz.ipynb) | Unrotated surface code | Z | `3d` |

Each notebook samples:

- code distances: 11, 13, 15, 17, and 19
- physical error rates: 0.05, 0.08, 0.10, 0.20, 0.30, 0.40, and 0.50
- decoder: `pymatching`
- stopping condition: up to 100,000 shots or 500 errors per task
- workers: 4

## Run locally

Python 3.11 is recommended.

```bash
git clone https://github.com/ayomikun-adekeye/finding-qecc-thresholds.git
cd finding-qecc-thresholds
python3.11 -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m pip install jupyterlab
jupyter lab
```

Open any notebook and run its cells from top to bottom. Full runs can be computationally expensive; reduce the distances, noise points, or shot limit for a quick validation.

## Reading the plots

Each curve represents one code distance. Below a threshold, larger distances should produce lower logical error rates. Near the threshold region, curves tend to meet or cross. Above it, increasing the distance no longer helps and may increase the logical error rate.

## Reproducibility notes

The dependency versions in [`requirements.txt`](requirements.txt) match a clean environment used for a reduced end-to-end validation. That check covered circuit generation, sampling, and decoding at distance 3 for 100 shots; it did not reproduce every full notebook result.

## Possible next improvements

- rerun all notebooks from a fresh kernel and commit consistent outputs
- refine the physical-error-rate grid around each apparent crossing
- export representative plots into the repository for at-a-glance results
- report uncertainty intervals and the method used to estimate each threshold
