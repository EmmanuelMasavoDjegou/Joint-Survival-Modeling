# Joint Modeling of Longitudinal and Survival Data in Big Health Datasets

**Paper Summary — 2024**  
This repository provides a concise overview of joint modeling techniques for longitudinal and survival data with a focus on the `jmBIG` framework and related R packages. The notes are based on a full review of recent methodologies for large-scale electronic health records (EHR) analysis.

---

## 🧠 Motivation

Traditional survival models often rely on static covariates measured at a single time point, failing to capture how patient profiles evolve over time. Joint modeling addresses this by incorporating:

- **Longitudinal data**: repeated clinical measurements (e.g., lab results, vitals)
- **Time-to-event data**: the time until a key event (e.g., death, relapse) occurs

**Use Cases**:
- Personalized healthcare interventions
- Monitoring disease progression and event risk (e.g., hospitalization, mortality)

---

## ⚙️ Model Structure

### 1. Longitudinal Submodel
Generalized Linear Mixed Model (GLMM):

η_i(t) = g(E[Y_i(t) | b_i]) = x_iᵀ(t)β + z_iᵀ(t)b_i


- `g(·)`: Link function  
- `x_i(t), z_i(t)`: Time-dependent covariates  
- `b_i ~ N(0, Δ)`: Random effects

### 2. Survival Submodel
Extended Cox Proportional Hazards Model:

h_i(t | H_i(t), w_i(t)) = h₀(t) · exp(γᵀw_i(t) + f(H_i(t), b_i, α))


- `H_i(t) = {η_i(s), 0 ≤ s < t}`: History of the longitudinal process  
- `f(·)`: Association between history and survival risk

### 3. Baseline Hazard (B-spline Representation)

- `B_q(t, ν)`: q-th B-spline basis function with knots `ν`

---

## 📐 Estimation Techniques

### Frequentist:
- Maximum Likelihood Estimation (MLE)
- Kaplan-Meier estimator
- Iterative optimization algorithms

### Bayesian:
- MCMC sampling for posterior distributions
- Incorporates prior knowledge
- Captures model uncertainty and non-linearity

p(β, θ | y, t) ∝ L(β, θ) · p(β, θ)

---

## 📦 R Packages for Joint Modeling

| Package        | Method      | Key Features |
|----------------|-------------|--------------|
| `jmBIG`        | Bayesian    | Scalable for large datasets, auto data split, conditional survival, random effects |
| `JMbayes2`     | Bayesian    | Time-varying coefficients, diagnostics, visualization |
| `fastJM`       | Bayesian    | Efficient MCMC, shared effects, scalability |
| `joinRML`      | Frequentist | MLE-based, shared random effects, good for big data |
| `rstanarm`     | Bayesian    | Stan backend, multiple longitudinal markers, diagnostics |

---

## 🚀 jmBIG Framework Highlights

- Tailored for **large-scale EHR analysis**
- Modular pipeline for:
  - Preprocessing
  - Model estimation
  - Posterior analysis
  - Conditional survival probabilities

### Core Functions

- `jim()`: Bayesian joint model fitting  
- `survitJMCS()`: Compute conditional survival probabilities  
- `joinRML_big()`: Fits joint model on chunks and aggregates estimates  
- `juntrig()`: Automates full modeling workflow

---

## 🧪 Output & Evaluation

- Posterior summaries: means, variances, credible intervals  
- Predicted longitudinal trajectories  
- Time-to-event survival probabilities  
- Visualization and diagnostic tools  
- Individual vs. population-level predictions

---

## ⚠️ Challenges & Considerations

- **Computational burden** (especially for full Bayesian inference)
- **Memory constraints** on large datasets
- **Model sensitivity** to parameter and prior choices

> ✅ Solutions include cloud-based computing, parallel processing, or memory-optimized tools like `jmBIG`.

---

## 📚 References

- Rizopoulos, D. et al. (2022). *Joint Modeling of Longitudinal and Survival Data in R with JMbayes2*  
- Rizopoulos, D. (2023). *Scalable Joint Models using jmBIG*

---

## 👨‍💻 Author

Notes prepared by **Emmanuel Masavo DJEGOU**, Ph.D. Candidate in Statistics  
Focus: Joint Modeling, Survival Analysis, AI in Health  
🔗 [LinkedIn](https://www.linkedin.com/in/emmanuel-djegou) • [Medium](https://medium.com/@emmanueldjegou5)

---

