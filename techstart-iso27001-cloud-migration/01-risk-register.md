# ⚠️ Risk Register

> 5 risks identified during the ISO 27001 risk assessment for TechStart Inc's on-premises-to-AWS customer database migration.

| # | Title | Category | Status | Risk Score |
|---|---|---|---|---|
| 1 | Chatbot Application Security & Data Exposure Risk | Application Security | ![Open](https://img.shields.io/badge/status-Open-d73a49) | 16 — ![Critical](https://img.shields.io/badge/risk-Critical-b60205) |
| 2 | Database Server Security & Recovery Risk | Data Protection | ![Open](https://img.shields.io/badge/status-Open-d73a49) | 15 — ![Critical](https://img.shields.io/badge/risk-Critical-b60205) |
| 3 | Cloud Account Misconfiguration & Access Risk | Access Control | ![Open](https://img.shields.io/badge/status-Open-d73a49) | 16 — ![Critical](https://img.shields.io/badge/risk-Critical-b60205) |
| 4 | Network Device Resilience & Hardening Risk | Availability | ![Open](https://img.shields.io/badge/status-Open-d73a49) | 15 — ![Critical](https://img.shields.io/badge/risk-Critical-b60205) |
| 5 | Data Store (S3) Configuration & Availability Risk | Data Protection | ![Open](https://img.shields.io/badge/status-Open-d73a49) | 12 — ![High](https://img.shields.io/badge/risk-High-e36209) |

## 1. Chatbot Application Security & Data Exposure Risk

**Category:** Application Security &nbsp;·&nbsp; **Status:** ![Open](https://img.shields.io/badge/status-Open-d73a49)  
**Likelihood:** 4/5 &nbsp;·&nbsp; **Impact:** 4/5 &nbsp;·&nbsp; **Risk Score:** 16 (![Critical](https://img.shields.io/badge/risk-Critical-b60205))  
**Owner:** Augustine Ozor

**Description**  
Chatbot is exposed to prompt injection, potential leakage of customer PII, hallucinated or incorrect responses damaging trust, and unauthorized access to backend APIs. In staging, real customer data may be used for testing; in DR, the model or configuration can drift stale from production.

**Decision Rationale**  
Likelihood rated Likely (4) because prompt injection and hallucination are common, low-effort issues against public-facing LLM apps, and staging data reuse is a frequent shortcut. Impact rated Major (4) because PII leakage carries regulatory and reputational consequences, and unauthorized API access could expose backend systems beyond the chatbot itself.

---

## 2. Database Server Security & Recovery Risk

**Category:** Data Protection &nbsp;·&nbsp; **Status:** ![Open](https://img.shields.io/badge/status-Open-d73a49)  
**Likelihood:** 3/5 &nbsp;·&nbsp; **Impact:** 5/5 &nbsp;·&nbsp; **Risk Score:** 15 (![Critical](https://img.shields.io/badge/risk-Critical-b60205))  
**Owner:** John Ketson

**Description**  
Database faces SQL injection, unauthorized access or exfiltration, unpatched vulnerabilities, insufficient backup and recovery, and weak access controls. Staging copies unmasked production data for testing, and DR replication lag risks data loss on failover.

**Decision Rationale**  
Likelihood rated Possible (3) assuming baseline protections (parameterized queries, access controls) exist but backup testing and data masking are inconsistently enforced. Impact rated Severe (5) because the database holds critical transactional and customer data, and a breach, data loss, or failed recovery would directly affect business operations and compliance obligations.

---

## 3. Cloud Account Misconfiguration & Access Risk

**Category:** Access Control &nbsp;·&nbsp; **Status:** ![Open](https://img.shields.io/badge/status-Open-d73a49)  
**Likelihood:** 4/5 &nbsp;·&nbsp; **Impact:** 4/5 &nbsp;·&nbsp; **Risk Score:** 16 (![Critical](https://img.shields.io/badge/risk-Critical-b60205))  
**Owner:** Augustine Ozor

**Description**  
Cloud account is exposed to misconfigured IAM permissions, exposed credentials or keys, public-facing storage or services, lack of MFA, and cost or resource sprawl. Staging often carries overly permissive access for convenience, and the DR account risks falling out of sync, configuration drift, and untested failover.

**Decision Rationale**  
Likelihood rated Likely (4) because IAM misconfiguration and credential exposure are among the most common cloud security findings industry-wide, and staging environments routinely relax controls for convenience. Impact rated Major (4) since a compromised account or exposed credentials could grant broad access to production infrastructure and data.

---

## 4. Network Device Resilience & Hardening Risk

**Category:** Availability &nbsp;·&nbsp; **Status:** ![Open](https://img.shields.io/badge/status-Open-d73a49)  
**Likelihood:** 3/5 &nbsp;·&nbsp; **Impact:** 5/5 &nbsp;·&nbsp; **Risk Score:** 15 (![Critical](https://img.shields.io/badge/risk-Critical-b60205))  
**Owner:** Network Team

**Description**  
Core network devices carry risk of single points of failure, outdated firmware, weak or default administrator credentials, lack of segmentation, and unauthorized configuration changes. Staging devices share the same vulnerabilities at lower impact, while DR paths are typically untested and prone to misconfigured routing during an actual failover.

**Decision Rationale**  
Likelihood rated Possible (3) reflecting periodic hardware/firmware issues and the tendency for DR failover paths to go untested between drills. Impact rated Severe (5) because a core network device failure or compromise can disrupt connectivity for every dependent system, making it a true single point of failure.

---

## 5. Data Store (S3) Configuration & Availability Risk

**Category:** Data Protection &nbsp;·&nbsp; **Status:** ![Open](https://img.shields.io/badge/status-Open-d73a49)  
**Likelihood:** 3/5 &nbsp;·&nbsp; **Impact:** 4/5 &nbsp;·&nbsp; **Risk Score:** 12 (![High](https://img.shields.io/badge/risk-High-e36209))  
**Owner:** Augustine Ozor

**Description**  
S3-based data stores are exposed to misconfigured bucket permissions or public access, lack of encryption, no versioning or logging, and accidental deletion. Staging unnecessarily replicates sensitive data, and DR synchronization delays can leave recovery data incomplete.

**Decision Rationale**  
Likelihood rated Possible (3) since bucket misconfiguration and accidental deletion remain common operational errors despite cloud provider default protections. Impact rated Major (4) because exposed or lost data in a critical data store carries significant confidentiality and business-continuity consequences, though slightly below the database server given narrower typical usage.

---


---

<div align="center">

[← Overview](README.md) &nbsp;|&nbsp; [🏠 Home](README.md) &nbsp;|&nbsp; [Scoring Legend →](02-legend.md)

</div>
