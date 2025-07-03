# Joint Modeling of Longitudinal and Survival Data for Big Health Data

> **Paper Reviewed**:  
Bhattacharjee, A., Rajbongshi, B., & Vishwakarma, G.K.  
**jmBIG: Enhancing dynamic risk prediction and personalized medicine through joint modeling of longitudinal and survival data in big routinely collected data**  
*BMC Medical Research Methodology*, 24, 172 (2024).  
📎 https://doi.org/10.1186/s12874-024-02289-0

---

## 📌 Overview

This repository summarizes key concepts, models, and tools introduced in the 2024 paper by Bhattacharjee et al. The authors present `jmBIG` — a scalable **Bayesian framework** for **joint modeling of longitudinal and survival data** in the context of **large, routinely collected healthcare datasets** such as Electronic Health Records (EHRs).

---

## 🎯 Motivation

Traditional survival analysis often ignores temporal patterns in patient health trajectories. `jmBIG` integrates:

- **Longitudinal data**: repeated clinical measurements (e.g., biomarkers, vitals)
- **Time-to-event data**: event outcomes like death, disease onset, readmission

By modeling these jointly, `jmBIG` enables:

- Improved **dynamic risk prediction**
- Personalized treatment planning
- Handling **high-dimensional** and **heterogeneous** data at scale

---

## ⚙️ Model Structure

### 1. Longitudinal Submodel
Generalized Linear Mixed-Effects Submodel:

$$
\eta_i(t) = g\left(\mathbb{E}\left[Y_i(t) \mid b_i\right]\right) = x_i^\top(t)\beta + z_i^\top(t)b_i
$$

- `g(·)`: Link function assumed one-to-one  
- `x_i(t), z_i(t)`: Time-dependent design covariates for the fixed effects $\beta$ and random effects $b_i$, respectively  
- `b_i ~ MVN(0, D)` or `b_i ~ t(df)`: Random effects with $D$ the covariance matrix

### 2. Survival Submodel
Extended Cox Proportional Hazards Model:

$$
h_i(t \mid H_i(t), w_i(t)) = h_0(t) \cdot \exp\left( \gamma^\top w_i(t) + f(H_i(t), b_i, \alpha) \right)
$$

- `H_i(t) = {η_i(s), 0 ≤ s < t}`: History of the longitudinal process up to time $t$
- `f(·)`: Association between history and survival risk
- `w_i(t)`: Additional time-dependent covariates
- $\alpha$: Association between features of the longitudinal process up to time $t$ and the hazard of the event at the same time. 

### 3. Baseline Hazard (B-spline Representation)

$$
\log h_0(t) = \gamma_0^0 + \sum_{q=1}^{Q} \gamma_0^q \cdot B_q(t, \mu)
$$

- `B_q(t, ν)`: q-th B-spline basis function with knots $\mu$

---

## 📐 Estimation Techniques

### Frequentist:
- Maximum Likelihood Estimation (MLE) via iterative optimization algorithms
- Nonparametric Estimation (Kaplan-Meier Estimator)

### Bayesian:
- Markov Chain Monte Carlo (MCMC) sampling for posterior distributions
- Incorporates prior knowledge
- Estimate model uncertainty and can account for non-linearity

---

## 📦 R Packages for Joint Modeling

| Package        | Method      | Key Features |
|----------------|-------------|--------------|
| `JMbayes2`     | Bayesian    | Time-varying coefficients, diagnostics, visualization |
| `fastJM`       | Bayesian    | Efficient MCMC, shared effects, scalability |
| `joineRML`     | Frequentist | MLE-based, shared random effects, good for big data |
| `rstanarm`     | Bayesian    | Stan backend, multiple longitudinal markers, diagnostics |
| `jmBIG`        | Bayesian    | Scalable for large datasets, auto data split, conditional survival, random effects |

---

## ⚠️ Challenges & Considerations

- **Computational burden** (especially for full Bayesian inference)
- **Memory constraints** on large datasets
- **Model sensitivity** to parameter and prior choices

> ✅ Solutions include cloud-based computing, parallel processing, or memory-optimized tools like `jmBIG`.

---

## 🚀 jmBIG Framework Highlights

- Tailored for **large-scale EHR analysis**
- Modular pipeline for:
  - Preprocessing
  - Model estimation
  - Posterior analysis
  - Conditional survival probabilities

### Core Functions

The core functions include `jmbayesBig()`, `jmcsBig()`, and `jmstanBig()`. The function `joinRMLBig()` offers the fastest processing time on EHR data by using a frequentist maximum likelihood estimation approach optimized for big data applications.

---

## 🧪 Output & Evaluation

- Posterior summaries: means, variances, credible intervals  
- Predicted longitudinal trajectories  
- Time-to-event survival probabilities  
- Visualization and diagnostic tools  
- Individual vs. cluster-level predictions


---

## 👨‍💻 Author

Notes prepared by **Emmanuel Masavo DJEGOU**, Ph.D. Candidate in Statistics @ Missouri S&T, Data Science Intern @RGA  
Focus: Joint Modeling, Survival Analysis, Biometric Data  
---

