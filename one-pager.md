# One Pager

Use case: **Scenario C · MOE Lower Secondary Biology** — AI-assisted assessment generation for the revised curriculum rollout.

All data in this document is synthetic.

## Problem and user

**User:** Lower secondary science teachers preparing for the revised biology curriculum.

**Problem:** Teachers understand the direction of the revised curriculum but struggle to translate it into practical assessments within their existing workload. They spend considerable time:
- Interpreting curriculum learning outcomes and content boundaries
- Searching for and adapting existing assessment resources
- Designing questions with appropriate difficulty and cognitive demand
- Developing answers and marking schemes
- Checking scientific accuracy and curriculum alignment

**Current state:** Teachers spend an average of 5.5 hours creating one aligned biology assessment, against a target of under 2 hours.

## Opportunity and evidence

**Opportunity:** Enable teachers to create high-quality, curriculum-aligned biology assessments in under two hours, giving them more time to focus on teaching and learning.

**Context:** MOE is rolling out a revised lower secondary biology curriculum across 140 secondary schools, involving approximately 1,100 science teachers and 40,000 students. Schools must be ready within 12 weeks. Only 41% of schools currently feel ready, against a target of 90%.

**Evidence (synthetic):**
- Schools ready for curriculum rollout: 41% (target: 90%)
- Average assessment preparation time: 5.5 hours (target: under 2 hours)
- Weekly enquiries from biology teachers: 450 (62% are repeats)

**User quotes (synthetic):**
- "I understand what the new curriculum wants us to achieve. It's finding the time to translate that into assessments that's difficult."
- "I don't just need AI to generate questions. I need to know why those questions are appropriate for my students."
- "If I have to spend hours checking and correcting the questions, I might as well create them myself."

## Experience and trust

**The moment:** A teacher selects the intended learning outcomes and generates a draft assessment, complete with questions, suggested answers, marking schemes and curriculum references. The teacher can confidently decide what to accept, refine or reject.

**What the user sees:**
- Selection of biology topics, learning outcomes, question types, difficulty levels
- Generated assessment with suggested answers and marking schemes
- Curriculum learning outcomes and source references alongside each question
- Indicators highlighting uncertainties or potential curriculum misalignment
- Edit, Regenerate, Replace and Restore Previous Version buttons
- Final review and approval step before exporting

**Trust gaps addressed:**
| Step | Trust gap | How we address it |
|------|-----------|-------------------|
| Trigger | Control — can't specify requirements | Topic, LO, difficulty, mark allocation selectors |
| AI step | Black box — why these questions? | Show curriculum reference for each question |
| Human check | Hallucination — is this accurate? | Flag uncertain alignment, surface source references |
| Outcome | Control — can't adjust easily | Edit, regenerate, replace individual questions |

## Risks (market, technical, team)

**Market risk:** Teachers won't change their workflow even if the tool works — they prefer their existing resources and methods.
- *How we test:* Measure voluntary repeat usage after first session. Kill if fewer than 50% of teachers return to use the tool a second time.

**Technical risk:** AI generates scientifically inaccurate or curriculum-misaligned content that teachers do not catch.
- *How we test:* Include deliberately flawed questions in prototype testing. Kill if teachers fail to catch more than 5% of planted errors, or if more than 30% of AI-generated questions contain inaccuracies requiring major correction.

**Team risk:** No curriculum specialist available to maintain and verify the knowledge base as the syllabus evolves.
- *How we test:* Identify a named curriculum owner before pilot launch. Kill if no owner commits to quarterly reviews of the knowledge base.

## Build plan and handoff

**Phase 1 (now):** Prototype with synthetic questions to test trust and retention.
**Phase 2:** Connect to approved curriculum knowledge base.
**Phase 3:** Pilot with teacher champions at selected schools.
**Phase 4:** Measure, refine, then scale across 140 schools.

**Handoffs:**
- Questions with uncertain curriculum alignment → flagged for teacher review
- Questions with potential scientific inaccuracy → flagged for teacher review
- Unresolved curriculum ambiguities → escalate to curriculum specialist
- Final assessment → requires teacher approval before use with students

## Agent role and guardrails

**Agent bet:** Generate curriculum-aligned biology assessment questions with answers and marking schemes by retrieving from the knowledge base and matching teacher requirements.

**What the agent does:**
1. Searches curriculum knowledge base for selected learning outcomes
2. Retrieves mark allocation guidelines for question type
3. Generates question text, suggested answer, and marking scheme
4. Verifies alignment with syllabus scope
5. Flags uncertainties for teacher review

**Rules of engagement:**
| Level | Scope |
|-------|-------|
| Decides alone | Which sources to query, how to phrase questions, when to flag |
| Proposes and waits | Each question (Keep/Edit/Reject), regeneration, edits |
| Person reviews | Final assessment, export, flagged questions, scope boundaries |

**Guardrails:**
- Generate only within specified topic and learning outcomes
- Never introduce upper secondary or tertiary biology content
- Never fabricate curriculum references or scientific facts
- Flag questions where alignment or accuracy is uncertain
- Require teacher approval before any content reaches students

**Stop conditions:**
- Content exceeds lower secondary scope → refuse and suggest alternative
- Knowledge base retrieval fails → offer Retry, Edit Manually, or Keep Original
- Teacher rejects >50% in a session → pause and ask if requirements need adjustment

**What stays human:** Learning outcome selection, Keep/Edit/Reject decisions, final approval, export sign-off. No student sees content the teacher did not explicitly approve.

**Source hierarchy:**
1. MOE Lower Secondary Science Syllabus — definitive authority
2. Biology Teaching and Learning Guide — content boundaries
3. Assessment Guidelines — question types, mark allocation
4. Approved Textbooks — Singapore-approved content
5. Sample Assessment Bank — vetted examples

## Roles and operating model

**Curriculum owner:** Science Curriculum Planning Office, MOE
- Maintains approved knowledge base
- Quarterly review of content accuracy

**School-level review:** Head of Department (Science)
- Reviews flagged questions
- Approves assessments for use

**Escalation path:** Cluster Science Master Teacher
- Resolves curriculum interpretation questions
- Advises on edge cases

**Teacher:** Retains full accountability
- Selects learning outcomes and requirements
- Reviews, edits, approves all generated content
- Decides what to keep, edit, or reject

## Strategy and roadmap

**Diagnosis:** Teachers understand the direction of the revised biology curriculum but struggle to translate it into practical assessments within their existing workload.

**Guiding policy:** Efficient but purposeful use — teachers use AI-assisted materials quickly while staying accountable, not offloading judgment.

**Coherent actions:**
1. Establish a trusted curriculum knowledge base with approved syllabus documents, learning outcomes, and assessment guidelines.
2. Build an AI-powered assessment assistant with teacher oversight — generate, verify, and refine questions with explicit mapping to learning outcomes.
3. Pilot with teacher champions, measure impact, refine, then scale across 140 secondary schools.

## Metrics plan and stop line

**Primary metric:** Question retention rate
- Target: At least 70% of AI-generated questions retained with no or minor edits
- Stop line: Below 50% retention

**Secondary metrics:**
| Metric | Target | Stop line |
|--------|--------|-----------|
| Teacher confidence (can verify accuracy) | ≥85% | <70% |
| Perceived control (can customise) | ≥90% | <80% |
| Repeat usage (voluntary return) | ≥80% | <50% |
| Error detection (catch planted errors) | ≥95% | <80% |
| Assessment time | <2 hours | >4 hours |

**Safety stop:** Suspend live use if confidential assessment materials are exposed, or if critical scientific inaccuracies cannot be reliably identified and controlled.

## Evals and gates

**Gate 1: Prototype testing (now)**
- Do teachers retain ≥70% of questions?
- Do teachers catch ≥95% of planted errors?
- Do teachers report confidence ≥4/5 in verifying accuracy?

**Gate 2: Pilot launch**
- Is a named curriculum owner committed?
- Is the knowledge base populated with approved content?
- Is the escalation path documented and staffed?

**Gate 3: Scale decision**
- Does assessment time drop below 2 hours?
- Do ≥80% of pilot teachers voluntarily return?
- Are there zero critical inaccuracies in approved assessments?

**Test questions (from context-skill.md):**
1. Within scope — generates appropriate content for specified LO
2. Flag required — refuses or flags when asked to exceed scope
3. Cognitive demand — matches question difficulty to mark allocation
4. Scientific accuracy — true/false statements are unambiguous
5. Source citation — includes curriculum reference, flags if LO not selected

## Decision: continue, pivot or stop

**Riskiest assumption:** Teachers will trust the accuracy of AI-generated questions enough to use them, rather than starting from scratch.

**Kill switch:** Stop if teachers consistently reject or heavily rewrite more than 50% of generated questions. This signals that the AI output is not a better starting point than their current resources.

**Success signal:** At least 7 in 10 teachers retain the generated questions with minor or no edits during prototype testing by 20 Nov.

**Decision framework:**
| Signal | Action |
|--------|--------|
| ≥70% retention + ≥95% error detection | Continue to pilot |
| 50-70% retention | Pivot — improve curriculum grounding |
| <50% retention or <80% error detection | Stop — assumption invalidated |

## Open issues

1. Which curriculum documents are approved for inclusion in the knowledge base?
2. Who is the named curriculum owner willing to commit to quarterly reviews?
3. How do we handle the transition period when both old and new syllabuses are in use?
4. What is the escalation SLA for curriculum interpretation questions?
5. How do we version-control the knowledge base as the syllabus evolves?
