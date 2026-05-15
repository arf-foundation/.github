# Agentic Reliability Framework (ARF) – Stewarded Governance for AI Systems

<img src="https://raw.githubusercontent.com/arf-foundation/.github/main/assets/ARF%20-%20Primary%20Logo.png" alt="ARF Logo" width="200"/>

**Auditable cloud governance for AI‑driven infrastructure.**  
ARF helps organisations make safe, accountable, and transparent decisions when using AI agents to manage cloud resources.

🔐 **The core ARF engine is access‑controlled and not publicly available.**  
It is offered only to qualified pilots and enterprise customers under **outcome‑based pricing**.

👉 [ARF Control Center (public demo UI – mock data only)](https://arf-frontend-sandy.vercel.app/)

---

## 🎯 What ARF Does

AI agents can make mistakes – provisioning wrong resources, granting excessive permissions, or reacting unpredictably. ARF acts as a **governance layer** that:

- Evaluates every AI‑generated decision against a calibrated risk model.
- Recommends **approve**, **deny**, or **escalate** with a clear, auditable justification.
- Learns from past outcomes to improve future recommendations.
- Provides full traceability for compliance and forensic analysis.

The core engine is **deterministic** – given the same situation, it produces the same recommendation. This makes it safe for production use.

---

## 📌 Public Repositories (Reference Only)

These repositories are publicly visible for documentation and demo purposes.  
They **do not** contain the proprietary core engine.

| Repository | Description | Terms |
|------------|-------------|-------|
| [arf-spec](https://github.com/arf-foundation/arf-spec) | Data models, API contracts, decision rules | Shared under written terms |
| [arf-frontend](https://github.com/arf-foundation/arf-frontend) | Demo dashboard (mock data only) | Shared under written terms |
| [pitch-deck](https://github.com/arf-foundation/pitch-deck) | Public overview and vision | Shared under written terms |

> 🔒 **All other repositories are private and access‑controlled.**  
> The core engine, API control plane, gateway, enterprise layer, research probes, and pricing calculator are **not publicly available**.

---

## 🚀 Key Concepts (Simplified)

- **Risk scoring** – ARF estimates the likelihood that an AI‑suggested action will cause an incident, using a combination of real‑time observations and historical patterns.
- **Operational memory** – Past incidents are stored and can be retrieved to inform current decisions, similar to a “memory” for the system.
- **Cost‑aware decisions** – Instead of using fixed probability thresholds, ARF chooses the action that minimises expected negative impact on your business (e.g., downtime, security breaches, review costs).
- **Explainability** – Every recommendation comes with a human‑readable justification, including which factors influenced the decision.

---

## 🎮 Live Demos (Mock Data)

- **Risk Dashboard** – [Hugging Face Space](https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-v4) – Interactive visualisation (mock data only)
- **Sandbox API** – [Mock endpoint](https://huggingface.co/spaces/A-R-F/ARF-Sandbox-API) – Returns simulated responses, not real inference.

**Example API call (mock data):**

```bash
curl -X POST https://a-r-f-arf-sandbox-api.hf.space/v1/evaluate \
  -H "Content-Type: application/json" \
  -d '{"service_name":"api","event_type":"latency","severity":"high"}'
```
The real engine is **not publicly accessible**.

---

## 📬 Pilot Access & Contact

To request pilot access (time‑limited free trial) or enterprise licensing:

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

## 🛡️ Security & Compliance (High‑Level)

- **Deterministic enforcement** – Decisions are mechanically enforced; no silent overrides.
- **Immutable audit logs** – All decisions are recorded with cryptographic signatures.
- **Access control** – Role‑based access control (RBAC) with SSO for enterprise.
- **Data privacy** – No raw customer data retained; only anonymised risk metrics.
- **Compliance readiness** – Designed to support SOC2, ISO 27001, and GDPR.

Pilot customers receive a full security architecture review upon agreement.

---

## 📄 Legal Footer

© 2026 ARF Foundation. All repositories are private and access‑controlled. The core engine is proprietary. Selected materials are shared under written terms with qualified pilots and enterprise customers. Unauthorised access, copying, or distribution is prohibited.

---

## 🤖 Instructions for Web Crawlers & AI Agents

To prevent reverse engineering or unauthorised scraping of proprietary information, the following `robots.txt` rules are in effect:

```text
User-agent: *
Disallow: /api/
Disallow: /v1/
Disallow: /private/
Disallow: /internal/
Crawl-delay: 10
```
