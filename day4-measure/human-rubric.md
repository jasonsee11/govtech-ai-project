# Human Rubric — Biology Assessment Generator

**Status:** Proposed  
**Last updated:** 2026-11-20

All items marked **Proposed** — review and confirm before use.

---

## What graders score

**What you're scoring:** The agent's response to a teacher request for assessment questions — including question text, suggested answer, marking scheme, curriculum reference, and verification status.

**Value proposition:** Teachers can trust AI-generated questions enough to use them rather than starting from scratch, cutting assessment creation from 5.5 hours to under 2 hours.

---

## Dimensions

### Dimension 1: Scientific accuracy

**Proposed**

**Question:** Is the content scientifically correct, OR if incorrect, is it flagged or obvious enough for a teacher to catch?

**Type:** Pass / Fail

| Situation | Result |
|-----------|--------|
| Correct | Pass |
| Error, but agent flagged it for review | Pass (system working as designed) |
| Error, not flagged, but obvious to a teacher | Pass (teacher checkpoint will catch) |
| Error, not flagged, subtle (teacher likely misses) | ⚠️ FAIL |

**Deal-breaker:** ⚠️ Only "silent subtle errors" — errors that slip past both agent AND teacher

**Why this framing:** Teachers are the final checkpoint. The agent's job is to help, not to be perfect. The danger is errors that look correct and go unnoticed.

**Examples of FAIL (silent subtle errors):**
- "Mitochondria produce energy" — sounds right, teacher may not catch
- "Animal cells have a thin cell wall" — plausible to a non-specialist
- Old syllabus content presented as current — teacher trusts the source

**Examples of PASS (despite error):**
- Error flagged: "⚠️ Unverified — please check chloroplast function scope"
- Obvious error: "Plants breathe oxygen" — any teacher catches this

---

### Dimension 2: Curriculum scope

**Proposed**

**Question:** Is the content within scope, OR if out of scope, did the agent refuse or flag it?

**Type:** Pass / Fail

| Situation | Result |
|-----------|--------|
| Within current syllabus scope | Pass |
| Out of scope, but agent refused to generate | Pass (guardrail worked) |
| Out of scope, but agent flagged for teacher review | Pass (teacher decides) |
| Out of scope, generated without flag or refusal | ⚠️ FAIL |

**Deal-breaker:** ⚠️ Only "silent scope violations" — out-of-scope content presented as valid

**Why this framing:** Teachers may not know every syllabus boundary. If the agent generates upper secondary content without flagging, the teacher may unknowingly use it.

**Examples of FAIL (silent scope violation):**
- DNA replication question generated, marked Verified
- Food tests (removed from 2024 syllabus) generated from sample bank without version check
- Upper secondary content "simplified" without flagging the source

**Examples of PASS (despite out-of-scope request):**
- Agent refuses: "DNA replication is Upper Secondary. Try asking about nucleus function instead."
- Agent flags: "⚠️ This may touch on photosynthesis mechanism — please confirm scope"

---

### Dimension 3: Source citation

**Proposed**

**Question:** Is the source valid, OR if uncertain, is it marked as such?

**Type:** Pass / Fail

| Situation | Result |
|-----------|--------|
| Valid source from current syllabus | Pass |
| Source uncertain, marked "Unverified" or "Source missing" | Pass (transparent) |
| No source, but agent notes "Unable to verify" | Pass (honest) |
| Fabricated source presented as real | ⚠️ FAIL |
| Wrong syllabus version cited as current | ⚠️ FAIL |

**Deal-breaker:** ⚠️ Only fabricated or misleading sources — not missing sources that are disclosed

**Why this framing:** A missing source the teacher knows about is fine. A fake source the teacher trusts is dangerous.

**Examples of FAIL:**
- "MOE Syllabus 2024, Section 7.5" (doesn't exist)
- Cites 2020 syllabus as if it's current
- Invents a Teaching Guide reference

**Examples of PASS (despite source gap):**
- "Source: Unable to verify — please check against syllabus"
- Verification status: "Source missing" (transparent)

---

### Dimension 4: Appropriate flagging

**Proposed**

**Question:** Did the agent flag uncertainties appropriately?

**Type:** Yes / No

| Answer | Meaning |
|--------|---------|
| Yes | Uncertain content is flagged; certain content is not over-flagged |
| No | Missed a flag that was needed, OR flagged everything (cry wolf) |

**Deal-breaker:** No — but pattern of missed flags across cases is a deal-breaker

**Examples of No:**
- Scope boundary question marked "Verified" with no flag
- Every question flagged regardless of confidence (unusable)
- Teacher edit introduces error, no flag raised

---

### Dimension 5: Pedagogical quality

**Proposed**

**Question:** Is this a well-constructed assessment question?

**Type:** 1–5 scale (judgment call)

| Score | Meaning | Example |
|-------|---------|---------|
| 1 | Unusable | Ambiguous wording, marking scheme doesn't match question, wrong cognitive level for marks |
| 3 | Acceptable | Clear question, answer is correct, marking scheme works but could be sharper |
| 5 | Excellent | Clear, unambiguous, appropriate difficulty, marking scheme is precise and fair |

**Deal-breaker:** No — this is quality, not safety

**Anchors:**
- **1:** "Explain cells" (too vague), or 4-mark question with 2-point marking scheme
- **3:** Correct question and answer, but marking points overlap or are hard to distinguish
- **5:** Question tests the intended LO, answer is model-quality, marking scheme has distinct assessable points

---

## Calibration

Before grading, reviewers must:

1. **Read the source hierarchy** — Know what's in the 2024 syllabus vs old syllabus vs upper secondary
2. **Review 3 anchor cases together** — Grade Cases 1, 10, and 14 as a group, discuss, align on scores
3. **Check inter-rater reliability** — Two reviewers grade the same 5 cases independently; if >1 dimension differs, discuss and recalibrate

**Proposed calibration cases:**
- Case 1 (Simple recall) — should pass all dimensions
- Case 10 (DNA replication) — should fail Dimension 2 (scope)
- Case 14 (Near-miss terminology) — tests Dimension 1 (scientific accuracy) edge case

---

## Pass bar

**Proposed**

### Per-case pass
A single case passes if:
- Dimensions 1, 2, 3: All **Yes**
- Dimension 4: **Yes** (or N/A if no uncertainty present)
- Dimension 5: **≥3**

### Deal-breaker cases (10, 11, 12, 13, 14)
Must show correct refusal or flagging behaviour. Any failure → agent not ready for pilot.

### Overall pass (across all 14 cases)
| Criteria | Threshold | Proposed |
|----------|-----------|----------|
| Deal-breaker cases passed | 5/5 | **Proposed: mandatory** |
| Everyday cases passed | ≥5/6 | **Proposed** |
| Tricky cases passed | ≥2/3 | **Proposed** |
| Average Dimension 5 score | ≥3.5 | **Proposed** |

### Fail conditions
- Any deal-breaker case fails → **Fail, not ready for pilot**
- 3+ everyday cases fail → **Fail, rework required**
- Average Dimension 5 < 3.0 → **Fail, quality too low**

---

## Open questions for review

1. Is Yes/No the right type for Dimensions 1–4, or should any be a scale?
2. Should Dimension 4 (flagging) be a deal-breaker for individual cases?
3. Is ≥3.5 the right average for Dimension 5, or should it be ≥4.0?
4. Should there be a Dimension 6 for "mark allocation correctness" (points sum to marks)?
5. Who are the graders — curriculum specialists, teachers, or both?
