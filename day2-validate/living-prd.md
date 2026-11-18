# Living PRD — Biology Assessment Generator

**Scenario:** C · MOE Lower Secondary Biology  
**Prototype:** `day2-validate/prototype/index.html`  
**Last updated:** 2026-11-18

This document is extracted from the actual code. Update it as the prototype evolves.

---

## 1. Product overview

An AI-assisted assessment generator that helps lower secondary biology teachers create curriculum-aligned assessments faster. Teachers select topics and learning outcomes, review AI-generated questions, and decide what to keep, edit, or reject.

**Target time:** Under 2 hours (down from 5.5 hours average).

---

## 2. Problem and riskiest assumption

**Problem:** Teachers understand the revised biology curriculum but struggle to translate it into practical assessments within their existing workload. They spend too much time searching, adapting, and verifying questions.

**Riskiest assumption:** Teachers will trust AI-generated questions enough to use them rather than starting from scratch.

**Kill switch:** Stop if >50% of questions are rejected or heavily rewritten.

**Success signal:** ≥70% of questions retained with minor or no edits.

---

## 3. User flow and screen map

### Screen 1: Select topic and learning outcomes
- Dropdown: Choose biology topic (e.g., "Cells and Organisation")
- Checkboxes: Select 1–3 learning outcomes
- Button: "Generate Assessment"
- Info box explains what the tool does

### Screen 2: Review generated questions
- 5 questions displayed as cards
- Each card shows:
  - Question number and marks
  - Question text and suggested answer
  - Verification status badge (✓ Verified, ⚠ Unverified, ✗ Source missing)
  - Expandable details panel (curriculum source, rationale, marking scheme)
  - Action buttons: Keep, Edit, Reject
  - Regenerate button (per-question)
- Summary box at bottom with retention stats and confidence survey
- Back link to return to Screen 1

### Trust Lab (tester overlay)
- 5 scenario buttons: Black Box, Hallucination, Control, AI Uncertainty, Failure Recovery
- Toggle: Show/hide curriculum references
- Toggle: Reveal planted errors
- Live metrics: Retention rate, Errors caught, Review time, Confidence
- Copy results button

---

## 4. Success metrics

| Metric | Target | Kill |
|--------|--------|------|
| Question retention rate | ≥70% | <50% |
| Error detection (planted errors caught) | ≥95% | <80% |
| Teacher confidence (can verify accuracy) | ≥85% | <70% |
| Assessment creation time | <2 hours | >4 hours |
| Repeat usage | ≥80% | <50% |

**Prototype captures automatically:**
- Retention rate (kept vs rejected)
- Errors caught (if reveal toggle used)
- Review time (from first question load)
- Confidence (1–5 survey at end)

---

## 5. Technical reality

### What exists

| Aspect | Current state |
|--------|--------------|
| File | Single `index.html`, 1,330 lines |
| Size | ~57KB, embedded CSS (~200 lines) + JS |
| Build step | None — open in browser |
| Backend | None — all data is hardcoded |
| Dependencies | Zero |
| Tests | Zero |

### Key state variables (lines 476–481, 862)
```javascript
let activeScenario = null;
let startTime = null;
let showRefsEnabled = true;
let revealErrors = false;
let teacherConfidence = null;
let simulateFailure = false;
let currentQuestions = [];
```

### Key functions
| Function | Purpose | Line |
|----------|---------|------|
| `runScenario()` | Loads Trust Lab test scenario | 890 |
| `renderQuestions()` | Draws question cards with current state | 1061 |
| `decide()` | Records Keep/Edit/Reject decision | 1191 |
| `startEdit()` / `saveEdit()` | Inline editing flow | 1140, 1168 |
| `regenerate()` | Replaces single question (or triggers failure) | 1213 |
| `showFailureModal()` | Opens failure recovery UI | 1230 |
| `toggleDetails()` | Expands/collapses curriculum details | 1128 |
| `updateMetrics()` | Refreshes Trust Lab metrics display | 935 |

### Question sets (hardcoded)
- `questions`: Standard set (5 questions)
- `blackboxQuestions`: With visible reasoning
- `hallucinationQuestions`: 2 planted errors
- `controlQuestions`: Standard for edit testing
- `uncertaintyQuestions`: With flagged/uncertain items
- `failureQuestions`: Triggers regeneration failure

---

## 6. Assumptions and risks

### Market risk
Teachers won't change their workflow even if the tool works.
- *Test:* Measure voluntary repeat usage after first session
- *Kill:* <50% return for second use

### Technical risk
AI generates inaccurate content that teachers don't catch.
- *Test:* Plant errors in prototype, measure detection rate
- *Kill:* <80% error detection, or >30% need major correction

### Team risk
No curriculum specialist to maintain knowledge base.
- *Test:* Identify named curriculum owner before pilot
- *Kill:* No owner commits to quarterly reviews

### Assumptions baked into prototype
1. Teachers will use a web-based tool (not paper/Word)
2. Teachers can evaluate question quality within the review flow
3. Keep/Edit/Reject is the right decision vocabulary
4. Curriculum references increase trust
5. Failure recovery options are sufficient (Retry, Edit, Keep)

---

## 7. In and out of scope

### In scope (prototype)
- ✅ Topic and learning outcome selection
- ✅ Question generation (hardcoded, not AI)
- ✅ Keep/Edit/Reject decisions
- ✅ Inline editing without regenerating full assessment
- ✅ Single-question regeneration
- ✅ Verification status badges
- ✅ Expandable curriculum details
- ✅ Trust Lab with 5 test scenarios
- ✅ Failure recovery modal with 3 options
- ✅ Metrics capture (retention, time, confidence)

### Out of scope (prototype)
- ❌ Real AI generation (using Claude or similar)
- ❌ Actual curriculum knowledge base connection
- ❌ Data persistence (decisions reset on refresh)
- ❌ User authentication
- ❌ Export to Word/PDF
- ❌ Multi-user or school-level features
- ❌ Mobile-optimised layout

---

## 8. Engineering recommendation

**Treat this as a throwaway prototype.**

The prototype exists to test a hypothesis about teacher trust, not to build production code. It has done its job if we learn whether teachers will trust AI-generated questions.

**What to carry forward:**
- The Keep/Edit/Reject decision flow
- Verification badges with three states
- Expandable details for transparency
- Per-question regeneration (not full-assessment regeneration)
- Failure recovery with multiple options
- Metrics capture approach (retention rate, confidence survey)

**What to rebuild:**
- Everything else

**Known fragilities:**
1. **State resets on screen transition** — `decisions` object clears when navigating back to Screen 1
2. **Timer never clears** — `setInterval` runs forever, no `clearInterval` on unmount
3. **No validation** — no checks for empty selections or edge cases

**Next engineering phase:**
1. Rebuild as a proper application (React/Next.js or similar)
2. Connect to curriculum knowledge base (RAG over MOE syllabus docs)
3. Integrate AI generation with guardrails from `context-skill.md`
4. Add persistence layer (database for decisions, progress)
5. Build test suite for trust scenarios
