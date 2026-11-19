# Operating Model — Biology Assessment Generator

**Last updated:** 2026-11-19

All data is synthetic.

---

## Roles

| Role | Responsibility |
|------|----------------|
| **Teacher** | Selects learning outcomes, reviews generated content, decides Keep/Edit/Reject, approves final assessment |
| **Head of Department (Science)** | Reviews flagged questions, approves assessments for school use, handles school-level escalations |
| **Cluster Science Master Teacher** | Resolves curriculum interpretation questions, advises on edge cases, handles cross-school escalations |
| **Curriculum Owner (CPDD, MOE)** | Maintains approved knowledge base, quarterly review of content accuracy, approves scope changes |
| **Product Owner** | Defines agent behaviour, approves permission settings, owns success metrics |
| **Engineering Lead** | Chooses vendor and model, implements agent, owns reliability and latency |
| **Data Protection Officer** | Approves data handling, reviews logs and retention, handles privacy incidents |
| **System Admin** | Manages access, monitors uptime, responds to incidents |

---

## Decision rights

| Decision | Harness part | Who decides | Who is consulted | Who is told |
|----------|--------------|-------------|------------------|-------------|
| **Scope** — What learning outcomes and content boundaries the agent can access | Knowledge base | Curriculum Owner | Product Owner, Master Teacher | Engineering Lead, Teachers |
| **Permissions** — What actions the agent can take (auto, confirm, block) | Agent config | Product Owner | Curriculum Owner, DPO, Engineering Lead | Teachers, System Admin |
| **Vendor and model** — Which LLM provider and model version to use | Infrastructure | Engineering Lead | Product Owner, DPO | Curriculum Owner, System Admin |
| **Go-live** — When to launch to teachers (pilot or scale) | Deployment | Product Owner | Curriculum Owner, Engineering Lead, HoD | Teachers, System Admin |
| **Incident** — How to respond when agent produces harmful or inaccurate content | Runtime | System Admin (immediate) / Product Owner (policy) | Engineering Lead, Curriculum Owner | Product Owner, Teachers, HoD, DPO |
| **Retire** — When to sunset the agent or roll back a version | Lifecycle | Product Owner | Curriculum Owner, Engineering Lead | Teachers, System Admin, HoD |

---

## Escalation path

```
Teacher
   ↓ cannot resolve
Head of Department (Science)
   ↓ cannot resolve
Cluster Science Master Teacher
   ↓ curriculum ambiguity
Curriculum Owner (CPDD, MOE)
```

---

## Review cadence

| Review | Frequency | Owner | Participants |
|--------|-----------|-------|--------------|
| Knowledge base accuracy | Quarterly | Curriculum Owner | Master Teacher, Product Owner |
| Permission settings | After each release | Product Owner | Engineering Lead, DPO |
| Incident review | Within 48h of incident | Product Owner | Engineering Lead, System Admin, affected Teachers |
| Success metrics | Monthly | Product Owner | Curriculum Owner, Engineering Lead |
| Model performance | Quarterly | Engineering Lead | Product Owner, Curriculum Owner |
