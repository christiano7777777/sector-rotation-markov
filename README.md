# Is Sector Rotation Predictable?

### A Markov-Chain Test Against the Correct Random-Matrix Null

Chan Tsz Him Chris — July 23, 2026

This repository holds the paper and the full analysis notebook for a short research paper that formalizes S&P 500 "sector rotation" as a discrete-time Markov chain and tests whether its spectral structure is statistically real, using the null model actually appropriate for a row-stochastic matrix (the circular law for random Markov matrices) rather than the Marchenko–Pastur law that's often reached for by default.

**Result:** the chain is well-defined, ergodic, and has a real in-sample spectral gap — but every eigenvalue is statistically indistinguishable from what a random 11×11 stochastic matrix would produce, under both a closed-form disk-radius test and a 5,000-replication permutation bootstrap. The same holds symmetrically for the "leader" (best-performer) chain. This null result is explained by mechanism: cap-weighted sector ETFs embed no forced rebalancing flow that would imprint serial structure on daily sector leadership.

Read the paper: [`paper/Is Sector Rotation Predictable - A Markov-Chain Test Against the Correct Random-Matrix Null.pdf`](paper/Is%20Sector%20Rotation%20Predictable%20-%20A%20Markov-Chain%20Test%20Against%20the%20Correct%20Random-Matrix%20Null.pdf)

## Contents

```
.
├── sector_rotation_markov.ipynb   # the single notebook — full analysis, start to finish
├── paper/
│   ├── *.pdf                       # the compiled paper
│   ├── main.tex                    # LaTeX source
│   ├── table_pi.tex, tables_matrices.tex   # auto-generated table includes
│   └── figures/                    # figures used in the paper
├── data/
│   └── sp500_sector_returns_daily.csv   # cached CRSP daily sector-ETF return panel, 2010–2024
├── figures/                        # notebook output figures (regenerated on run)
├── requirements.txt
└── README.md
```

## Running it

```bash
pip install -r requirements.txt
jupyter notebook sector_rotation_markov.ipynb
```

The notebook uses the cached return panel in `data/` by default, so **no WRDS/CRSP credentials are required** to reproduce every result. If you want to re-pull the raw data yourself, delete `data/sp500_sector_returns_daily.csv` and the first data cell will re-pull via the `wrds` package (requires a WRDS account with CRSP access).

Two cells run 5,000-replication permutation bootstraps (the laggard-chain and leader-chain null tests in Sections 7 and 8.3) and take several minutes each — everything else runs in seconds.

## Structure

The notebook mirrors the paper's own structure section by section: state-space construction, MLE/Laplace-smoothed estimation, ergodic properties (stationary distribution, recurrence, hitting times), spectral analysis, the random-matrix null test (both the disk-radius approximation and the permutation bootstrap), robustness checks (Markov order, time-homogeneity, and the leader-chain reflection), a microstructural mechanism explanation, and a worked hand-computable toy example in the appendix.

## Data

Eleven SPDR Select Sector ETFs (XLK, XLV, XLF, XLY, XLC, XLI, XLP, XLE, XLU, XLRE, XLB) as tradable proxies for the GICS sectors. Daily total returns from CRSP (`dsf`), 2010-01-01 through 2024-12-31, pulled via WRDS. The Markov-chain analysis is restricted to the common period where all 11 sectors have data simultaneously (2018-06-20 to 2024-12-31), since Communication Services and Real Estate launched later than the rest.

## References

- Bordenave, C., Caputo, P., & Chafaï, D. (2012). Circular law theorem for random Markov matrices. *Probability Theory and Related Fields*, 152(3–4), 751–779.
- Marchenko, V. A., & Pastur, L. A. (1967). Distribution of eigenvalues for some sets of random matrices. *Matematicheskii Sbornik*, 114(4), 507–536.
- Seneta, E. (2006). *Non-negative Matrices and Markov Chains* (2nd ed.). Springer.
- Kemeny, J. G., & Snell, J. L. (1976). *Finite Markov Chains*. Springer-Verlag.
- Levin, D. A., Peres, Y., & Wilmer, E. L. (2017). *Markov Chains and Mixing Times* (2nd ed.). American Mathematical Society.
- Norris, J. R. (1998). *Markov Chains*. Cambridge University Press.
- Hamilton, J. D. (1989). A new approach to the economic analysis of nonstationary time series and the business cycle. *Econometrica*, 57(2), 357–384.
- Moskowitz, T. J., & Grinblatt, M. (1999). Do industries explain momentum? *The Journal of Finance*, 54(4), 1249–1290.
- Jacobsen, B., Stangl, J. S., & Visaltanachoti, N. (2009). Sector rotation across the business cycle. Working paper, SSRN 1467457.
- Molchanov, A., & Stangl, J. (2024). The myth of business cycle sector rotation. *International Journal of Finance & Economics*, 29(4), 4419–4442.
- Laloux, L., Cizeau, P., Bouchaud, J.-P., & Potters, M. (1999). Noise dressing of financial correlation matrices. *Physical Review Letters*, 83(7), 1467–1470.
- Plerou, V., Gopikrishnan, P., Rosenow, B., Amaral, L. A. N., & Stanley, H. E. (2000). Random matrix theory approach to financial cross-correlations. *Physica A*, 287(3–4), 374–382.
- Bouchaud, J.-P., & Potters, M. (2009). Financial applications of random matrix theory: a short review. arXiv:0910.1205.
- CRSP, University of Chicago Booth School of Business. Daily Stock File, via WRDS.
