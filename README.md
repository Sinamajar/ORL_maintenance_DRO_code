# ORL_maintenance_DRO_code

Code accompanying **Research Problem 2 (RP2)**: a **distributionally robust age-based maintenance** problem under **moment uncertainty** (known mean lifetime and variance, unknown lifetime distribution).

This repository implements the numerical experiment used in the paper and reproduces the main plot and the optimization summary table.

---

## What this repository contains

- `RP2_reproduce_results.py`  
  Sweeps a range of lifetime standard deviations (σ), evaluates the robust objective \(Q(\alpha)\), computes the minimizer \(\alpha^\*\) (when finite), and produces:
  - a figure: `Q_alpha_multisigma.png`
  - a printed table of results (σ, feasibility checks, \(\alpha^\*\), \(Q(\alpha^\*)\), and \(T^\*=\mu\alpha^\*\))

---

## Model & notation (high level)

We consider an age-based replacement policy with preventive replacement age \(T\), preventive cost \(c_p\), and failure replacement cost \(c_f\).  
The lifetime distribution is not known exactly, but is assumed to belong to a moment-based ambiguity set defined by the **mean** \(\mu\) and **variance** \(\sigma^2\). The objective is to choose \(T\) that minimizes the **worst-case** long-run average cost rate over all distributions in the ambiguity set.

The script uses the paper’s one-dimensional reformulation in terms of \(\alpha = T/\mu\) and evaluates the function \(Q(\alpha)\) over the feasible interval \((\alpha_1,\alpha_2)\).

---

## Parameter values (as in the paper)

The default parameters are set to the values **suggested in the paper**:

- Mean lifetime: `mu = 100` (weeks)
- Preventive replacement cost: `c_p = 500`  *(paper-suggested)*
- Failure replacement cost: `c_f = 6000`    *(paper-suggested)*

The script then sweeps σ over a grid (modifiable in the code):
```python
sigmas = np.linspace(1, 48, 12)
