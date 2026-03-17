<p align="center">
  <img src="../assets/ARF%20-%20Primary%20Logo.png" alt="ARF Primary Logo" width="220" />
</p>

<p align="center">
  <img src="../assets/ARF%20-%20Transparent%20Primary%20Logo.png" alt="ARF Transparent Logo" width="220" />
</p>

<p align="center">
  <strong>Agentic Reliability Framework (ARF)</strong><br/>
  Auditable cloud governance powered by Bayesian intelligence.
</p>

<p align="center">
  <a href="https://arf-frontend-sandy.vercel.app/">Dashboard</a> ·
  <a href="https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-v4">OSS Demo</a> ·
  <a href="https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-API">API Demo</a> ·
  <a href="https://arf-foundation.github.io/arf-spec/">Specification</a> ·
  <a href="https://huggingface.co/A-R-F">Hugging Face</a>
</p>

---

## What ARF is

ARF is an open-source framework for reliable, observable, and self-healing AI systems. It combines probabilistic reasoning, governance logic, semantic memory, and deterministic decision thresholds to support auditable infrastructure decisions.

## What we build

- **OSS Engine**  
  Core Bayesian models, memory, and governance loop.

- **API Control Plane**  
  FastAPI service exposing the framework for integrations and custom workflows.

- **Frontend UI**  
  Next.js dashboard for visualizing risk, decisions, history, and system health.

- **Specification Layer**  
  Canonical design for data models, decision rules, and API contracts.

- **Research**  
  Mathematical foundations of hybrid Bayesian inference, semantic memory, and reliability analysis.

## Key capabilities

- **Bayesian Risk Scoring**  
  Conjugate priors plus HMC for calibrated uncertainty.

- **Semantic Memory**  
  FAISS-based retrieval of similar past incidents.

- **Deterministic Probability Thresholds**  
  Approve, escalate, or deny using clear thresholds: 0.2 / 0.8.

- **Multi-Agent Orchestration**  
  Anomaly detection, root cause analysis, and forecasting.

## Ecosystem overview

| Module | Purpose | Link |
|---|---|---|
| OSS Engine | Core Bayesian models, memory, and governance loop | [agentic-reliability-framework](https://github.com/arf-foundation/agentic-reliability-framework) |
| API Control Plane | FastAPI service exposing the framework | [arf-api](https://github.com/arf-foundation/arf-api) |
| Frontend UI | Real-time governance dashboard | [arf-frontend](https://github.com/arf-foundation/arf-frontend) |
| ARF Spec | Canonical specification and design | [arf-spec](https://arf-foundation.github.io/arf-spec/) |
| Public Research | Experimental work and reliability studies | [research](https://github.com/arf-foundation/research) |

## Live demos

**OSS Demo**  
Interactive risk dashboard and governance control plane:  
https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-v4

**API Demo**  
Backend API for evaluation and governance workflows:  
https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-API

**Frontend Dashboard**  
Real-time visual interface for ARF:  
https://arf-frontend-sandy.vercel.app/

## Mathematical foundations

| Concept | Implementation |
|---|---|
| Conjugate Priors | Per-category Beta priors updated online with outcomes |
| HMC Sampling | Logistic regression with NUTS, serialized for hot-loading |
| Risk Fusion | Weighted combination of online, hyperprior, and HMC estimates |
| DPT | Approve if P(failure) < 0.2, deny if > 0.8, otherwise escalate |

## Contributing

We welcome contributions from developers, researchers, and practitioners.

1. Fork a repository
2. Make your changes
3. Submit a pull request
4. Open issues or discussions for feedback

## Contact

- Email: petter2025us@outlook.com
- LinkedIn: https://www.linkedin.com/in/petterjuan/
- Calendly: https://calendly.com/petter2025us/30min

---

© 2026 ARF Foundation · Open source under Apache 2.0
