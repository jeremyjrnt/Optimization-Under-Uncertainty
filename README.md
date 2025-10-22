# 🧮 Optimization Under Uncertainty

**Author:** Jeremy Jornet  
**Institution:** Technion – Israel Institute of Technology  
**Course:** Optimization Under Uncertainty  

---

## 📘 Overview

This repository contains four major projects exploring decision-making under uncertainty — combining **Robust Optimization**, **Distributionally Robust Optimization (DRO)**, **Sample-based Multi-Stage Optimization**, and an **extension of the Joint Estimation and Robustness Optimization (JERO)** framework.

Each notebook implements and analyzes optimization formulations that remain feasible and near-optimal when model parameters, distributions, or data are uncertain.

---

## 🎯 Global Objective

> Design, implement, and compare optimization models that balance **performance, tractability, and robustness** across deterministic, probabilistic, and data-driven uncertainty settings.

The projects progressively cover:

- Analytical derivation of **robust counterparts (RCs)** for uncertain optimization problems.  
- Convex and **semidefinite reformulations** using duality.  
- Empirical validation through **Monte Carlo simulations**.  
- New methodological contributions extending robust optimization to **estimation-aware** settings.

---

## 📁 Repository Structure

Optimization_Under_Uncertainty/
│
├── Robust_Optimization.ipynb
│   ── Implementation of classical robust optimization methods
│
├── Distributionally_Robust_Optimization.ipynb
│   ── Implementation of distributionally robust optimization
│
├── SAA_SRO_MultiStage_Optimization.ipynb
│   ── Multi-stage optimization with Sample Average Approximation (SAA)
│      and Sample Robust Optimization (SRO)
│
├── Research_Project_JERO.pdf
│   ── Research project extending the JERO framework
│      (Joint Estimation and Robustness Optimization)
│
└── README.md

---

## 🧠 First Part – Robust Optimization

**Goal:** Derive and solve robust counterparts for uncertain linear and network flow problems; analyze cost–robustness trade-offs.

**Highlights**
- Robust min-cost flow with ℓ∞, ℓ₂, and ℓ₁ uncertainty sets.  
- Production-mix model with distinct uncertainty for objectives and constraints.  
- Duality-based reformulations and SDP derivations.  
- Monte Carlo validation confirming >95 % feasibility under uncertainty.

**Libraries:** `PICOS`, `CVXPY`, `NetworkX`, `Gurobi`, `CVXOPT`, `Matplotlib`

---

## 🧩 Second Part – Distributionally Robust Optimization (DRO)

**Goal:** Optimize against **ambiguity in probability distributions** using various ambiguity sets.

**Implemented Sets**
1. Moment-based DRO  
2. Moment-lifting DRO  
3. Data-driven moment ambiguity sets  
4. 1-Wasserstein metric DRO  
5. ∞-Wasserstein (Sample Robust Optimization)

**Experiments**
- Implemented as **semidefinite programs** in CVXPY.  
- Sensitivity analysis over sample size *(N = 10 – 10 000)* and hyper-parameters *(γ₁, γ₂, εₙ)*.  
- Demonstrated convergence of DRO → nominal solution as N increases.

**Key Insights**
- Wasserstein DRO generalizes best for small N.  
- γ-parameters tune the conservatism/variance trade-off.  
- Theoretical consistency with Esfahani & Kuhn (2018).

**Libraries:** `CVXPY`, `NumPy`, `SciPy`, `Matplotlib`

---

## 🔄 Third Part – SAA, SRO & Multi-Stage Optimization

**Goal:** Study **multi-stage stochastic decision-making** using  
Sample Average Approximation (SAA), Sample Robust Optimization (SRO), and Linear Decision Rules (LDRs).

**Applications**
- 5-stage inventory control with uncertain demand.  
- 10 Monte Carlo SAA experiments (N = 10 000) + scenario-tree (branching = 8).  
- Comparison of SAA vs SRO vs Robust vs Dynamic Programming (DP).

**Findings**
- Robust LDR policies = always feasible but conservative.  
- SAA improves with N; SRO performs better under data scarcity.  
- Dynamic-programming lower bound (107 cost units) validates formulations.  
- Introduced **cross-validated Wasserstein radius** εₙ.

**Libraries:** `CVXPY`, `NumPy`, `Pandas`, `Matplotlib`

---

## 🔬 Research Project – Joint Estimation and Robustness Optimization (JERO)

**Reference Paper:**  
T. Zhu, J. Xie & M. Sim (2020).  
[*Joint Estimation and Robustness Optimization*](https://pubsonline.informs.org/doi/abs/10.1287/mnsc.2020.3898?journalCode=mnsc).  
*Management Science*, 66(12).  

### Concept
The JERO framework unifies **parameter estimation** and **robust optimization**, deriving uncertainty sets directly from estimation metrics (e.g., OLS, MLE) instead of arbitrary radii.  
It maximizes robustness by finding the largest uncertainty radius *r* consistent with a target goal cost τ₀.

### Implementation Highlights
- Theoretical derivations for Linear and Poisson regression.  
- Convex dual reformulations via **Fenchel duality**.  
- Real-world case: **Healthcare reimbursement optimization** (26 hospitals, 25 500 patients).  
- JERO solutions maintain robustness with realistic budgets (~102 M ¥).

---

### ✨ Extensions Developed

#### 1️⃣ Regularization-Based Uncertainty Sets
Defined  
\( U_\Lambda = \bigcup_{\lambda∈[0,Λ]} \hatβ(λ) \)  
where each estimator is obtained from penalized fitting \( \minβ ℓ(β;D)+λR(β) \).

- Links robustness ↔ generalization path.  
- Replaces radius r by interpretable regularization bound Λ.  
- Preserves convexity (Lasso, Ridge) and structure-aware robustness.

#### 2️⃣ Data-Space Uncertainty Sets
Defined uncertainty **directly in the data domain**:
\( U_D(r)=\{D':‖D'-D‖_F≤r\text{ or }dist(P'_n,P_n)≤r\} \).

- Captures measurement noise and sampling bias.  
- Allows probabilistic calibration of r (Wasserstein distance or statistical tests).  
- Faithfully models JERO’s premise: *uncertainty originates from data.*

#### 3️⃣ Automatic Bound Selection
Proposed a **doubling scheme** to automatically determine the upper bound r̄ for binary-search optimization, removing arbitrary hyper-parameters and ensuring logarithmic convergence.

---

## 📚 Key References

- Ben-Tal A., El Ghaoui L., Nemirovski A. (2009). *Robust Optimization*. Princeton UP.  
- Bertsimas D., Sim M. (2004). *The Price of Robustness*. *Operations Research*, 52(1).  
- Delage E., Ye Y. (2010). *DRO under Moment Uncertainty*. *Operations Research*, 58(3).  
- Esfahani P. M., Kuhn D. (2018). *Data-Driven DRO Using Wasserstein Metric*. *Math Programming*, 171.  
- Bertsimas D., Gupta V., Kallus N. (2018). *Data-Driven Robust Optimization*. *Math Programming*, 167(2).  
- Zhu T., Xie J., Sim M. (2020). *Joint Estimation and Robustness Optimization*. *Management Science*.  

---

## 💡 Learning Outcomes

- Deep understanding of **robust, distributionally-robust, and stochastic** optimization.  
- Implemented **convex / semidefinite** reformulations in Python.  
- Linked **estimation theory** with **robust optimization** (JERO extension).  
- Proposed new frameworks for **data-driven and regularization-based robustness**.  
- Built a consistent and reproducible experimental workflow.

---

## 🛠️ Stack

| Category | Tools / Libraries |
|-----------|------------------|
| Optimization | PICOS · CVXPY · CVXOPT · Gurobi |
| Data & Simulation | NumPy · SciPy · Pandas |
| Visualization | Matplotlib · Seaborn |
| Modeling | NetworkX |
| Environment | Python 3.11 · Jupyter Notebook |

