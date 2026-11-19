# Agent Control Panel

**Agent bet:** Generate curriculum-aligned biology assessment questions with answers and marking schemes by retrieving from the knowledge base and matching teacher requirements.

All data is synthetic.

---

## What the agent is doing

The agent takes a teacher's selection (topic, learning outcomes, mark allocation) and generates draft assessment questions. For each question, it:

1. Searches the curriculum knowledge base for the selected learning outcome
2. Retrieves mark allocation guidelines for the question type
3. Generates question text appropriate for lower secondary level
4. Generates a suggested answer
5. Generates a marking scheme with point allocation
6. Verifies alignment with syllabus scope
7. Flags uncertainties for teacher review

The agent does not decide what goes into the final assessment. It produces drafts; the teacher decides.

---

## Opportunity portfolio

| Opportunity | Value | Confidence | Dependencies |
|-------------|-------|------------|--------------|
| Cut assessment creation from 5.5 hours to under 2 hours | High | Medium | Knowledge base quality, teacher trust |
| Reduce repeat enquiries to curriculum team (currently 450/week, 62% repeats) | Medium | High | Questions answered by in-context references |
| Improve curriculum alignment consistency across 140 schools | High | Low | Adoption rate, teacher training |
| Free teacher time for actual teaching | High | Medium | Workflow change acceptance |

**Primary bet:** Teachers will trust AI-generated questions enough to use them rather than starting from scratch.

**Kill signal:** <50% retention rate, or teachers miss >5% of planted errors.

---

## Rules of engagement

### Decides alone
The agent decides alone on:
- Which knowledge base sources to query
- How to phrase the question within scope
- How to structure the marking scheme
- Whether to flag a question as uncertain (flag is automatic; resolution is not)

### Proposes and waits
The agent proposes and waits for teacher decision on:
- Each generated question (Keep / Edit / Reject)
- Flagged questions with uncertain alignment
- Regeneration requests
- Any edit to question text or answer

### A person reviews
A person must review before:
- Any question is included in a final assessment
- Any assessment is exported for student use
- Any flagged question is kept despite the flag
- Scope boundary decisions (is this topic in or out?)

**Escalation path:**
- Teacher cannot resolve → Head of Department (Science)
- HoD cannot resolve → Cluster Science Master Teacher
- Curriculum ambiguity → Science Curriculum Planning Office, MOE

---

## Stop conditions

The agent stops and surfaces the issue when:

| Condition | Agent action |
|-----------|--------------|
| No learning outcomes selected | Ask teacher to select at least one |
| Learning outcome not in knowledge base | Flag as unverified; ask teacher to proceed or skip |
| Content exceeds lower secondary scope | Refuse to generate; explain why and suggest alternative |
| Scientific accuracy uncertain | Flag question; do not auto-include |
| Knowledge base retrieval fails | Offer Retry, Edit Manually, or Keep Original |
| Teacher rejects >50% in a session | Pause and ask if requirements need adjustment |
| Confidence below threshold (< 0.7) | Flag for review; do not mark as verified |

**Hard stops (agent cannot override):**
- Upper secondary or tertiary content requested
- No teacher logged in
- Knowledge base unavailable for >30 seconds
- Export requested without teacher approval on all questions

---

## What stays human

These decisions stay with the teacher, not the agent:

| Decision | Why it stays human |
|----------|-------------------|
| Which learning outcomes to assess | Pedagogical judgment based on class progress |
| Final Keep / Edit / Reject on each question | Professional accountability for content |
| Whether to use a flagged question despite the flag | Teacher accepts the risk |
| Mark allocation per question | Teacher knows their assessment weighting |
| When the assessment is ready for students | Teacher signs off on the whole, not just the parts |
| Whether AI-generated content is appropriate for their class | Context the agent cannot see (student needs, prior learning) |

**The line:** The agent generates and flags. The teacher decides and approves. No student ever sees content the teacher did not explicitly approve.
