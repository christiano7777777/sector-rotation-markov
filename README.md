# Is Sector Rotation Predictable?

### A Markov-Chain Test Against the Correct Random-Matrix Null

Chan Tsz Him Chris — November 2026 · HKU Trading Group Quant Team (analyst contributors: Chan Tsz Him Chris, Aidarkhan Zhubatkan, Sojin Jeon)

This repository holds the paper and the full analysis notebook. The paper defines the daily S&P 500 sector "laggard" (the SPDR sector ETF with the lowest return) as the state of a Markov chain and asks whether today's laggard tells us anything about tomorrow's.

**Result:** no first-order memory. A pre-specified family of three tests (χ² independence, largest non-Perron modulus, trace) fails to reject (p = 0.36, 0.21, 0.58), against a noise benchmark derived from the circular law for random matrices with a variance profile, radius √((n−1)/N) = 0.078, rather than Marchenko–Pastur or the Dirichlet radius 1/√n, which is almost four times too wide here. Simulations show the tests would detect broad persistence or rotation of |λ| ≈ 0.05. Out of sample, models that use past laggards forecast worse than the laggard's unconditional frequency. Dependence at lags of two to eight days is detectable but small and does not improve forecasts. The result holds across alternative estimators, state definitions and sampling schemes.

Read the paper: [`paper/Is Sector Rotation Predictable - A Markov-Chain Test Against the Correct Random-Matrix Null.pdf`](paper/Is%20Sector%20Rotation%20Predictable%20-%20A%20Markov-Chain%20Test%20Against%20the%20Correct%20Random-Matrix%20Null.pdf)

## Contents

```
.
├── sector_rotation_markov.ipynb   # the single notebook: every number, table and figure in the paper
├── paper/
│   ├── *.pdf                       # the compiled paper
│   ├── main.tex                    # LaTeX source
│   └── figures/                    # figures used in the paper
├── data/
│   └── sp500_sector_returns_daily.csv   # cached CRSP daily sector-ETF total returns, 2010–2024
├── requirements.txt
└── README.md
```

## Running it

```bash
pip install -r requirements.txt
jupyter notebook sector_rotation_markov.ipynb
```

The notebook uses the cached return panel in `data/`, so no WRDS/CRSP credentials are needed to reproduce the results. It runs in about three minutes, uses one fixed seed so reruns are identical, and checks the transition counts against the paper's count table before running any test. Outputs go to `output/` (`results.json`, a workbook of all numbers, and the figures).

## Data

Eleven SPDR Select Sector ETFs (XLK, XLV, XLF, XLY, XLC, XLI, XLP, XLE, XLU, XLRE, XLB) as tradable proxies for the GICS sectors. Daily total returns from the CRSP daily stock file via WRDS, 2010-01-01 to 2024-12-31. The chain uses the common period in which all eleven funds trade, 2018-06-20 to 2024-12-31 (1,644 days, 1,643 transitions).

## Key references

- Bordenave, C., Caputo, P., & Chafaï, D. (2012). Circular law theorem for random Markov matrices. *Probability Theory and Related Fields*, 152(3–4), 751–779.
- Cook, N., Hachem, W., Najim, J., & Renfrew, D. (2018). Non-Hermitian random matrices with a variance profile (I). *Electronic Journal of Probability*, 23.
- Marchenko, V. A., & Pastur, L. A. (1967). Distribution of eigenvalues for some sets of random matrices. *Matematicheskii Sbornik*, 72(114)(4), 507–536.
- Diebold, F. X., & Mariano, R. S. (1995). Comparing predictive accuracy. *Journal of Business & Economic Statistics*, 13(3), 253–263.

The full reference list is in the paper.
