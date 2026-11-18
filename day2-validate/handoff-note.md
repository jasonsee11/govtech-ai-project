# Handoff Note — Biology Assessment Generator Prototype

**Date:** 2026-11-18  
**Prototype:** `day2-validate/prototype/index.html`  
**Status:** Keep prototyping

---

## What it does

A single-file clickable prototype (1,458 lines, zero dependencies) that lets teachers:

1. **Select** a biology topic and learning outcomes
2. **Review** 5 AI-generated questions with suggested answers, marking schemes, and curriculum references
3. **Decide** on each question: Keep, Edit, or Reject
4. **Edit** individual questions inline without regenerating the entire assessment
5. **Regenerate** a single question if needed
6. **See** verification status (Verified, Unverified, Source missing) and expandable curriculum details

The Trust Lab provides 5 test scenarios for testers: Black Box, Hallucination, Control, AI Uncertainty, and Failure Recovery.

---

## What is synthetic

Everything. This is a prototype for testing trust, not a working product.

| Component | Synthetic |
|-----------|-----------|
| Questions | 5 hardcoded question sets, not AI-generated |
| Curriculum references | Made-up syllabus citations |
| Verification status | Manually assigned per question |
| Planted errors | 2 deliberate mistakes in Hallucination scenario |
| Failure simulation | Triggered by scenario selection, not real API failure |
| Metrics | Calculated from in-memory state, not persisted |

---

## What is missing for production

| Category | Gap |
|----------|-----|
| **AI generation** | No LLM integration — questions are hardcoded |
| **Knowledge base** | No curriculum document retrieval (RAG) |
| **Persistence** | Decisions reset on page refresh |
| **Authentication** | No user login or school-level access |
| **Export** | No Word/PDF output |
| **Backend** | No server, no database |
| **Tests** | Zero automated tests |
| **Accessibility** | Not audited |
| **Mobile** | Not optimised for smaller screens |

---

## Decisions an engineer must not change without asking

These reflect validated design choices from prototype testing:

1. **Keep / Edit / Reject vocabulary** — This three-option flow tested well. Do not rename or add options without user research.

2. **Per-question regeneration** — Teachers want to replace one question without losing others. Do not change to full-assessment regeneration.

3. **Verification badges at top of each card** — Visibility of trust signals matters. Do not bury these in expandable sections.

4. **Failure recovery with 3 options** — Retry, Edit Manually, Keep Original. This pattern preserves teacher control. Do not reduce to a single "OK" dismissal.

5. **Expandable curriculum details** — Teachers want transparency on demand, not by default. Do not auto-expand or remove the expand/collapse pattern.

6. **Metrics captured: retention rate, errors caught, review time, confidence** — These map to our success criteria. Do not remove or rename without updating the metrics plan.

---

## Handoff decision

**Decision:** Keep prototyping

**Why:**
- Have not tested with real teachers yet — prototype was built for Trust Lab scenarios, not live user sessions
- Metrics are captured but no data has been collected — need to run actual test sessions before we know if the hypothesis holds

**What must happen before moving to production spec:**
1. Run 3–5 test sessions with real teachers using the Trust Lab
2. Capture retention rate, error detection, and confidence scores
3. Review results against success criteria (≥70% retention, ≥95% error detection)
4. If criteria met, proceed to production spec with findings as evidence

**Next step:** Schedule teacher testing sessions and prepare a brief test script.
