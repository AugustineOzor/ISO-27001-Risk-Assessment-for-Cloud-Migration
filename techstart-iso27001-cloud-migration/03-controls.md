# 🛡️ Controls

> 5 security controls implemented and assessed against ISO 27001 Annex A, NIST CSF, and CIS Controls, each mapped to a specific migration risk.

| # | Control | Linked Risk | Framework | Reference | Effectiveness |
|---|---|---|---|---|---|
| 1 | Prompt Injection & Output Filtering Controls | Chatbot Application Security & Data Exposure Risk | NIST CSF | `PR.PS-06` | ![Partially Effective](https://img.shields.io/badge/status-Partially%20Effective-dbab09) |
| 2 | Database Access Control & Encryption | Database Server Security & Recovery Risk | ISO 27001 | `A.8.3` | ![Effective](https://img.shields.io/badge/status-Effective-28a745) |
| 3 | Cloud IAM Governance & MFA Enforcement | Cloud Account Misconfiguration & Access Risk | CIS Control | `CIS 6.5` | ![Partially Effective](https://img.shields.io/badge/status-Partially%20Effective-dbab09) |
| 4 | Network Device Hardening & Redundancy | Network Device Resilience & Hardening Risk | CIS Control | `CIS 12.1` | ![Not Tested](https://img.shields.io/badge/status-Not%20Tested-6a737d) |
| 5 | S3 Bucket Policy & Data Protection Controls | Data Store (S3) Configuration & Availability Risk | CIS Control | `CIS 3.3` | ![Effective](https://img.shields.io/badge/status-Effective-28a745) |

## 1. Prompt Injection & Output Filtering Controls

**Linked Risk:** Chatbot Application Security & Data Exposure Risk  
**Framework:** NIST CSF `PR.PS-06` &nbsp;·&nbsp; **Frequency:** Continuous  
**Effectiveness:** ![Partially Effective](https://img.shields.io/badge/status-Partially%20Effective-dbab09) &nbsp;·&nbsp; **Owner:** Augustine Ozor

**Description**  
Works by validating and sanitizing user inputs, restricting system prompt/instruction exposure, and filtering outputs for PII patterns before they reach the user. Implemented as a guardrail layer sitting between the user interface and the LLM API, including rate limiting on suspicious input patterns. Tested through periodic red-team prompt injection exercises and automated regression tests run before each release.

**Decision Rationale**  
Rated Partially Effective because the guardrails measurably reduce exposure but cannot fully eliminate evolving prompt injection techniques, and testing currently runs on a release-cycle basis rather than continuous automated coverage, leaving a window between releases where new attack patterns go undetected.

---

## 2. Database Access Control & Encryption

**Linked Risk:** Database Server Security & Recovery Risk  
**Framework:** ISO 27001 `A.8.3` &nbsp;·&nbsp; **Frequency:** Continuous  
**Effectiveness:** ![Effective](https://img.shields.io/badge/status-Effective-28a745) &nbsp;·&nbsp; **Owner:** John Ketson

**Description**  
Works by enforcing role-based access control (RBAC) so users and services only reach the data they need, combined with TLS-encrypted connections and encryption at rest. Implemented via IAM roles mapped to database users and infrastructure-level encryption enabled by default. Tested through quarterly access reviews to confirm least-privilege assignment and annual penetration testing to validate the access boundary holds under attack.

**Decision Rationale**  
Rated Effective because the most recent quarterly access review and annual penetration test found no material access control failures, and encryption is enforced automatically at the infrastructure layer rather than depending on manual configuration.

---

## 3. Cloud IAM Governance & MFA Enforcement

**Linked Risk:** Cloud Account Misconfiguration & Access Risk  
**Framework:** CIS Control `CIS 6.5` &nbsp;·&nbsp; **Frequency:** Continuous  
**Effectiveness:** ![Partially Effective](https://img.shields.io/badge/status-Partially%20Effective-dbab09) &nbsp;·&nbsp; **Owner:** Augustine Ozor

**Description**  
Works by applying least-privilege IAM policies and requiring multi-factor authentication for privileged account access, with credential rotation to limit the lifespan of exposed keys. Implemented through cloud-native IAM policies and a cloud security posture management (CSPM) tool that flags risky configurations. Tested via monthly automated configuration scans plus periodic manual review of high-privilege roles.

**Decision Rationale**  
Rated Partially Effective because monthly scans continue to surface overly permissive policies and MFA is not yet enforced on every privileged account, meaning the control reduces but does not currently close the access risk it targets.

---

## 4. Network Device Hardening & Redundancy

**Linked Risk:** Network Device Resilience & Hardening Risk  
**Framework:** CIS Control `CIS 12.1` &nbsp;·&nbsp; **Frequency:** Quarterly  
**Effectiveness:** ![Not Tested](https://img.shields.io/badge/status-Not%20Tested-6a737d) &nbsp;·&nbsp; **Owner:** Network Team

**Description**  
Works by applying hardened configuration baselines to network devices (disabling default accounts, replacing default credentials) and maintaining a planned redundant failover path for core devices. Implemented through configuration management standards and scheduled firmware patch cycles. Intended to be validated through DR failover drills and configuration audits, but no such drill or audit has yet been performed.

**Decision Rationale**  
Rated Not Tested because, while the hardening baseline and redundancy design exist on paper, no failover drill or configuration audit has been carried out to confirm the control actually performs as intended under a real device failure.

---

## 5. S3 Bucket Policy & Data Protection Controls

**Linked Risk:** Data Store (S3) Configuration & Availability Risk  
**Framework:** CIS Control `CIS 3.3` &nbsp;·&nbsp; **Frequency:** Monthly  
**Effectiveness:** ![Effective](https://img.shields.io/badge/status-Effective-28a745) &nbsp;·&nbsp; **Owner:** Augustine Ozor

**Description**  
Works by enforcing bucket policies that block public access and apply least-privilege permissions, combined with default server-side encryption, versioning, and access logging. Implemented via S3 bucket policies, account-level Block Public Access settings, and CloudTrail logging for auditability. Tested through monthly automated configuration scans and periodic review of access logs.

**Decision Rationale**  
Rated Effective because monthly automated scans have consistently confirmed no public exposure and that encryption, versioning, and logging remain enabled across the review period, with no exceptions identified.

---


---

<div align="center">

[← Scoring Legend](02-legend.md) &nbsp;| [Risk Treatment Plan →](04-risk-treatment-plan.md)

</div>
