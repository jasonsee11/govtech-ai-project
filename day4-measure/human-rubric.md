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

### Dimension 1: Scientific accuracy ⚠️ DEAL-BREAKER

**Proposed**

**Question:** Is the content scientifically correct at lower secondary level?

**Type:** Yes / No

| Answer | Meaning |
|--------|---------|
| Yes | All facts, terminology, and concepts are accurate |
| No | Contains one or more scientific errors |

**Deal-breaker:** ⚠️ YES — one wrong answer here fails the case

**Examples of No:**
- "Animal cells have a thin cell wall" (they have none)
- "Mitochondria produce energy" (energy is released/transferred, not produced)
- "Chloroplasts store genetic information" (that's the nucleus)

---

### Dimension 2: Curriculum scope ⚠️ DEAL-BREAKER

**Proposed**

**Question:** Is the content within lower secondary syllabus scope?

**Type:** Yes / No

| Answer | Meaning |
|--------|---------|
| Yes | Content matches current syllabus (2024 revision) for lower secondary |
| No | Contains upper secondary content, outdated syllabus content, or out-of-scope topics |

**Deal-breaker:** ⚠️ YES — one wrong answer here fails the case

**Examples of No:**
- DNA replication mechanism (upper secondary)
- Food tests like Benedict's solution (removed from 2024 syllabus)
- Detailed photosynthesis steps (upper secondary)

---

### Dimension 3: Source citation ⚠️ DEAL-BREAKER

**Proposed**

**Question:** Is a valid curriculum source cited?

**Type:** Yes / No

| Answer | Meaning |
|--------|---------|
| Yes | Cites a real document from the source hierarchy (Syllabus, Teaching Guide, etc.) |
| No | Source is missing, fabricated, or references wrong syllabus version |

**Deal-breaker:** ⚠️ YES — fabricated sources break trust

**Examples of No:**
- No source provided
- "MOE Syllabus 2024, Section 7.5" (Section 7.5 doesn't exist)
- Cites 2020 syllabus when 2024 is current

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
