# The Cognitive Monte Carlo: Externalizing Clinical Uncertainty

This repository contains Supplementary Material S1 for the paper **"The Cognitive Monte Carlo: Externalizing Clinical Uncertainty Through Transparent Probabilistic Modeling."** 

It provides an illustrative Python implementation showing how soft, qualitative clinical heuristics—such as *"worsens for 3–5 days and resolves in 1–2 weeks"*—can be formalized into explicit probability distributions, propagated via Monte Carlo sampling, and visually communicated.

> **⚠️ Important Clinical Disclaimer:**  
> This simulation generates **model-derived probabilities** from explicitly specified assumptions. It does **NOT** provide empirically validated clinical event rates and should **NOT** be used as a validated clinical decision tool or prediction model.

---

## Key Features

- **Implicit Heuristic Formalization:** Translates qualitative medical knowledge into formal statistical models (Uniform and Lognormal distributions).
- **Exact Numerical Reproducibility:** Uses a fixed random seed (`42`) over $100,000$ virtual iterations.
- **Logical Constraint Enforcement:** Ensures logical consistency (e.g., recovery cannot precede the end of peak worsening).
- **Zero Heavy Dependencies:** Custom, chunked Gaussian Kernel Density Estimation (KDE) written natively in NumPy to avoid extra visualization library dependencies.
- **Publication-Ready Plotting:** Automated script that outputs high-resolution figures (`300 DPI`) with embedded descriptive statistics.

---

## Model Parameterization

| Parameter | Clinical Heuristic Translation | Mathematical Representation |
| :--- | :--- | :--- |
| **Peak Worsening** | Days 3–5 post-onset | $\text{Uniform}(3.0, 5.0)$ |
| **Recovery Horizon** | Median total recovery ~10.5 days | $3.0 + \text{Lognormal}(\mu, \sigma)$ |
| **Log-Location ($\mu$)** | Corrected target median ($10.5 - 3.0 = 7.5$) | $\mu = \ln(7.5) \approx 2.0149$ |
| **Log-Scale ($\sigma$)** | Recovery variation tail | $\sigma = 0.30$ |
| **Consistency Rule** | Min interval after peak worsening | $\max(\text{Recovery}, \text{Peak} + 0.5)$ |

---

## Requirements & Setup

This script runs on Python 3.8+ with minimal core statistical packages.

### Prerequisites

```bash
pip install numpy matplotlib

```

### Running the Simulation

Run the Python script directly to execute the simulation, display console telemetry, and save the figure:

```bash
python cognitive_monte_carlo.py

```

---

## Expected Outputs

1. **Console Telemetry:** Prints model-internal validation checks, empirical percentiles (P25, P50, P75, P95, P99), cumulative recovery metrics, and day-by-day probability progression.
2. **Saved Figure:** Outputs `Figure_S1_Cognitive_Monte_Carlo.png` in the root directory.

---

## License

Distributed under the MIT License. See `LICENSE` for more information.

