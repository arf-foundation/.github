# Agentic Reliability Framework (ARF) – Stewarded Governance for AI Systems

<img src="https://raw.githubusercontent.com/arf-foundation/.github/main/assets/ARF%20-%20Primary%20Logo.png" alt="ARF Logo" width="200"/>

**Auditable cloud governance powered by Bayesian intelligence.** Build reliable, observable, and self‑healing AI systems for real‑world infrastructure.

🔐 **The core ARF engine is access‑controlled and not open source.**  
It is available only to qualified pilots and enterprise customers under **outcome‑based pricing**.

👉 [ARF Control Center (public demo UI)](https://arf-frontend-sandy.vercel.app/)

---

## 🎯 Our Mission

ARF makes AI operations **provably safe, auditable, and transparent**.  
We provide a **mathematically rigorous governance layer** for deterministic and probabilistic decision‑making in production AI systems.

- ✅ Enable **provably safe AI operations** in cloud, hybrid, and multi‑agent environments.
- 🧮 Deliver **expected loss minimisation** and **hybrid Bayesian inference** for calibrated risk scoring.
- 🔍 Offer **full traceability** through auditable logs, semantic memory, and transparent decision records.
- 🧭 **Steward the framework** – not a free‑for‑all, but a protected, pilot‑first product.

---

## 📌 Pinned Repositories (Public Only)

| Repository | Description | Language |
|------------|-------------|----------|
| [arf-spec](https://github.com/arf-foundation/arf-spec) | Canonical specification: data models, decision rules, and API contracts | Markdown |
| [arf-frontend](https://github.com/arf-foundation/arf-frontend) | Next.js dashboard (public demo UI – uses mock data) | TypeScript |
| [pitch-deck](https://github.com/arf-foundation/pitch-deck) | Public overview and vision | HTML |

> 🔒 **Private repositories** (core engine, API control plane, enterprise code) are **not listed here**. Access is restricted to pilots and enterprise customers.

---

## 🚀 Ecosystem Overview (Public vs. Protected)

| Module | Purpose | Access |
|--------|---------|--------|
| **Public Specification** (`arf-spec`) | Data models, API contracts, decision rules | ✅ Public (Apache 2.0) |
| **Public Demo UI** (`arf-frontend`) | Dashboard with mock data, showcases concepts | ✅ Public (Apache 2.0) |
| **Protected Core Engine** | Bayesian risk scoring, semantic memory, governance loop | 🔒 Pilot / Enterprise only |
| **Protected API Control Plane** | FastAPI service exposing live endpoints | 🔒 Pilot / Enterprise only |
| **Enterprise Extensions** | Advanced compliance, audit trails, outcome‑based pricing | 🔒 Enterprise only |

---

## 🧠 Key Capabilities (Conceptual Overview)

- **Bayesian Risk Scoring** – Conjugate priors + HMC for calibrated uncertainty.
- **Semantic Memory** – FAISS‑based retrieval of similar past incidents.
- **Expected Loss Minimisation** – Chooses approve/deny/escalate by balancing risk, cost, and uncertainty.
- **Multi‑Agent Orchestration** – Automated anomaly detection, root cause analysis, forecasting.
- **Policy Composability** – AND/OR/NOT combinators for complex rules.
- **Traceability & Audit** – Every decision is fully auditable and queryable.

> ⚠️ These capabilities are implemented in the **protected core engine**, not in public demo assets.

---

## 🎮 Live Demos (Sanitised / Mock Data)

- **UI Concept Demo** – [Hugging Face Space](https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-v4) – Interactive risk dashboard (mock data only).
- **Sandbox API** – [Mock endpoint on Hugging Face](https://huggingface.co/spaces/A-R-F/ARF-Sandbox-API) – Returns mock responses, not real Bayesian inference. Interactive docs at `/docs`.

**Example sandbox call (returns mock data):**

```bash
curl -X POST https://a-r-f-arf-sandbox-api.hf.space/v1/evaluate \
  -H "Content-Type: application/json" \
  -d '{"service_name":"api","event_type":"latency","severity":"high"}'
```

The real engine is **not publicly accessible**.

## 🧑‍💻 Contributing (Public Repositories Only)

We accept **limited contributions** to public repositories (`arf-spec`, `arf-frontend`, `pitch-deck`) – bug fixes, documentation, demo improvements.  
**We do not accept pull requests against private core repositories.**

1. Open an issue describing your proposed change.
2. Wait for a maintainer to assign the issue.
3. Sign a Contributor License Agreement (CLA) if requested.
4. Submit a pull request referencing the issue.

All changes are reviewed and merged at the founder’s discretion.

For questions about the protected engine or pilot access, please **do not open issues** – use the contact details below.

---

## 📬 Pilot Access & Contact

The core ARF engine is **not open source**. To request pilot access (time‑limited free trial) or enterprise licensing, contact us directly:

| Method | Details |
|--------|---------|
| **Email** | petter2025us@outlook.com |
| **LinkedIn** | [Juan Petter](https://www.linkedin.com/in/petterjuan/) |
| **Book a Call** | [30‑Min Consultation](https://calendly.com/petter2025us/30min) |

**When requesting access, please provide:**  
- Your full name and organisation  
- Use case description  
- Expected monthly incident volume  
- Cloud environment (AWS, Azure, GCP, on‑prem)

---

## 📜 License & Legal

- **Public repositories** (`arf-spec`, `arf-frontend`, `pitch-deck`) are licensed under **Apache 2.0**.
- **The core engine and all private repositories are proprietary** – no license is granted for public use.
- See the [NOTICE](https://github.com/arf-foundation/.github/blob/main/NOTICE) file for full details.

> All modules, dashboards, and APIs that are **public** are open source (Apache 2.0).  
> The **core Bayesian engine** is **not** open source – it is protected and access‑controlled.

---

*Stewarded by the founder – pilot‑first, outcome‑based pricing.*
