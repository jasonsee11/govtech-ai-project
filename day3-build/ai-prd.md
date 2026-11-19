# AI PRD — Biology Assessment Generator

**Status:** Approved  
**Last updated:** 2026-11-19

All data is synthetic.

---

## Problem and user

**User:** Lower secondary science teachers preparing for the revised biology curriculum.

**Problem:** Teachers spend an average of 5.5 hours creating one curriculum-aligned biology assessment. They struggle to:
- Interpret curriculum learning outcomes and content boundaries
- Design questions with appropriate difficulty and cognitive demand
- Develop answers and marking schemes
- Check scientific accuracy and curriculum alignment

**Target:** Under 2 hours per assessment.

**Agent bet:** Generate curriculum-aligned biology assessment questions with answers and marking schemes by retrieving from the knowledge base and matching teacher requirements.

---

## Instructions

The agent generates draft assessment questions for teacher review. It is not an autonomous decision-maker.

**For each question, the agent must:**
1. Search the curriculum knowledge base for the selected learning outcome
2. Retrieve mark allocation guidelines for the question type and mark value
3. Generate question text appropriate for lower secondary level
4. Generate a suggested answer
5. Generate a marking scheme with point allocation
6. Cite the curriculum source (document, section)
7. Assign a verification status (verified, unverified, source missing)
8. Flag uncertainties for teacher review

**Tone:** Professional, clear, concise. Use Singapore English conventions.

**Format:** Each question returned as a structured object with: question text, answer, marking scheme, marks, learning outcome, source, verification status, and flag reason (if any).

---

## Tools

| Tool | Purpose | Required |
|------|---------|----------|
| `curriculum_search` | Retrieve learning outcomes and content boundaries from knowledge base | Yes |
| `question_generate` | Generate a question for a specific learning outcome | Yes |
| `verify_alignment` | Check if generated content aligns with syllabus scope | Yes |
| `get_marking_scheme` | Retrieve mark allocation guidelines for question types | Yes |
| `sample_bank_search` | Find vetted example questions for reference | No |
| `flag_for_review` | Mark a question as uncertain for teacher attention | Yes |

---

## Context and memory

### Source hierarchy (query in this order)
1. MOE Lower Secondary Science Syllabus — definitive authority
2. Biology Teaching and Learning Guide — content boundaries and depth
3. Assessment Guidelines — question types, cognitive demand, mark allocation
4. Approved Textbooks — Singapore-approved terminology and examples
5. Sample Assessment Bank — vetted question patterns

### Remember across turns
- Selected topic and learning outcomes for the current session
- Questions already generated (avoid duplicates)
- Teacher edits and rejections (learn from feedback within session)
- Flagged uncertainties awaiting resolution

### Do not remember
- Teacher personal details beyond session
- Student names or performance data
- Content from previous assessment sessions (start fresh each time)
- Rejected question content after 30 days

---

## Permissions

Every action the agent takes, with tier and approved setting.

| Action | Tier | Setting | Notes |
|--------|------|---------|-------|
| Search curriculum knowledge base | Read | ** Auto** | No side effects |
| Retrieve marking scheme guidelines | Read | ** Auto** | No side effects |
| Search sample assessment bank | Read | ** Auto** | No side effects |
| Generate question text | Draft | ** Auto** | Teacher reviews before use |
| Generate suggested answer | Draft | ** Auto** | Teacher reviews before use |
| Generate marking scheme | Draft | ** Auto** | Teacher reviews before use |
| Assign verification status | Draft | ** Auto** | Teacher sees status on review |
| Flag question as uncertain | Draft | ** Auto** | Flags are visible, not hidden |
| Regenerate a single question | Draft | ** Confirm** | Replaces previous draft |
| Edit question text | Write | ** Confirm** | Modifies teacher's working copy |
| Edit suggested answer | Write | ** Confirm** | Modifies teacher's working copy |
| Edit marking scheme | Write | ** Confirm** | Modifies teacher's working copy |
| Mark question as Keep | Write | ** Confirm** | Records teacher decision |
| Mark question as Reject | Write | ** Confirm** | Records teacher decision |
| Save assessment to database | Write | ** Confirm** | Persists work |
| Export assessment to Word/PDF | Send | ** Confirm** | Leaves the system |
| Share assessment with other teachers | Send | ** Block** | Reaches other users |
| Send assessment to students | Send | ** Block** | Reaches students |
| Log session metrics | Write | ** Auto** | For analytics, no PII |
| Access teacher profile | Read | ** Auto** | For personalisation |
| Access student data | Read | ** Block** | Out of scope |
| Modify knowledge base | Write | ** Block** | Curriculum owner only |

**Tier definitions:**
- **Read** — retrieves data, no side effects
- **Draft** — creates content teacher will review before use
- **Write** — modifies persisted state
- **Send** — content leaves the system or reaches other people

**Setting definitions:**
- **Auto** — agent proceeds without asking
- **Confirm** — agent proposes, waits for teacher approval
- **Block** — agent cannot perform this action

---

## Human checkpoints

The teacher must confirm before the agent proceeds:

| Checkpoint | Trigger | Options |
|------------|---------|---------|
| After generation | Agent completes a question | Keep, Edit, Reject |
| After edit | Teacher modifies question | Save, Discard |
| On uncertainty | Agent flags a question | Keep anyway, Edit, Reject |
| On scope boundary | Agent unsure if topic is in scope | Confirm in scope, Skip |
| Before export | Teacher requests export | Approve, Cancel |
| On >50% rejection | Teacher rejects more than half | Adjust requirements, Continue |

---

## Stop conditions

The agent stops and surfaces the issue when:

| Condition | Agent action |
|-----------|--------------|
| No learning outcomes selected | Ask teacher to select at least one |
| Learning outcome not in knowledge base | Flag as unverified; ask teacher to proceed or skip |
| Content exceeds lower secondary scope | Refuse to generate; explain why and suggest alternative |
| Scientific accuracy uncertain | Flag question; do not mark as verified |
| Knowledge base retrieval fails | Offer Retry, Edit Manually, or Keep Original |
| Teacher rejects >50% in a session | Pause and ask if requirements need adjustment |
| Verification confidence < 0.7 | Flag for review; do not mark as verified |
| Export requested with unapproved questions | Block export; list questions needing approval |

**Hard stops (cannot be overridden):**
- Upper secondary or tertiary content requested
- No teacher session active
- Knowledge base unavailable for >30 seconds

---

## Logs

### What to log
| Field | Example | Retention |
|-------|---------|-----------|
| Session timestamp | 2026-11-19T10:23:00+08:00 | 1 year |
| Teacher ID (anonymised) | teacher-7842 | 1 year |
| Topic selected | Cells and Organisation | 1 year |
| Learning outcomes selected | 3 | 1 year |
| Questions generated | 5 | 1 year |
| Decisions per question | Q1: Keep, Q2: Keep, Q3: Reject | 1 year |
| Flags raised | 1 | 1 year |
| Flags resolved | 1 (teacher approved) | 1 year |
| Retention rate | 80% | 1 year |
| Session duration | 18 minutes | 1 year |
| Errors encountered | KB timeout at 10:25:12 | 90 days |

### What not to log
- Teacher name or email
- Student names or data
- Full question text (reference by ID only)
- Content of rejected questions after 30 days

---

## Business rules

| Rule | Behaviour |
|------|-----------|
| Scope boundary | Generate only within selected learning outcomes |
| Content level | Lower secondary only; refuse upper secondary or tertiary |
| Source citation | Every question must cite a curriculum source |
| Verification | Mark as verified only if source found and confidence ≥ 0.7 |
| Flagging | Flag automatically when uncertain; resolution is human |
| Mark allocation | Marking scheme points must sum to question marks |
| Duplicates | Do not generate duplicate questions within a session |
| Scientific accuracy | All facts must be accurate at lower secondary level |
| Fabrication | Never fabricate curriculum references or scientific facts |
| Approval | No content reaches students without teacher approval |

---

## What engineering decides

These are implementation decisions for engineering, not product:

| Decision | Options | Constraints |
|----------|---------|-------------|
| LLM provider | Claude, GPT-4, Gemini, etc. | Must support tool use |
| Knowledge base architecture | Vector DB, graph DB, hybrid | Must support source citation |
| Retrieval strategy | RAG, fine-tuning, hybrid | Must return source references |
| Verification method | Embedding similarity, LLM judge, rule-based | Must produce confidence score |
| Session storage | Redis, PostgreSQL, etc. | Must support 30-day retention |
| Export format | docx, pdf, both | Must preserve formatting |
| Hosting | Cloud, on-prem, hybrid | Must meet data residency requirements |
| Latency target | <3s per question, <15s for 5 questions | User-facing, not batch |

---

## Open decisions

Decisions that need to be made before production:

| Decision | Options | Owner | Deadline |
|----------|---------|-------|----------|
| Which curriculum documents are approved for the knowledge base? | Syllabus only, Syllabus + TLG, All 5 sources | Curriculum owner | Before pilot |
| Who is the named curriculum owner for quarterly reviews? | CPDD officer, Master Teacher, School HoD | MOE | Before pilot |
| What is the escalation SLA for curriculum interpretation questions? | 24h, 48h, 1 week | MOE | Before pilot |
| How do we handle the transition period (old + new syllabus)? | Separate KBs, tagged content, version selector | Product + Eng | Before pilot |
| What is the minimum confidence threshold for auto-verification? | 0.7, 0.8, 0.9 | Product | Before pilot |
| Should teachers see confidence scores or just verified/unverified? | Scores visible, Binary only, Configurable | Product | Before pilot |
| What happens to rejected questions after 30 days? | Hard delete, Anonymise, Archive | Legal + Eng | Before pilot |
| Can teachers share assessments with colleagues? | Yes (confirm), No (block), School-only | Product | Before scale |
| What data residency requirements apply? | Singapore only, GCC, etc. | Legal + Infra | Before build |
