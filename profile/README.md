# Agentic Reliability Framework (ARF) 👋

<img src="assets/ARF%20-%20Primary%20Logo.png" alt="ARF Logo" width="200"/>
<img src="assets/ARF%20-%20Transparent%20Primary%20Logo.png" alt="ARF Transparent Logo" width="200"/>

Auditable cloud governance powered by **Bayesian intelligence**. Build reliable, observable, and self-healing AI systems for real-world infrastructure.

Live Dashboard: [ARF Dashboard](https://arf-frontend-sandy.vercel.app/)  

---

## 🌟 Our Vision
- Enable **provably safe AI operations** in cloud and hybrid environments.
- Provide **open-source advisory engines** that are mathematically rigorous and auditable.
- Foster a **community of AI engineers, researchers, and cloud practitioners** building the next generation of reliable AI systems.

---

## 📌 Pinned Repositories

| Repository | Description | Language |
|------------|-------------|---------|
| [agentic_reliability_framework](https://github.com/arf-foundation/agentic-reliability-framework) | OSS advisory engine with deterministic probability thresholding & hybrid Bayesian inference | Python |
| [arf-api](https://github.com/arf-foundation/arf-api) | FastAPI-based control plane for ARF, providing cloud governance APIs | Python |
| [arf-frontend](https://github.com/arf-foundation/arf-frontend) | Interactive UI for visualizing ARF decisions, risk scores, and multi-agent simulations | TypeScript |
| [arf-spec](https://github.com/arf-foundation/arf-spec) | Formal specification of ARF data models, decision rules, and API contracts | Markdown |
| [research](https://github.com/arf-foundation/research) | Experimental research projects, including hallucination detection & vector memory studies | Python |
| [Start-ups](https://github.com/arf-foundation/Start-ups) | Pilot projects, early ecosystem experiments, and client demos | Various |

---

## 🚀 Ecosystem Overview

| Module | Purpose | Link |
|--------|---------|------|
| **OSS Engine** | Core Bayesian models, memory, and governance loop | [Engine Repo](https://github.com/arf-foundation/agentic-reliability-framework) |
| **API Control Plane** | FastAPI service exposing the framework | [API Repo](https://github.com/arf-foundation/arf-api) |
| **Frontend UI** | Next.js dashboard for visualizing risk and multi-agent simulations | [Frontend Repo](https://github.com/arf-foundation/arf-frontend) |
| **Research** | Mathematical foundations of hybrid Bayesian inference | [Research Repo](https://github.com/arf-foundation/research) |
| **Enterprise** | Advanced compliance, audit trails, and support | Contact for details |

---

## 🧠 Key Capabilities

- **Bayesian Risk Scoring**: Conjugate priors + HMC for calibrated uncertainty.
- **Semantic Memory**: FAISS-based retrieval of similar past incidents.
- **Deterministic Probability Thresholds (DPT)**: Approve/Deny/Escalate decisions (0.2 / 0.8).
- **Multi-Agent Orchestration**: Anomaly detection, root cause analysis, forecasting.

---

## 📊 Mathematical Insights

| Concept | Implementation |
|---------|----------------|
| Conjugate Priors | Per-category Beta priors, updated online with outcomes |
| HMC Sampling | Logistic regression with NUTS, serialized to JSON for hot-loading |
| Risk Fusion | Weighted combination of conjugate, hyperprior, and HMC estimates |
| DPT Thresholds | Approve if P(failure) < 0.2, Deny if > 0.8, otherwise Escalate |

---

## 🎮 Live Demos

- **OSS Demo**: [v4 Hugging Face Space](https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-v4) – Interactive Bayesian risk dashboard.
- **API Demo**: [v4 API](https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-API)

**Example API call:**

```bash
curl -X POST https://huggingface.co/spaces/A-R-F/Agentic-Reliability-Framework-API/api/v1/incidents/evaluate
```

*   **Frontend Dashboard**: [ARF Dashboard](https://arf-frontend-sandy.vercel.app/) – Real-time governance visuals.
    

🧑‍💻 Contributing
------------------

We welcome contributions from developers, researchers, and enthusiasts. To get involved:

1.  Fork any repository, make your changes, and submit a pull request.
    
2.  Report issues or feature requests in the Discussions tab.
    
3.  Follow our Contribution Guidelines.
    

**License**: Apache 2.0

📬 Contact
----------

*   Email: petter2025us@outlook.com
    
*   LinkedIn: Juan Petter
    
*   Book a 30-min call: [Calendly](https://calendly.com/)
    

Join us to make ARF the **standard for reliable AI operations**.

© 2026 ARF Foundation – Open source (Apache 2.0)Documentation: [ARF Spec](https://arf-foundation.github.io/arf-spec/)

