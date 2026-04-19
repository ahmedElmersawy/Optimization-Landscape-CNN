# Optimization Landscape Analysis of a Fixed Convolutional Sigmoid Network  
**Author:** Ahmed Elmersawy (`aelmersa@purdue.edu`)

---

## Overview

This repository contains the full experiment notebook accompanying the paper:

> *Optimization Landscape Analysis of a Fixed Convolutional Sigmoid Network for Inverse Problems*  
> Ahmed Elmersawy, NeurIPS 2024 format, ECE 50024 Project 2026

The project analyzes the optimization landscape of a fixed single-layer convolutional neural network with sigmoid activation used for inverse reconstruction. The objective is to recover an input $x^*$ that minimizes:

$$J(x) = \|y - h(Ax)\|_2^2$$

where $A$ is a fixed convolution operator, $h$ is a sigmoid activation with stiffness parameter $\alpha$, and $y \in \{0,1\}^N$ is a binary target.

---

## Repository Structure
├── notebook.ipynb          # Main experiment notebook (all cells)
├── figures/                # Generated figures used in the paper
├── csvs/                   # Saved experiment results (CSV format)
└── README.md

---

## Experiments

The notebook covers the following experiments:

| Section | Experiment | Key Result |
|---|---|---|
| §6.2 | Sigmoid stiffness sweep (α) | IoU peaks at α=2, degrades monotonically after |
| §6.3 | Cutoff threshold sweep (c) | V-shaped profile, optimal at c=0.5 |
| §6.4 | Gradient sparsity per optimizer | Adam retains 15% active gradients at α=20 vs <5% for others |
| §6.5 | Convolution kernel sensitivity | Laplacian hardest, identity-like easiest |
| §6.6 | Target pattern sensitivity | Stripes easiest, sparse dots hardest |
| §6.7 | Convergence curves | Adam fastest with lowest variance |
| §6.11 | Success rate analysis | Adam maintains IoU>0.7 up to α=12 |
| §6.12 | Qualitative reconstruction | Non-uniqueness demonstrated across optimizers |

---

## Optimizers Compared

- **Projected Gradient Descent (PGD)**
- **Momentum**
- **Nesterov Accelerated Gradient**
- **Adam**
- **L-BFGS-B**

---

## Setup

No special installation required beyond standard scientific Python:

```bash
pip install numpy scipy matplotlib pandas
```

Open the notebook in Google Colab or Jupyter:

```bash
jupyter notebook notebook.ipynb
```

---

## Key Findings

1. **Sigmoid stiffness** is the primary driver of optimization difficulty. As α increases, the sigmoid derivative collapses to a Dirac delta, causing gradient sparsity and effective dimensional collapse.

2. **Adam outperforms all methods** in high-α regimes by maintaining a significantly higher fraction of active gradient components at convergence (~15% at α=20 vs <5% for non-adaptive methods).

3. **Convolution structure** independently controls landscape complexity — Laplacian kernels introduce strong variable coupling and produce the highest loss across all optimizers.

4. **Reconstruction is edge-driven**: gradients are active only near the sigmoid transition boundary $Ax \approx c$, forcing early iterations to reconstruct edges before filling interior regions.

5. **Non-uniqueness**: multiple distinct inputs can produce identical outputs, meaning low loss does not guarantee recovery of the true signal.

---

## Paper

The full paper is included in the submission and follows the NeurIPS conference format (up to 10 pages). The LLM Reflection Report is submitted as a separate PDF document.

---

## License

For academic use only. ECE 50024, Purdue University, Spring 2026.
