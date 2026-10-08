# A single-hit Poisson model of Cre mRNA delivery

Authors: Julia Borgsved, Angela Lyman  
CB2330 project, autumn 2026.

## What this is

Sago et al. (2018, PNAS) deliver Cre mRNA to a reporter mouse at 10, 100 and 1000 ng and
measure the percentage of cells that switch to RFP+. The response rises with dose but is not otherwise modelled.

This project proposes a mechanism for it. Each cell receives a Poisson number of functional
mRNA copies with mean λ = kD, and a single copy is enough to switch the cell, so

    P(RFP+ | D) = 1 - exp(-k*D)

with one fitted parameter, k, the functional delivery rate in copies per cell per ng. The
notebook simulates the model forwards, fits k backwards against the paper's three points,
and tests how far that estimate can be trusted.

## What it found

- **k̂ = 0.00191 per ng** for L2K, fitted by a parameter sweep scored with sum of squared error.
- Shifting the three observed fractions by up to ±0.03 (reading error on the published bars)
  and refitting 300 times puts k between roughly **0.00175 and 0.00209 per ng**.
- Fitting simulated data generated from a known k recovers it with no detectable bias, so
  the fitting procedure itself is sound.
- **The model is rejected by its own consistency check.** Finding k from the probability formula using dose separately gives k = 0.0041, 0.0015 and 0.0020 per ng for 10, 100 and 1000 ng. These should agree and do not, and the gap is far outside the refit interval.

## How to run

Requires Python 3 (with built-in csv and math) and matplotlib. No other dependencies — the random number generator is a hand-written LCG and the arithmetic is plain Python.

    pip install matplotlib jupyter
    jupyter notebook project.ipynb

Then run all cells, top to bottom. Runtime is a few seconds. Paths are relative, so run it
from the repository root.

## Layout

    README.md          this file
    project.ipynb      the project card, then the work
    data/
      dose_response.csv  the three points from Fig. 1G
      README.md          where they came from and their shape

## Source

Sago, C. D. et al. (2018). High-throughput in vivo screen of functional mRNA delivery identifies nanoparticles for endothelial cell gene editing. *PNAS* 115(42): E9944–E9952.
https://doi.org/10.1073/pnas.1811276115
