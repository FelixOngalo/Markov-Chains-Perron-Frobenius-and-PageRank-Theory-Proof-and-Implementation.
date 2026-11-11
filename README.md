# Markov Chains, Perron-Frobenius and PageRank

Finite Markov chains and PageRank implemented from scratch in R. The key
theorems are proved in the report and then checked numerically on simulated
graphs and webs.

## Question

How fast does a Markov chain forget its starting point, what controls that
speed, and why does PageRank converge quickly and have a unique answer?

## Key findings

*(Fill in after running: decay factor of the random walk versus its second
eigenvalue, mixing time, PageRank iterations at d = 0.85 versus the worst-case
bound, hitting-time agreement with simulation.)*

## What is in it

- **Contraction lemma:** every zero-sum vector shrinks by 1 - delta under a
  stochastic matrix with Doeblin constant delta. This alone proves existence,
  uniqueness and geometric convergence of the stationary distribution
  (Perron-Frobenius, positive case)
- **Reversible chains:** total variation distance bounded by the second
  eigenvalue, via symmetrisation and Cauchy-Schwarz
- **Periodicity:** why a plain walk on a bipartite graph never converges and
  the lazy walk does
- **Hitting times:** a linear system checked against simulation, plus a short
  proof of Kac's formula (expected return time = 1 / pi)
- **PageRank:** the Google matrix, the eigenvalue theorem (other eigenvalues
  are d times those of P), power iteration versus a direct linear solve, and a
  damping-factor scan

## Tools

R (base linear algebra: `eigen`, `solve`), dplyr, tibble, tidyr, ggplot2, Quarto.
No graph or Markov-chain packages.

## Reproduce

1. `install.packages(c("dplyr", "tibble", "tidyr", "ggplot2", "knitr", "quarto"))`
2. Run `R/01_run_experiments.R` (saves `data/clean/results.rds`)
3. Render `reports/report.qmd`

All data are simulated, so no download is needed.

## Project structure

```
R/markov_functions.R       chains, stationary distribution, TV, contraction constants, hitting times, PageRank
R/01_run_experiments.R     all experiments and checks
reports/report.qmd         theorems, proofs, results and interpretation
data/clean/                saved results (generated)
```

## Limitations

- Finite chains only; the positive case of Perron-Frobenius is proved and the
  general theorem is cited
- The spectral bound needs reversibility
- Single simulated graph and web, so numbers vary with the seed; real web
  graphs are heavier-tailed
- Dense eigen-decompositions are used for verification and do not scale
- Personalised PageRank, floating-point convergence and mixing-time lower
  bounds (conductance, Cheeger) are not covered
