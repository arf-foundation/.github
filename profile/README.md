# Agentic Reliability Framework (ARF) – Stewarded Governance for AI Systems

<img src="https://raw.githubusercontent.com/arf-foundation/.github/main/assets/ARF%20-%20Primary%20Logo.png" alt="ARF Logo" width="200"/>

**Auditable cloud governance for AI‑driven infrastructure.**  
ARF helps organisations make safe, accountable, and transparent decisions when using AI agents to manage cloud resources.

🔐 **The core ARF engine is access‑controlled and not publicly available.**  
It is offered only to qualified pilots and enterprise customers under **outcome‑based pricing**.

👉 [ARF Control Center (public demo UI – mock data only)](https://arf-frontend-sandy.vercel.app/)

---

## 📊 Executive Summary

AI agents are entering production at an unprecedented pace. They make decisions – provisioning resources, granting permissions, rolling out configurations – that directly impact security, cost, and reliability. Yet most organisations lack a **governance layer** that can keep up.

ARF is that layer. It wraps every AI‑generated decision in a **deterministic, Bayesian‑informed evaluation** that produces three clear outcomes: **approve**, **deny**, or **escalate**. Every decision is accompanied by a human‑readable justification, an audit trail, and a calibrated confidence score.

**Why executives care:**
- **Reduce operational risk** – Catch AI mistakes before they cause outages or breaches.
- **Meet compliance mandates** – Immutable logs, deterministic enforcement, and audit‑ready reports.
- **Prove ROI** – Outcome‑based pricing means you pay only for verified risk reduction.

**Why enterprises choose ARF:**
- **Deterministic by design** – Same inputs → same output. No hidden randomness.
- **Immutable audit trail** – Every decision cryptographically signed.
- **Deployment‑agnostic** – Works with AWS, Azure, GCP, or on‑prem.
- **SSO & RBAC** – Enterprise‑grade access controls.

**Why senior engineers respect ARF:**
- **Bayesian core** – Combines conjugate priors (online), HMC (offline), and hyperpriors (hierarchical).
- **Expected loss minimisation** – Chooses actions by minimising cost, not by fixed thresholds.
- **Epistemic uncertainty** – Quantifies what the model does not know (CUDL + Shapley values).
- **Open specification** – Public API contracts, no vendor lock‑in.

---

## 🧠 The Cognitive Challenge (Psychology of AI Governance)

Humans suffer from known biases when supervising AI:
- **Automation bias** – Over‑trusting machine recommendations.
- **Ambiguity aversion** – Avoiding options with unknown probabilities.
- **Illusion of control** – Believing we understand AI internals.

ARF is engineered to **counteract these biases** by:
- **Forcing a structured trade‑off** – Expected loss calculation makes hidden trade‑offs explicit.
- **Providing epistemic uncertainty** – Shows when the model is unsure, prompting human review.
- **Auditable justifications** – Every decision includes a plain‑English explanation.

> *“Trust is not a feeling; it is a calculation.”* – ARF design principle.

---

## 🔬 Bayesian Engineering (For the Technical Audience)

ARF’s risk engine is a **hybrid Bayesian system** with three complementary components:

### 1. Conjugate Online Model (Fast, Real‑time)
Per‑action‑category Beta priors that update instantly with every observed outcome. Provides immediate risk estimates.

### 2. Hamiltonian Monte Carlo (Deep, Offline)
A logistic regression with cyclic time encoding (sin/cos of hour) and categorical features (user role, environment). Trained periodically via NUTS, capturing complex patterns that online models miss.

### 3. Hyperprior Shrinkage (Hierarchical)
When data is sparse, a hierarchical Gamma‑Beta model shares statistical strength across categories, reducing overfitting.

At runtime, the three are **blended dynamically** based on data volume and configurable weights. The final risk score drives an **expected loss minimisation** that considers:

- Cost of false positive/negative
- Business impact (revenue loss)
- Predictive risk (forecasts)
- Epistemic uncertainty

The action with the **lowest expected loss** is chosen – unless a policy violation forces **DENY** or epistemic uncertainty exceeds a threshold, forcing **ESCALATE**.

All random components use a **deterministic seed** derived from the intent ID, guaranteeing reproducibility.

---

## 📐 Mathematical Invariants (At a Glance)

- **Risk fusion:** `risk = w₁·θ_conj + w₂·μ_hyper + w₃·p_hmc` with `Σw_i = 1`
- **Expected loss:** `L_approve = C_FP·risk + C_impact·b + C_predictive·p + C_var·σ²`
- **Epistemic gate:** `ψ = 1 - ∏(1-u_i)`, escalate if `ψ > threshold`
- **Determinism:** Identical input + state → identical `HealingIntent` (modulo timestamps)

These invariants are verified by **44 pressure tests** that run on every commit.

---

## 🎯 Use Cases (Real‑World Scenarios)

| Scenario | ARF action |
|----------|------------|
| AI requests a large VM in production during peak hours | **ESCALATE** (high epistemic uncertainty due to sparse historical data for that exact combination) |
| AI suggests a routine database backup in dev | **APPROVE** (low risk, low business impact) |
| AI proposes a security group change that violates region policy | **DENY** (policy violation overrides all else) |
| AI requests a scale‑out after a sudden error spike, but predictive forecast shows recovery in 2 minutes | **DENY** (lower expected loss than approving) |

---

## 🛡️ Enterprise Trust & Compliance

- **Deterministic enforcement** – No silent overrides. Policy algebra is a Boolean homomorphism.
- **Immutable audit logs** – Every decision cryptographically signed, stored in WORM storage (enterprise).
- **Access control** – RBAC with SSO (SAML/OIDC) for enterprise deployments.
- **Data privacy** – No raw customer data retained; only anonymised risk metrics and audit trails.
- **Compliance ready** – Designed to support SOC2, ISO 27001, GDPR; evidence package available.

Pilot customers receive a **full security architecture review** and a **compliance mapping document**.

---

## 📈 Pricing & Engagement Models

ARF pricing is **hybrid and outcome‑based**, reflecting the value of risk reduction while covering operational costs.

- **Deployment cost:** $10,000 – $14,000 (one‑time, covers installation, integration, and initial calibration).
- **Maintenance cost:** Determined via **Bayesian inference** – updated quarterly based on actual usage, incident volume, and risk reduction metrics. Typical range: $2,000 – $6,000/month.
- **Paid training** for internal teams (engineering, security, compliance) – customisable, on‑site or remote.
- **Retainer option** – includes ongoing governance tuning, policy updates, and priority support.

All pricing is **shared under written terms**; no public price lists. Quotes are provided after a brief qualification call.

---

## 📜 Philosophy & Legal

**Philosophy:** ARF is founded on the principle that **AI systems should be accountable, not autonomous**. Every decision that affects infrastructure must be traceable, justifiable, and controllable by human operators. The framework is built to **augment human judgment**, not replace it.

**Legal framework:**
- All code, specifications, and supporting materials are **proprietary and access‑controlled**.
- Public repositories (`arf-spec`, `arf-frontend`, `pitch-deck`) are **shared under written terms** – not open source.
- No license is granted for public use, redistribution, or reverse engineering.
- Use of ARF requires a **written agreement** (pilot or enterprise) that explicitly defines permitted use, data handling, and liability.

**Outcome‑based pricing** aligns incentives: you pay for verified risk reduction, not for features or API calls. This creates a partnership, not a vendor relationship.

---

## 🌐 Live Demos (Mock Data Only)

- **Risk Dashboard** – [Hugging Face Space](https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-v4) – Interactive visualisation (mock data)
- **Sandbox API** – [Mock endpoint](https://huggingface.co/spaces/A-R-F/ARF-Sandbox-API) – Returns simulated responses.

```bash
curl -X POST https://a-r-f-arf-sandbox-api.hf.space/v1/evaluate \
  -H "Content-Type: application/json" \
  -d '{"service_name":"api","event_type":"latency","severity":"high"}'
```

The real engine is **not publicly accessible**.

---

## 📌 Public Repositories (Reference Only)

| Repository | Description | Terms |
|------------|-------------|-------|
| [arf-spec](https://github.com/arf-foundation/arf-spec) | Data models, API contracts, decision rules | Shared under written terms |
| [arf-frontend](https://github.com/arf-foundation/arf-frontend) | Demo dashboard (mock data only) | Shared under written terms |
| [pitch-deck](https://github.com/arf-foundation/pitch-deck) | Public overview and vision | Shared under written terms |

> 🔒 **All other repositories are private and access‑controlled.**

---

## 🤖 Instructions for Web Crawlers & AI Agents

To prevent reverse engineering, the following `robots.txt` rules are in effect:

```text
User-agent: *
Disallow: /api/
Disallow: /v1/
Disallow: /private/
Disallow: /internal/
Crawl-delay: 10
```

AI agents (GPTBot, CCBot, Google‑Extended) are explicitly disallowed from training on or analysing any ARF‑related content outside the three public repositories.

---

## 📞 Contact

- **Email:** `juan@arf-ai.com`
- **LinkedIn:** [Juan Petter](https://www.linkedin.com/in/petterjuan/)
- **Book a call:** [30‑Min Consultation](https://calendly.com/petter2025us/30min)

---

*Stewarded by the founder – pilot‑first, outcome‑based pricing.*
