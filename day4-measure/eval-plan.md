# Eval Plan — Biology Assessment Generator

**Status:** Proposed  
**Last updated:** 2026-11-20

All items marked **Proposed** — review and confirm before use.

---

## Who owns what

| Responsibility | Role | Proposed |
|----------------|------|----------|
| **Signs the pass bar** | Product Owner | **Proposed** — owns go/no-go decision for pilot and scale |
| **Writes test cases** | Product Owner + Curriculum Owner | **Proposed** — Product Owner writes everyday/tricky cases; Curriculum Owner writes scope and accuracy cases |
| **Refreshes test cases** | Product Owner | **Proposed** — quarterly, or when syllabus changes |
| **Runs the eval** | Engineering Lead | **Proposed** — runs automated eval on every release; manual eval before go-live |
| **Reviews weekly sample** | Master Teacher | **Proposed** — reviews 10 random production responses per week for quality drift |
| **Calibrates graders** | Product Owner | **Proposed** — runs calibration session before each eval round |
| **Escalates failed deal-breakers** | Engineering Lead → Product Owner | **Proposed** — immediate escalation, blocks release |

---

## When it runs

| Trigger | Eval type | Scope | Proposed |
|---------|-----------|-------|----------|
| **Before go-live (pilot)** | Full eval | All 14 cases + 5 deal-breakers | **Proposed** — must pass bar before first teacher sees agent |
| **Before go-live (scale)** | Full eval + field sample | All cases + 20 real teacher sessions | **Proposed** — validates pilot learnings hold at scale |
| **Before every model change** | Full eval | All 14 cases | **Proposed** — new model version, prompt change, or knowledge base update |
| **Before every permission change** | Targeted eval | Cases affected by the permission | **Proposed** — e.g., if "regenerate" moves from Confirm to Auto, run Cases 6, 7 |
| **Weekly (production)** | Sample review | 10 random responses | **Proposed** — Master Teacher reviews for quality drift |
| **Monthly (production)** | Metrics review | Retention rate, error detection, time | **Proposed** — Product Owner reviews dashboard |
| **When syllabus changes** | Full eval + new cases | All cases + new syllabus-specific cases | **Proposed** — triggered by Curriculum Owner |
| **After incident** | Targeted eval | Cases related to incident type | **Proposed** — within 48h of incident |

---

## How I'll know it's working

### Goal

**Proposed**

Teachers trust AI-generated questions enough to use them rather than starting from scratch, cutting assessment creation from 5.5 hours to under 2 hours.

---

### Baseline

**Proposed**

| Metric | Baseline (pre-agent) | Source |
|--------|---------------------|--------|
| Assessment creation time | 5.5 hours | Teacher survey (synthetic) |
| Question retention rate | N/A (no agent) | — |
| Teacher confidence in AI | N/A | — |
| Error detection rate | N/A | — |

---

### Target and review date

**Proposed**

| Metric | Target | Review date | Owner |
|--------|--------|-------------|-------|
| Question retention rate | ≥70% | Pilot end (Week 4) | Product Owner |
| Teacher confidence (can verify accuracy) | ≥85% | Pilot end (Week 4) | Product Owner |
| Error detection (planted errors caught) | ≥95% | Pilot end (Week 4) | Product Owner |
| Assessment creation time | <2 hours | Scale (Week 12) | Product Owner |
| Repeat usage (voluntary return) | ≥80% | Scale (Week 12) | Product Owner |
| Deal-breaker pass rate | 100% | Every release | Engineering Lead |

---

### Usage metric

**Proposed**

**Primary:** Weekly active teachers (WAT) — teachers who generate at least one assessment per week.

| Phase | Target WAT | Proposed |
|-------|------------|----------|
| Pilot (Week 1–4) | 10–20 teachers | **Proposed** |
| Scale (Week 5–12) | 100+ teachers | **Proposed** |
| Steady state | 500+ teachers | **Proposed** |

**Why this metric:** If teachers aren't using the agent voluntarily, the value proposition has failed — regardless of eval scores.

---

### Pattern to watch first

**Proposed**

**Watch:** Silent subtle errors (Dimension 1 failures) in the first 2 weeks of pilot.

| Signal | What it means | Action |
|--------|---------------|--------|
| 0 silent errors in Week 1–2 | Guardrails working | Continue pilot |
| 1–2 silent errors in Week 1–2 | Edge cases exist | Add to test cases, patch, re-eval |
| 3+ silent errors in Week 1–2 | Systematic gap | Pause pilot, root cause analysis |

**Why this pattern:** Silent subtle errors are the deal-breaker type that erodes trust. If they appear early, the agent isn't ready.

---

### Stop line

**Proposed**

| Condition | Action | Owner |
|-----------|--------|-------|
| Any deal-breaker case fails in eval | Block release | Engineering Lead |
| <50% question retention in pilot | Stop pilot, rework | Product Owner |
| <80% error detection in pilot | Stop pilot, rework | Product Owner |
| 3+ silent subtle errors in production | Suspend agent, incident review | Product Owner |
| Teacher reports content used with students that contained undetected error | Suspend agent, immediate review | System Admin → Product Owner |

---

## First 30 days

**Proposed**

### Week 1: Pre-pilot eval

| Day | Activity | Owner | Output |
|-----|----------|-------|--------|
| 1–2 | Run full eval (14 cases) | Engineering Lead | Eval results |
| 3 | Calibration session | Product Owner + Master Teacher | Aligned scoring |
| 4 | Product Owner reviews results | Product Owner | Go/no-go decision |
| 5 | Fix any failures, re-run eval | Engineering Lead | Pass bar met |

### Week 2: Pilot launch

| Day | Activity | Owner | Output |
|-----|----------|-------|--------|
| 6 | Pilot launch to 10 teachers | Product Owner | Agent live |
| 7–10 | Monitor usage, collect feedback | Product Owner | Usage dashboard |
| 10 | First sample review (10 responses) | Master Teacher | Quality check |

### Week 3: Pilot monitoring

| Day | Activity | Owner | Output |
|-----|----------|-------|--------|
| 11–15 | Daily usage check | Product Owner | Adoption curve |
| 15 | Second sample review | Master Teacher | Quality trend |
| 15 | Interim metrics review | Product Owner | Retention rate, confidence |

### Week 4: Pilot decision

| Day | Activity | Owner | Output |
|-----|----------|-------|--------|
| 16–19 | Collect pilot teacher feedback | Product Owner | Survey results |
| 20 | Third sample review | Master Teacher | Final quality check |
| 20 | Full metrics review | Product Owner | All targets checked |
| 20 | Pilot decision meeting | Product Owner + Curriculum Owner + Engineering Lead | Continue / Pivot / Stop |

### Week 5 onwards: Scale or iterate

| Outcome | Next step |
|---------|-----------|
| Pass all targets | Proceed to scale (100+ teachers) |
| Miss retention target (50–70%) | Iterate on question quality, extend pilot 2 weeks |
| Miss error detection target (<95%) | Rework flagging logic, re-eval, restart pilot |
| Miss any deal-breaker | Stop, root cause, major rework |

---

## Open questions

| Question | Options | Owner | Proposed |
|----------|---------|-------|----------|
| Who grades the weekly sample — Master Teacher alone or with Product Owner? | Solo / Pair | Product Owner | **Proposed: Pair for first month, then solo** |
| How are the 10 weekly samples selected — random or stratified by topic? | Random / Stratified | Engineering Lead | **Proposed: Stratified by topic** |
| Should teachers know they're in pilot, or is it a silent rollout? | Informed / Silent | Product Owner | **Proposed: Informed — builds trust** |
| What's the minimum pilot duration before scale decision? | 2 weeks / 4 weeks / 6 weeks | Product Owner | **Proposed: 4 weeks** |
