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

## 🧑‍💻 Contributing (Public Repositories Only)

We accept **limited contributions** to publicly listed repositories (`arf-spec`, `arf-frontend`, `pitch-deck`) – bug fixes, documentation, demo improvements.  
**We do not accept pull requests against private core repositories.**

1. Open an issue describing your proposed change.
2. Wait for a maintainer to assign the issue.
3. Sign a Contributor License Agreement (CLA) if requested.
4. Submit a pull request referencing the issue.

All changes are reviewed and merged at the founder’s discretion.

For questions about the protected engine or pilot access, please **do not open issues** – use the contact details below.

---

## 📬 Pilot Access & Contact

The core ARF engine is **not publicly available**. To request pilot access (time‑limited free trial) or enterprise licensing, contact us directly:

| Method | Details |
|--------|---------|
| **Email** | `juan@arf-ai.com` |
| **LinkedIn** | [Juan Petter](https://www.linkedin.com/in/petterjuan/) |
| **Book a Call** | [30‑Min Consultation](https://calendly.com/petter2025us/30min) |

**When requesting access, please provide:**  
- Your full name and organisation  
- Use case description  
- Expected monthly incident volume  
- Cloud environment (AWS, Azure, GCP, on‑prem)

---

## 📜 License & Legal

- **Publicly listed repositories** (`arf-spec`, `arf-frontend`, `pitch-deck`) are shared under written terms – **not open source**.
- **All private repositories** (core engine, API control plane, gateway, enterprise, research, pricing calculator) are **proprietary and access‑controlled** – no license is granted for public use without a written agreement.
- See the [NOTICE](https://github.com/arf-foundation/.github/blob/main/NOTICE) file for full details.

> All public demos, dashboards, and APIs use **mock data only**.  
> The **core Bayesian engine** is **not publicly available** – it is protected and access‑controlled.

---

## ❓ Frequently Asked Questions (FAQ)

<details>
<summary><strong>What is ARF?</strong></summary>
ARF is a governance layer that evaluates infrastructure decisions through a calibrated risk model. It recommends one of three actions — approve, deny, or escalate — together with a confidence indicator and a full audit trail. The core engine is access‑controlled and available only to qualified pilots.
</details>

<details>
<summary><strong>Is ARF publicly available?</strong></summary>
No. ARF is proprietary and access‑controlled. All repositories are private, and access to code, specifications, and supporting materials is granted only through approved pilot or enterprise arrangements.
</details>

<details>
<summary><strong>What’s the difference between the demo and the real engine?</strong></summary>
The demo is illustrative and uses mock or advisory data. It is designed to explain the workflow, not expose the protected engine. The real system is private and available only through pilot or enterprise access.
</details>

<details>
<summary><strong>How do I interpret the risk score?</strong></summary>
The risk indicator is a value between 0 and 1. Higher values indicate higher estimated risk. The recommended action — approve, deny, or escalate — comes from a structured trade‑off model, not a fixed threshold, and includes a full, auditable justification.
</details>

<details>
<summary><strong>Can I use the sandbox API for production?</strong></summary>
No. The sandbox API returns only mock data and is rate‑limited. It is intended for demonstration and testing only. For production use, you need pilot access to the real engine.
</details>

<details>
<summary><strong>What is Cost‑Optimized Decisioning?</strong></summary>
The system evaluates the potential cost of each possible action based on configurable parameters and the current risk assessment. It then selects the action with the lowest expected impact, producing a human‑readable, auditable justification.
</details>

<details>
<summary><strong>How many requests per second can the real engine handle?</strong></summary>
Performance depends on deployment scale. For pilot customers, we provide guidance based on your expected volume. Enterprise customers receive SLAs and dedicated capacity.
</details>

<details>
<summary><strong>What data is stored?</strong></summary>
The engine stores audit logs (decisions, risk scores, justifications) for compliance. No raw customer data is retained beyond what is required for the audit trail. Contact us for detailed retention policies.
</details>

<details>
<summary><strong>How can I engage with ARF?</strong></summary>
ARF is not accepting public contributions. Collaboration is handled through private pilot, partner, or enterprise channels. Reach out to discuss possible involvement.
</details>

<details>
<summary><strong>Where do I report a bug in the demo?</strong></summary>
Contact us directly through the support or pilot request channel. We review issues from approved users and pilot participants.
</details>

<details>
<summary><strong>Is there a community Slack?</strong></summary>
There is an invite‑only Slack workspace for pilot customers and approved collaborators. [Join here](https://join.slack.com/t/arf-gnv9451/shared_invite/zt-3t2omlgwg-Zf5_jmy9EIU~b51kMJ8Zdg).
</details>

<details>
<summary><strong>What license governs ARF materials?</strong></summary>
ARF materials are proprietary and access‑controlled. Any access to code, specifications, or supporting materials is governed by written agreement and approved use terms.
</details>

<details>
<summary><strong>Can I use the real engine in a commercial product?</strong></summary>
Yes, under a pilot or enterprise agreement. Outcome‑based pricing applies. Contact us for details.
</details>

---

## 🗺️ Roadmap (Protected Development)

The following capabilities are under active development for pilot and enterprise customers:

| Feature | Target Availability | Description |
|---------|---------------------|-------------|
| Enhanced policy algebra | Q3 2026 | AND/OR/NOT combinators with temporal constraints |
| Multi‑region audit federation | Q4 2026 | Cross‑region audit trail aggregation |
| Real‑time anomaly detection | Q1 2027 | Streaming ML for pre‑decision alerts |
| Cost‑based auto‑remediation | Q2 2027 | Automated healing actions within policy bounds |

> Note: The roadmap is shared with qualified pilots under written terms. Dates are estimates and subject to change.

---

## 🔒 Security & Compliance

- **Deterministic enforcement** – Every policy decision is mechanically enforced; no silent overrides.
- **Immutable audit logs** – All decisions are recorded with cryptographic signatures.
- **Access control** – Role‑based access control (RBAC) with SSO integration for enterprise.
- **Data privacy** – No raw customer data retained; only anonymised risk metrics and audit trails.
- **Compliance readiness** – Designed to support SOC2, ISO 27001, and GDPR requirements.

Pilot customers receive a full security architecture review and compliance package upon agreement.

---

## 📊 Support Channels

| Tier | Access | Response SLA |
|------|--------|---------------|
| Sandbox (public) | Community Slack, public issues | Best effort |
| Pilot | Email, private Slack, scheduled office hours | < 24 hours (business days) |
| Enterprise | Dedicated TAM, phone support, private Slack | < 4 hours (24/7) |

For pilot and enterprise support, contact `support@arf-ai.com` or use the provided private channels.

---

## 📝 Versioning & Changelog

- **Public specification** (`arf-spec`) is versioned and changes are documented in its [CHANGELOG](https://github.com/arf-foundation/arf-spec/blob/main/CHANGELOG.md).
- **Protected engine** versions are shared with pilot customers under written terms. No public changelog is provided.

Current protected engine version: **4.2.0** (available to qualified pilots).

---

## 🌐 Related Resources

- [ARF Control Center (demo UI)](https://arf-frontend-sandy.vercel.app/)
- [Public Specification (arf-spec)](https://github.com/arf-foundation/arf-spec)
- [Pilot Request Form](https://arf-ai.com/signup)
- [Slack Community (invite‑only for pilots)](https://join.slack.com/t/arf-gnv9451/shared_invite/zt-3t2omlgwg-Zf5_jmy9EIU~b51kMJ8Zdg)

---

## 📄 Legal Footer

© 2026 ARF Foundation. All repositories are private and access‑controlled. The core engine is proprietary. Selected materials are shared under written terms with qualified pilots and enterprise customers. Unauthorised access, copying, or distribution is prohibited.

---

*Stewarded by the founder – pilot‑first, outcome‑based pricing.*

---

## 📈 Calibration & Reliability Metrics (Protected Engine)

ARF continuously measures its own calibration using **Expected Calibration Error (ECE)** and **reliability diagrams**. For each predicted risk score \( \hat{p} \), the true outcome \( y \in \{0,1\} \) is logged. Binning predictions into \( M \) bins of equal width:

\[
\text{ECE} = \sum_{m=1}^{M} \frac{|B_m|}{n} \left| \frac{1}{|B_m|} \sum_{i \in B_m} y_i - \frac{1}{|B_m|} \sum_{i \in B_m} \hat{p}_i \right|
\]

A well‑calibrated system yields ECE near zero. ARF exposes this metric via `/metrics` endpoint (Prometheus) and alerts if ECE exceeds configurable thresholds (default 0.05).

---

## 🧵 Thread Safety & Concurrency Model

All core components (`BetaStore`, `HyperpriorBetaStore`, `_PendingRiskCache`, `_component_risk_history`) are **thread‑safe** using fine‑grained locks (`threading.RLock`). The governance loop is **stateless** across calls, with per‑call deterministic RNG seeded from the intent ID. The engine supports concurrent evaluation of thousands of intents without blocking.

---

## ⏱️ Time‑Decaying Risk Smoothing

To avoid overreaction to single incidents, ARF applies exponential smoothing to the risk score per component:

\[
\text{risk}_{\text{decayed}} = \lambda \cdot \text{risk}_{\text{prev}} + (1 - \lambda) \cdot \text{risk}_{\text{raw}}
\]

with \( \lambda = 0.9 \) (configurable). This smooths volatility and provides a more stable risk signal for long‑running services.

---

## 🧠 Semantic Memory – Operational Retrieval

Past incidents are stored as nodes in a directed graph, indexed by FAISS (`IndexFlatL2`, 384‑dim embeddings). At query time, ARF retrieves the top‑\(k\) similar incidents (cosine similarity) and computes a weighted similarity score. This memory is **read‑only** in the OSS edition; enterprise editions support online updates and advanced indices (IVF, HNSW).

---

## 🔁 Deterministic HealingIntent Serialization

Every `HealingIntent` is cryptographically signed (when enforcement is enabled) and serialised to JSON with a deterministic field order. The deterministic ID is computed as:

\[
\text{id} = \text{SHA256}(\text{intent\_type} \| \text{component} \| \text{parameters\_canonical} \| \text{timestamp\_floor\_sec})
\]

This guarantees that repeated evaluations with the same inputs produce the same ID, enabling deduplication and replay auditing.

---

## 🚦 Wilson Confidence Gate for Model Promotion

When a new HMC model is trained on historical data, it is **shadow‑deployed** for a probation period. The Wilson lower bound is computed daily; only when the bound exceeds `0.99999` (99.999% confidence) is the model promoted to production. This prevents regressions and ensures high‑confidence deployments.

---

## 🧪 Epistemic Uncertainty – CUDL Shapley Attribution

The **CUDL** (Causal Uncertainty Decomposition Layer) computes Shapley values for each uncertainty source:

\[
\phi_i = \sum_{S \subseteq U \setminus \{i\}} \frac{|S|!(|U|-|S|-1)!}{|U|!}\bigl[ \psi(S \cup \{i\}) - \psi(S) \bigr]
\]

Where \(U = \{\text{hallucination}, \text{forecast\_uncertainty}, \text{data\_sparsity}\}\). This provides a breakdown of how much each factor contributes to the overall epistemic uncertainty \( \psi \). The results are included in the `metadata` of the `HealingIntent`.

---

## 🛡️ Deterministic Policy Algebra – Formal Guarantees

The policy language forms a Boolean algebra with evaluation homomorphism:

\[
\begin{aligned}
f(p \land q) &= f(p) \cup f(q) \\
f(p \lor q) &= f(p) \cap f(q) \\
f(\neg p) &= \overline{f(p)}
\end{aligned}
\]

Where \(f(p)\) returns the set of violation strings (empty = allowed). This ensures that policies are **composable, reversible, and auditable**. The Rust‑backed enforcer (enterprise) provides a verified implementation that shadows the Python evaluator for divergence detection.

---

## ⚡ Performance Characteristics

| Operation | Typical latency (p99) | Throughput |
|-----------|----------------------|-------------|
| Risk evaluation (conjugate only) | < 5 ms | > 2000 req/s |
| Risk evaluation (conjugate + HMC) | < 20 ms | > 500 req/s |
| Epistemic uncertainty (with probe) | < 50 ms | > 200 req/s |
| Semantic memory retrieval (k=5) | < 30 ms | > 300 req/s |

All numbers are on a 2‑core, 8GB instance. Scaling is linear with CPU cores. Enterprise deployments can achieve 10× higher throughput.

---

## 🔐 Auditable Logging & Forensics

Every governance decision produces a structured log entry containing:

- `timestamp` (UTC, nanosecond precision)
- `intent_id` (deterministic)
- `risk_score`, `variance`, `weights`
- `expected_losses` (approve, deny, escalate)
- `selected_action`
- `epistemic_breakdown` (hallucination, forecast, sparsity)
- `policy_violations` (list)
- `user` (if available)

Logs are written to a **write‑once, read‑many** (WORM) storage (enterprise). In OSS, they are rotated daily with a 30‑day retention.

---

## 📁 Repository Structure (Private vs Public)

| Repository | Visibility | Purpose |
|------------|------------|---------|
| `agentic_reliability_framework` | Private | Core engine (Bayesian, governance, memory) |
| `arf-api` | Private | FastAPI control plane |
| `arf-gateway` | Private | Go‑based auth & routing gateway |
| `enterprise` | Private | Rust enforcement, audit, policy algebra |
| `research` | Private | ECLIPSE hallucination probe, CUDL |
| `arf-bayesian-pricing-calculator` | Private | Pricing engine with MCMC |
| `arf-spec` | Public | Specification (shared under written terms) |
| `arf-frontend` | Public | Demo dashboard (mock data) |
| `pitch-deck` | Public | Public overview |

---

## 🧰 Development Environment (Pilots Only)

Qualified pilots receive access to:

- Private PyPI repository for the core engine (`pip install arf-core`)
- Docker images of the full stack (control plane + gateway)
- Terraform modules for AWS/Azure/GCP deployment
- Sample client libraries in Python, Go, TypeScript
- 30‑day free trial with 1,000 advisory evaluations / month

---

## 📚 Further Reading (Internal, Access‑Controlled)

- **White paper:** “Bayesian Governance for AI Infrastructure” (v4.2, shared under NDA)
- **Security architecture review** (available upon pilot agreement)
- **Compliance mapping** (SOC2, ISO27001, GDPR – evidence package)
- **Performance benchmark report** (10‑node cluster, 10k req/s)

Request via `juan@arf-ai.com`.

---
