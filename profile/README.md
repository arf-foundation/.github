# Agentic Reliability Framework (ARF) – Stewarded Governance for AI Systems

<img src="https://raw.githubusercontent.com/arf-foundation/.github/main/assets/ARF%20-%20Primary%20Logo.png" alt="ARF Logo" width="200"/>

**Auditable cloud governance powered by Bayesian intelligence.** Build reliable, observable, and self‑healing AI systems for real‑world infrastructure.

🔐 **The core ARF engine is access‑controlled and not publicly available.**  
It is available only to qualified pilots and enterprise customers under **outcome‑based pricing**.

👉 [ARF Control Center (public demo UI – mock data only)](https://arf-frontend-sandy.vercel.app/)

---

## 🎯 Our Mission

ARF makes AI operations **provably safe, auditable, and transparent**.  
We provide a **mathematically rigorous governance layer** for deterministic and probabilistic decision‑making in production AI systems.

- ✅ Enable **provably safe AI operations** in cloud, hybrid, and multi‑agent environments.
- 🧮 Deliver **Cost‑Optimized Decisioning** (hybrid Bayesian inference + calibrated risk scoring).
- 🔍 Offer **full traceability** through auditable logs, Operational Memory, and transparent decision records.
- 🧭 **Steward the framework** – not a free‑for‑all, but a protected, pilot‑first product.

---

## 📐 Mathematical Foundations (Protected Engine)

### 1. Continuous Risk Calibration – Bayesian Beta‑Binomial Model

For each action category \(c\), ARF maintains a Beta posterior:

\[
\theta_c \sim \text{Beta}(\alpha_c, \beta_c)
\]

Prior parameters \((\alpha_{c,0}, \beta_{c,0})\) are domain‑informed (e.g., pessimistic for database changes).  
After observing \(s\) successes and \(f\) failures:

\[
\alpha_c = \alpha_{c,0} + s, \quad \beta_c = \beta_{c,0} + f
\]

Posterior mean (risk score) and variance:

\[
\mathbb{E}[\theta_c] = \frac{\alpha_c}{\alpha_c+\beta_c}, \quad
\mathrm{Var}[\theta_c] = \frac{\alpha_c\beta_c}{(\alpha_c+\beta_c)^2(\alpha_c+\beta_c+1)}
\]

### 2. Offline Pattern Discovery – Hamiltonian Monte Carlo (NUTS)

A logistic regression model captures complex, non‑linear interactions (time‑of‑day, user role, environment):

\[
\Pr(\text{failure}\mid \mathbf{x}) = \sigma\!\left( w_0 + w_{\text{role}} + w_{\text{env}} + w_{\sin}\sin(2\pi t/24) + w_{\cos}\cos(2\pi t/24) + \cdots \right)
\]

The weight posterior \(p(\mathbf{w} \mid \mathcal{D})\) is approximated using No‑U‑Turn Sampling (NUTS), a variant of HMC. The model is serialised to `hmc_model.json` and loaded at runtime.

### 3. Hyperprior Shrinkage – Hierarchical Beta Model

When enabled, category‑specific parameters share a common hyperprior:

\[
\alpha_c \sim \text{Gamma}(\alpha_0, \beta_0), \quad
\beta_c \sim \text{Gamma}(\alpha_0, \beta_0)
\]

This hierarchical structure pools statistical strength across categories, reducing overfitting when data is sparse.

### 4. Hybrid Risk Fusion

The final risk score is a convex combination:

\[
\text{risk} = w_{\text{conj}} \cdot \frac{\alpha}{\alpha+\beta} + w_{\text{hyper}} \cdot \mu_{\text{hyper}} + w_{\text{hmc}} \cdot p_{\text{hmc}}
\]

where \(\sum w_i = 1\). Weights are dynamically computed based on data volume and configuration (hyperparameters `n0` and `hyperprior_weight`). A context multiplier (e.g., `1.5` for production environment) caps the final risk at \(1.0\).

### 5. Expected Loss Minimisation (Cost‑Optimized Decisioning)

ARF chooses among three actions: **approve**, **deny**, **escalate** by minimising expected loss:

\[
\begin{aligned}
L_{\text{approve}} &= C_{\text{FP}}\cdot \text{risk} + C_{\text{impact}}\cdot b + C_{\text{predictive}}\cdot p_{\text{future}} + C_{\text{variance}}\cdot \mathrm{Var}[\theta] \\
L_{\text{deny}} &= C_{\text{FN}}\cdot (1-\text{risk}) + C_{\text{opp}}\cdot v \\
L_{\text{escalate}} &= C_{\text{review}} + C_{\text{uncertainty}}\cdot \psi
\end{aligned}
\]

Where:
- \(b\) = business impact (revenue loss estimate)
- \(p_{\text{future}}\) = predictive risk from time‑series forecasts
- \(v\) = opportunity value (e.g., estimated value of the action)
- \(\psi\) = epistemic uncertainty (see below)

All cost coefficients \(C_{\text{...}}\) are configurable and calibrated to organisational risk appetite.

### 6. Epistemic Uncertainty (CUDL – Causal Uncertainty Decomposition Layer)

Uncertainty is quantified via the **product of complements**:

\[
\psi = 1 - (1 - h)(1 - f)(1 - s)
\]

Where:
- \(h\) = hallucination risk (from ECLIPSE probe using entropy, evidence lift, contradiction)
- \(f\) = forecast uncertainty (1 − mean confidence of predictive models)
- \(s\) = data sparsity (exponential decay of historical data count)

The **Shapley value** decomposition attributes \(\psi\) to reducible vs irreducible sources, providing actionable insights:

\[
\phi_i = \sum_{S \subseteq U \setminus \{i\}} \frac{|S|!(|U|-|S|-1)!}{|U|!}\bigl[ \psi(S \cup \{i\}) - \psi(S) \bigr]
\]

### 7. Wilson Confidence Gate

Before promoting a policy or releasing a model, ARF checks the lower bound of a 99.9% Wilson confidence interval:

\[
p_{\text{lower}} = \frac{\hat{p} + \frac{z^2}{2n} - z\sqrt{\frac{\hat{p}(1-\hat{p})}{n} + \frac{z^2}{4n^2}}}{1 + \frac{z^2}{n}}, \quad z = 3.291
\]

Promotion occurs only if \(p_{\text{lower}} > 0.99999\).

### 8. Deterministic Policy Algebra

Policies form a Boolean algebra with homomorphic evaluation:

\[
f(p \land q) = f(p) \cup f(q), \quad
f(p \lor q) = f(p) \cap f(q), \quad
f(\neg p) = \text{complement of } f(p)
\]

Atomic predicates include `RegionAllowedPolicy`, `ResourceTypeRestrictedPolicy`, `MaxPermissionLevelPolicy`, `CostThresholdPolicy`. Composite policies are built with `&`, `|`, `~` operators and evaluated deterministically.

### 9. Governance Loop Invariants

For fixed inputs and a fixed engine state, the **same `HealingIntent`** (excluding timestamps and IDs) is produced every time. All random components use a deterministic RNG seeded from the intent ID, ensuring reproducibility and auditability.

---

## 📌 Publicly Listed Repositories (Reference Only)

These repositories are publicly visible for documentation and demo purposes.  
They **do not** contain the proprietary core engine.

| Repository | Description | Terms |
|------------|-------------|-------|
| [arf-spec](https://github.com/arf-foundation/arf-spec) | Canonical specification: data models, decision rules, API contracts | Shared under written terms |
| [arf-frontend](https://github.com/arf-foundation/arf-frontend) | Next.js demo dashboard (uses mock data only) | Shared under written terms |
| [pitch-deck](https://github.com/arf-foundation/pitch-deck) | Public overview and vision | Shared under written terms |

> 🔒 **All other repositories are private and access‑controlled.**  
> The core engine, API control plane, gateway, enterprise layer, research probes, and pricing calculator are **not publicly available**.

---

## 🚀 Ecosystem Overview (Public vs. Protected)

| Module | Purpose | Access |
|--------|---------|--------|
| **Public Specification** (`arf-spec`) | Data models, API contracts, decision rules | ✅ Public reference (shared under written terms) |
| **Public Demo UI** (`arf-frontend`) | Dashboard with mock data, showcases concepts | ✅ Public demo (shared under written terms) |
| **Protected Core Engine** | Continuous Risk Calibration, Operational Memory, governance loop | 🔒 Pilot / Enterprise only |
| **Protected API Control Plane** | FastAPI service with live endpoints | 🔒 Pilot / Enterprise only |
| **Enterprise Extensions** | Deterministic enforcement, audit trails, outcome‑based pricing | 🔒 Enterprise only |

---

## 🔐 Key Capabilities (Protected Engine)

| Capability (Public Name) | Implementation (Protected) |
|--------------------------|----------------------------|
| Continuous Risk Calibration | Conjugate priors + HMC |
| Operational Memory | FAISS‑based retrieval with similarity search |
| Cost‑Optimized Decisioning | Expected loss minimisation with trade‑off costs |
| Epistemic Uncertainty (CUDL) | Shapley value decomposition + Wilson confidence gate |

> ⚠️ These capabilities are **not** exposed in the public demo. They exist only in the protected core engine, available under pilot or enterprise terms.

---

## 🎮 Live Demos (Sanitised / Mock Data)

- **UI Concept Demo** – [Hugging Face Space](https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-v4) – Interactive risk dashboard (mock data only)
- **Sandbox API** – [Mock endpoint](https://huggingface.co/spaces/A-R-F/ARF-Sandbox-API) – Returns mock responses, not real Bayesian inference. Interactive docs at `/docs`.

**Example sandbox call (returns mock data):**

```bash
curl -X POST https://a-r-f-arf-sandbox-api.hf.space/v1/evaluate \
  -H "Content-Type: application/json" \
  -d '{"service_name":"api","event_type":"latency","severity":"high"}'
```

The real engine is **not publicly accessible**.

---

## 🔬 Bayesian Validation of the Governance Loop

Every decision path is subject to **posterior predictive checks**. For a given infrastructure intent \(X\) and observed outcome \(y\) (success/failure), the model’s posterior predictive distribution is

\[
p(\tilde{y} \mid X, \mathcal{D}) = \int p(\tilde{y} \mid X, \theta) \, p(\theta \mid \mathcal{D}) \, d\theta,
\]

where \(\theta\) includes all conjugate, HMC, and hyperprior parameters. The governance loop’s calibration is validated using the **Bayesian p‑value**:

\[
p_B = \Pr\bigl( T(\tilde{y}) \ge T(y) \mid X, \mathcal{D} \bigr),
\]

with \(T\) a discrepancy measure (e.g., the Brier score). Well‑calibrated systems yield \(p_B \approx 0.5\). ARF computes this offline and exposes it in `/metrics` as `arf_calibration_p_value`.

**Counterfactual analysis** extends this: for each denied action, we impute the counterfactual outcome if it had been approved using the **potential outcomes framework**:

\[
\text{ITE} = Y_i(1) - Y_i(0),
\]

where \(Y_i(1)\) is the outcome under approval, \(Y_i(0)\) under denial. The expected **cost of a wrong decision** is then:

\[
\mathbb{E}[\text{cost}_{\text{policy}}] = \mathbb{E}\bigl[ \mathbb{I}_{\text{deny}} \cdot \text{ITE} \cdot C_{\text{FN}} + \mathbb{I}_{\text{approve}} \cdot (1-\text{ITE}) \cdot C_{\text{FP}} \bigr].
\]

This counterfactual loss is logged for every decision and aggregated into a **policy regret** dashboard (enterprise only).

---

## 🌳 Tree‑of‑Thought Reasoning for Decision Paths

The governance loop operates as a **tree of sequential thought** where each branch corresponds to a possible action sequence (approve → escalate → deny, etc.). The system evaluates each branch using **expected utility**:

\[
U(\text{path}) = \sum_{t=1}^{T} \gamma^{t-1} \cdot \mathbb{E}[u(a_t \mid s_t)],
\]

with discount factor \(\gamma = 0.95\). The policy selects the branch that maximises \(U\). This is implemented via **dynamic programming over a finite horizon** (typically 3 steps). The branching factor is limited by the number of applicable policies and is computed on‑the‑fly.

**Tree‑of‑thought validation** checks for **planning coherence**: the chosen action at time \(t\) must be consistent with the optimal action at time \(t-1\) under the same belief state. Deviations trigger an **alarm** and are recorded for human review.

---

## 📊 Epistemic Uncertainty Decomposition with Shapley–Entropy

Beyond the product‑of‑complements formula, ARF decomposes epistemic uncertainty using **information‑theoretic Shapley values**:

\[
\phi_i^{\text{info}} = \sum_{S \subseteq U \setminus \{i\}} \frac{|S|!(|U|-|S|-1)!}{|U|!} \left[ H(\psi(S \cup \{i\})) - H(\psi(S)) \right],
\]

where \(H\) is the Shannon entropy of the uncertainty distribution. This gives the **reduction in uncertainty entropy** attributable to each source. The enterprise dashboard displays these values as a **waterfall chart**, enabling root‑cause analysis of high \( \psi \) incidents.

---

## 🧠 Enterprise Semantic Epistemic Layer (ESEL)

ARF maintains an **ontology of risk factors** (hierarchical Bayesian network) with conditional probability tables learned from historical data. For a given intent, the engine runs **belief propagation** to compute marginal posteriors of unobserved latent variables (e.g., “operator fatigue”, “infrastructure health”). The network is defined as:

\[
P(\mathbf{Z}, \mathbf{X}) = \prod_{j=1}^{J} P(Z_j \mid \text{Pa}(Z_j)) \cdot \prod_{i=1}^{I} P(X_i \mid \text{Pa}(X_i)),
\]

where \(Z_j\) are latent risk drivers, \(X_i\) observable metrics. The **epistemic score** is the variance of the posterior predictive distribution:

\[
\text{epistemic}_{\text{ESEL}} = \text{Tr}\bigl( \text{Cov}[\mathbf{Z} \mid \mathbf{X}] \bigr).
\]

This layer is **access‑controlled** and available only under enterprise agreements.

---

## ⚖️ Counterfactual Fairness & Bias Detection

Using **Pearl’s do‑calculus**, ARF audits decisions for demographic parity and equal opportunity. For a protected attribute \(A\) (e.g., region, user role), we compute:

\[
\text{CF fairness} = \bigl| P(\text{approve} \mid \text{do}(A=1), \mathbf{X}) - P(\text{approve} \mid \text{do}(A=0), \mathbf{X}) \bigr|.
\]

If the difference exceeds a threshold (default 0.1), the policy is flagged as potentially biased. A **counterfactual audit log** stores the imputed outcomes under all possible protected‑attribute values for every decision, enabling retrospective fairness analysis.

---

## 🔐 Mathematical Guarantees of Determinism

**Theorem**: For a fixed `RiskEngine` state and identical `InfrastructureIntent` and context, the same `HealingIntent` (except `intent_id`, `created_at`, `deterministic_id`, `detected_at`, `age_seconds`) is returned with probability 1.

**Proof sketch**:
- All RNG calls use a deterministic seed: `seed = hash(intent_id) mod 2**32` (if no ID, a SHA‑256 of the full intent+context).
- The `numpy.random.Generator` is seeded with this seed, and all sampling (conjugate, CVaR, etc.) uses this generator.
- The `BetaStore`, `HyperpriorBetaStore`, and `_component_risk_history` are updated deterministically based solely on observed outcomes; no other mutable state influences the calculation.
- The policy evaluator is deterministic by construction (no randomness).
- The `HallucinationRisk` probe returns a deterministic function of its inputs (sigmoid with fixed coefficients).
- Therefore, all intermediate values are functions of the same seed and inputs, yielding identical outputs.

The formal proof is available in the enterprise security package.

---

## 🎯 Bayesian Optimisation of Cost Coefficients

The cost coefficients \(C_{\text{FP}}, C_{\text{FN}}, C_{\text{review}}, \dots\) are not static; they are **tuned via Bayesian optimisation** to minimise total organisational loss:

\[
\mathcal{L}_{\text{org}}(C) = \sum_{t=1}^{T} \bigl( \mathbb{E}[L_{\text{approve}}] \cdot \mathbb{I}_{\text{approve}} + \mathbb{E}[L_{\text{deny}}] \cdot \mathbb{I}_{\text{deny}} + \mathbb{E}[L_{\text{escalate}}] \cdot \mathbb{I}_{\text{escalate}} \bigr).
\]

Using a **Gaussian process surrogate**, ARF explores the hyperparameter space and recommends new coefficients every 30 days (pilot customers) or continuously (enterprise). The acquisition function is **expected improvement**:

\[
\text{EI}(C) = \mathbb{E}\left[ \max(0, \mathcal{L}_{\text{min}} - \mathcal{L}(C)) \right].
\]

All optimisation runs are audited and can be reverted to previous states.

---

## 📈 Hierarchical Bayesian Model for Cross‑Category Risk

The hyperprior model is extended to a **full hierarchical Dirichlet‑Multinomial** for multi‑category outcomes:

\[
\boldsymbol{\theta}_c \sim \text{Dirichlet}(\boldsymbol{\alpha}_c), \quad
\boldsymbol{\alpha}_c \sim \text{Gamma}(\alpha_0, \beta_0) \text{ (elementwise)}.
\]

Posterior inference uses **Gibbs sampling** (via Pyro) with 1000 burn‑in steps. The resulting shrinkage estimates are used to compute **pooled risk scores** for categories with scarce data. This layer is enabled only when `use_hyperpriors=True` and Pyro is installed.

---

## 🛡️ Robustness to Adversarial Inputs – Bayesian Sensitivity Analysis

For each incoming intent, ARF performs a **local sensitivity analysis** by perturbing input features within a trust region \(\epsilon\) (default 0.05) and measuring the maximum change in the final decision:

\[
\text{sensitivity} = \max_{\| \delta \|_\infty \le \epsilon} \bigl| \text{risk}(X + \delta) - \text{risk}(X) \bigr|.
\]

If sensitivity exceeds a threshold (0.2), the intent is flagged as **adversarially fragile** and automatically escalated for human review. The perturbation distribution is modelled as a Gaussian with covariance estimated from historical noise – a **Bayesian robust optimisation** approach.

---

## 🧰 Enterprise‑Only Extensions (Referenced)

The following capabilities are **not** in the protected core engine; they are available under enterprise agreements:

- **Real‑time anomaly detection** using online changepoint detection (Bayesian CUSUM)
- **Automated healing actions** with safety bounds (constrained Bayesian optimisation)
- **Federated learning** across multi‑region deployments (privacy‑preserving posterior aggregation)
- **Explainable AI (XAI) module** – SHAP values for each feature in the HMC model
- **Compliance report generator** – automated SOC2 / ISO27001 evidence collection

For technical specifications, request the *Enterprise Technical Addendum*.

---

## 📚 References (Internal, Access‑Controlled)

1. *Bayesian Decision Theory for AI Governance* (ARF Whitepaper v4.2)
2. *Causal Inference in Policy Auditing* (Enterprise Technical Note 2026‑03)
3. *Tree‑of‑Thought Planning for Autonomous Systems* (Internal Research Report)
4. *Shapley‑Entropy Decomposition for Epistemic Uncertainty* (ARF Journal, forthcoming)

Request via `juan@arf-ai.com`.

---

*The mathematical guarantees, counterfactual analysis, and Bayesian optimisation layers ensure that ARF remains deterministic, auditable, and commercially credible under all conditions.*
