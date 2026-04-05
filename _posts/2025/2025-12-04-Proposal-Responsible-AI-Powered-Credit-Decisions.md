---
title: "Proposal for Responsible AI-Powered Credit Deicisions"
date: 2025-12-04
tags: [AI Governance, Academic Papers]
dropbox_url: https://www.dropbox.com/scl/fi/ox78te3m5b3i3sijkmwxr/Brief-Draft-Proposal-for-Responsible-AI-Credit-Decisions.pdf?rlkey=kisqm7tildebdyt40bpz7hpmk&st=ss89yswx&dl=0
---
*Note: This is a project I completed for Purdue's [AI Management and Policy Master's Program ](https://www.purdue.edu/online/artificial-intelligence/ai-management-and-policy/){:target="_blank"}. The data and business scenarios are part of a simulated case study and do not represent the actual operations of any real-world entity.*

## Executive Summary
Ficus Bank (Ficus) faces a pivotal choice: continue with manual underwriting processes that are increasingly slow and exclusionary or transition to an AI-driven model. While AI offers a path to rapid decisioning and broader financial inclusion, it introduces risks regarding algorithmic bias and transparency. This proposal recommends integrating the **NIST AI Risk Management Framework (AI RMF)** to ensure that Ficus’s modernization is both compliant with emerging state laws (like the Colorado AI Act) and aligned with the bank’s core values of equity and security.

## Introduction
Ficus Bank has long been an economic anchor for its community. However, a recent surge in small business loan applications has strained manual underwriting, creating bottlenecks and frustrating customers. Furthermore, traditional credit metrics often exclude creditworthy "nontraditional" businesses.

To stay competitive, Ficus plans to replace manual workflows with machine-learning-based underwriting. By considering alternative data—such as rental histories, utility payments, and employment records—the bank can reduce decision times from days to minutes. However, moving from human logic to "black box" algorithms requires a fundamental shift in risk management.

## The Risks of AI Credit Decisioning

### 1. The Alignment Problem
Ficus must ensure the AI system balances efficiency with ethics. The project must:
* **Reduce** decision times while **maintaining** or reducing default rates.
* **Increase** approval rates for nontraditional businesses.
* **Comply** with all state and federal fair lending laws.

### 2. Algorithmic Bias & Proxy Variables
Unlike traditional software, AI is *trained*, not programmed. It can internalize historical socio-economic disparities. Even without explicit "race" or "gender" data, the model may use **proxy variables** (e.g., zip codes or specific shopping habits) to infer protected characteristics.

> **Data Insight: Existing Disparities in Lending**
> Current data from the Federal Reserve's Small Business Credit Survey (2024/2025) highlights why manual processes often fail:
> * **Black-owned firms** are approved for the full amount of credit they seek only **28%** of the time.
> * **White-owned firms** see a much higher full-approval rate of **54%**.
> * **Hispanic-owned firms** fall in between at approximately **31%**.
> AI aims to bridge this gap, but without rigorous oversight, it risks automating and scaling these very inequities.

### 3. The “Black Box” Problem
"Deep" machine learning models encode millions of relationships, often making it impossible for humans to see *why* a specific decision was made. This opacity makes it difficult to provide the "adverse action" reasons required by the **Equal Credit Opportunity Act (ECOA)**.

## Compliance in an Evolving Policy Landscape

Ficus operates in a shifting regulatory environment where federal and state requirements are increasingly divergent.

* **Federal Policy:** Recent shifts, including **Executive Order 14179 (2025)**, prioritize American AI leadership by reducing regulatory burdens. However, the **Consumer Financial Protection Bureau (CFPB)** remains clear: using a "black box" does not exempt a bank from explaining credit denials.
* **State Policy:** States are filling the federal vacuum. The **Colorado AI Act (SB 24-205)**, effective June 30, 2026, mandates that credit decisioning systems undergo annual impact assessments and provide consumers with options to appeal AI-generated decisions.

## Policy Options

| Option | Strategy | Advantages | Tradeoffs |
| :--- | :--- | :--- | :--- |
| **1** | **Avoid the Risk** | No AI-specific compliance costs. | High long-term strategic risk; loss of market share to Fintechs. |
| **2** | **Targeted Compliance** | Low upfront cost; uses existing ERM. | "Tick-box" approach; high risk of reputational damage. |
| **3** | **Integrate NIST AI RMF** | Strong compliance; future-proofed. | High upfront investment in governance. |

## Recommendations: Integrating the NIST AI RMF

We recommend **Option 3**. To implement this, Ficus should act across the four NIST pillars:

1.  **Govern:** Establish a cross-functional **AI Governance Committee** (Legal, Risk, IT) to align AI use with bank values.
2.  **Map:** Conduct a **Governance Gap Analysis** to identify where legacy risk structures fail to address data provenance and model lineage.
3.  **Measure:** Perform a **Pre-deployment Impact Assessment** to document training data and identify proxy discrimination before it hits the market.
4.  **Manage:** Define **Explainability Solutions**, using interpretable machine learning tools to ensure Ficus can always provide specific reasons for loan denials.

## Conclusion
AI underwriting is an operational necessity, but it cannot be deployed through legacy governance. By adopting the **NIST AI Risk Management Framework**, Ficus Bank can solve its operational bottlenecks and expand financial inclusion while securing its reputation as a leader in responsible, secure innovation.

---

## References
* **American Bankers Association. (2024).** Letter to the Treasury on artificial intelligence.
* **Blueprint for an AI Bill of Rights. (2022).** The White House.
* **Boncella, R. (2024).** AI and management: Navigating the alignment problem. *Issues In Information Systems, 25*(4).
* **Consumer Financial Protection Bureau. (2024).** Circular 2022-03: Adverse action notification requirements.
* **Colorado Senate Bill 24-205. (2024).** Consumer Protections for Artificial Intelligence.
* **Dastin, J. (2018).** Amazon scraps secret AI recruiting tool. *Reuters*.
* **Executive Order 14179. (2025).** Removing barriers to American leadership in AI. *90 Fed. Reg. 2172*.
* **Tabassi, E. (2023).** NIST AI Risk Management Framework (AI RMF 1.0).