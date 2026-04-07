---
title: "AI Risk Impact Assessment Proposal: Biometric Identity Verification"
date: 2026-03-01
tags: [AI Governance, Academic Papers]
---
> *Note: This is a project I completed for Purdue's [AI Management and Policy Master's Program ](https://www.purdue.edu/online/artificial-intelligence/ai-management-and-policy/){:target="_blank"}. The data and business scenarios are part of a simulated case study and do not represent the actual operations of any real-world entity.*

---

## Executive Summary
This proposal recommends the bank implement an **AI-powered biometric identity verification system** utilizing “selfies” to block transactions initiated by fraudsters. Since this technology involves an autonomous AI system and introduces novel customer interactions, the bank should conduct an **AI risk impact assessment** during the planning and design stage to address legal, ethical, and reputational risks. 

By integrating the **National Institute of Standards and Technology (NIST)** AI Risk Management Framework's **Map function** with existing Enterprise Risk Management (ERM) procedures, relevant stakeholders will evaluate the technology for fairness, security, and regulatory alignment (**SR 11-7**), while proactively consulting regulators and customers.

---

## AI-Powered Biometric Identity Verification for Fraud Prevention
As sophisticated fraud schemes escalate, banks face significant losses (Experian, 2026; Kadyshevitch, 2024). To address this, I propose incorporating an AI-powered biometric verification system utilizing **facial recognition and liveness detection**. 

* **Process:** When a customer attempts a high-risk action (e.g., transferring large funds), the app prompts for a live, on-screen selfie.
* **Mechanism:** The AI compares this against registered IDs, analyzing depth, texture, and micro-movements to confirm physical presence.
* **Outcome:** Transactions initiated by imposters are automatically rejected (Yu et al., 2022).

**System Limitations:** While compelling, limitations include potential demographic bias (Buolamwini & Gebru, 2018), degraded accuracy in poor lighting, and an inability to prevent scams where customers initiate transfers themselves. These factors necessitate a formal risk assessment.

---

## Business Case for an AI Risk Impact Assessment
A rigorous assessment prior to deployment ensures the system does not introduce unintended negative consequences:

* **Algorithmic Bias:** Systems may disproportionately flag certain demographics, leading to legal and reputational harm.
* **Privacy Repercussions:** Failures in processing sensitive biometric data could be devastating (Moharrak & Mogaji, 2025).
* **Psychological Factors:** Customers may opt out due to privacy discomfort, while others may become over-reliant on the AI and decrease their own vigilance (Barlas et al., 2020; Rahmati, 2025).

---

## Assess Risks Early in the AI Governance Lifecycle
This assessment should be completed during the **planning and design stage**. Early completion allows the bank to engage key risk departments—Legal, Compliance, Third-Party Risk, Model Risk Management (MRM), and InfoSec—to establish mitigation guardrails before finalizing vendor selection. The bank will also continuously monitor and reassess performance post-deployment.

---

## Risk Impact Assessment Framework
To address unique AI risks, the framework combines existing procedures with the **NIST AI Risk Management Framework’s Map function**:

1.  **Algorithmic Analysis:** MRM will ensure **Federal Reserve SR 11-7** compliance by evaluating fairness, transparency, and reliability.
2.  **Risk-Based Assessment:** Aligned with the NIST Map function, drawing on expertise from Legal, Compliance, InfoSec, and Business Units.

---

## Roles and Responsibilities

* **Fraud Manager:** Product owner; responsible for deployment and maintenance.
* **Chief Risk Officer:** Accountable for the risk assessment and resulting mitigations.
* **MRM Manager:** Responsible for the algorithmic assessment per SR 11-7 guidelines.
* **Compliance, General Counsel, CISO, & TPRM:** Responsible for assessing risks related to their respective areas based on their existing procedures and NIST guidance.
* **Vendor:** Developer providing system documentation for assessment.
* **Customers (End Users):** Engaged via focus groups to assess concerns.
* **The Federal Reserve:** Primary regulator providing supervisory guidance.

---

## Relevant Legal and Industry Standards
The deployment must comply with overlapping financial and data privacy regulations:

* **Federal Reserve SR 11-7:** Mandates independent validation for conceptual soundness, reliability, and lack of bias.
* **Interagency Guidance on Third-Party Relationships:** Requires assessment of vendor security and resilience.
* **Gramm-Leach-Bliley Act (GLBA):** Requires consent, data minimization, and strict retention schedules to protect non-public personal information.

---

## Stakeholder Engagement Strategy
* **Internal:** Layman’s-terms training and Q&A forums for non-technical units.
* **External:** Proactive briefings with primary regulators; consultations with consumer advocacy and digital accessibility experts.
* **Customers:** Focus groups and surveys to gauge openness and privacy concerns.

---

## Conclusion
Implementing biometric identity verification is a business necessity to counter escalating fraud. By executing a rigorous impact assessment early using the **NIST Map function**, the bank can roll out this technology safely. This proactive approach bolsters the bank’s reputation for responsibility, security, and innovation.

---

## References

**Barlas, Y., Basar, O. E., Akan, Y., Isbilen, M., Alptekin, G. I., & Incel, O. D. (2020).** DAKOTA: Continuous authentication with behavioral biometrics in a mobile banking application. *2020 5th International Conference on Computer Science and Engineering (UBMK)*, 1–6. https://doi.org/10.1109/UBMK50275.2020.9219365

**Board of Governors of the Federal Reserve System. (2011).** *SR 11-7: Guidance on model risk management.* https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm

**Board of Governors of the Federal Reserve System, Federal Deposit Insurance Corporation, & Office of the Comptroller of the Currency. (2023).** Interagency guidance on third-party relationships: Risk management. *Federal Register, 88*(111), 37920–37937. https://www.federalregister.gov/documents/2023/06/09/2023-12340/interagency-guidance-on-third-party-relationships-risk-management

**Buolamwini, J., & Gebru, T. (2018).** Gender shades: Intersectional accuracy disparities in commercial gender classification. *Proceedings of Machine Learning Research, 81*, 1–15. http://proceedings.mlr.press/v81/buolamwini18a.html

**Experian. (2026).** *2026 future of fraud forecast: Insights into the next wave of AI-driven fraud.* https://www.experian.com/thought-leadership/business/2026-future-of-fraud-forecast-infographic

**Gramm-Leach-Bliley Act, 15 U.S.C. § 6801 et seq. (1999).** https://www.govinfo.gov/app/details/PLAW-106publ102

**Kadyshevitch, D. (2024).** Generative AI has democratised fraud and cybercrime. *Computer Fraud & Security.* https://doi.org/10.12968/s1361-3723(24)70018-9

**Lagasio, V., Mercuri, D., Pirillo, J., & Belloli, M. (2025).** Integrating generative AI and large language models in financial sector risk management: Regulatory frameworks and practical applications. *Risk Management Magazine, 20*(1), 30–48. https://doi.org/10.47473/2020rmm0150

**Moharrak, M., & Mogaji, E. (2025).** Generative AI in banking: Empirical insights on integration, challenges and opportunities in a regulated industry. *International Journal of Bank Marketing, 43*(4), 871–896. https://doi.org/10.1108/IJBM-08-2024-0490

**National Institute of Standards and Technology. (2023).** *Artificial intelligence risk management framework (AI RMF 1.0)* (NIST AI 100-1). U.S. Department of Commerce. https://doi.org/10.6028/NIST.AI.100-1

**Okpala, I., Golgoon, A., & Kannan, A. R. (2025).** *Agentic AI systems applied to tasks in financial services: Modeling and model risk management crews.* arXiv. https://doi.org/10.48550/arXiv.2502.05439

**Rahmati, M. (2025).** Real-time financial fraud detection using adaptive graph neural networks and federated learning. *International Journal of Management and Data Analytics.* https://doi.org/10.5281/zenodo.15107110

**Yu, Z., Qin, C., Zhao, C., Li, X., & Zhao, G. (2022).** Deep learning for face anti-spoofing: A survey. *IEEE Transactions on Pattern Analysis and Machine Intelligence, 45*(7), 8609–8631. https://doi.org/10.1109/TPAMI.2022.3215850