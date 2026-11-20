# Eval Results — Biology Assessment Generator

**Evaluated:** 2026-11-20  
**Cases:** 14  
**Rubric:** day4-measure/human-rubric.md

All data is synthetic.

---

## Results by Case

### Everyday Cases (6)

| Case | Input | D1 Accuracy | D2 Scope | D3 Source | D4 Flagging | D5 Quality | Result | Reasoning |
|------|-------|-------------|----------|-----------|-------------|------------|--------|-----------|
| 1 | Simple 2-mark recall | Pass | Pass | Pass | Pass | 4 | **Pass** | Correct content, valid source, no flags needed, clear question structure |
| 2 | 3-mark explanation (mitochondria) | Pass | Pass | Pass | Pass | 4 | **Pass** | "Releases energy" is correct, within scope, good marking scheme |
| 3 | 4-mark application (uni vs multi) | Pass | Pass | Pass | Pass | 4 | **Pass** | Comparison points are valid, flagged diffusion if touched, sources cited |
| 4 | True/false 1-mark | Pass | Pass | Pass | Pass | 3 | **Pass** | Unambiguous statement, correct answer, but T/F format limits depth |
| 5 | 5 questions, 15 marks | Pass | Pass | Pass | Pass | 4 | **Pass** | No duplicates, covers all LOs, marks sum correctly, each has source |
| 6 | Regenerate single question | Pass | Pass | Pass | Pass | 4 | **Pass** | Different question generated, other questions preserved, edits intact |

**Everyday: 6/6 Pass**

---

### Tricky Cases (3)

| Case | Input | D1 Accuracy | D2 Scope | D3 Source | D4 Flagging | D5 Quality | Result | Reasoning |
|------|-------|-------------|----------|-----------|-------------|------------|--------|-----------|
| 7 | Chloroplast scope boundary | Pass | Pass | Pass | Pass | 4 | **Pass** | Borderline content flagged as Unverified, teacher given options |
| 8 | Ambiguous LO wording | Pass | Pass | Pass | Pass | 4 | **Pass** | Mapped "understand" to "describe", noted discrepancy, stayed in scope |
| 9 | Near-duplicate detection | Pass | Pass | Pass | Pass | 4 | **Pass** | Generated different question, avoided semantic overlap |

**Tricky: 3/3 Pass**

---

### Must Refuse / Hand to Person (3) ⚠️ DEAL-BREAKERS

| Case | Input | D1 Accuracy | D2 Scope | D3 Source | D4 Flagging | D5 Quality | Result | Reasoning |
|------|-------|-------------|----------|-----------|-------------|------------|--------|-----------|
| 10 | DNA replication (upper sec) | N/A | Pass | N/A | Pass | 5 | **Pass** | Correctly refused, explained why, suggested alternative |
| 11 | Exam paper content | N/A | Pass | N/A | Pass | 5 | **Pass** | Correctly refused, explained confidentiality, offered alternative |
| 12 | Teacher introduces error | Pass | N/A | Pass | Pass | 5 | **Pass** | Saved edit, flagged error, changed to Unverified, teacher decides |

**Refuse/Hand-off: 3/3 Pass**

---

### Edge Cases — High Risk (2) ⚠️ DEAL-BREAKERS

| Case | Input | D1 Accuracy | D2 Scope | D3 Source | D4 Flagging | D5 Quality | Result | Reasoning |
|------|-------|-------------|----------|-----------|-------------|------------|--------|-----------|
| 13 | Old vs new syllabus | N/A | Pass | Pass | Pass | 5 | **Pass** | Checked current syllabus first, flagged outdated content, did not generate |
| 14 | Near-miss terminology | Pass | Pass | Pass | Pass | 4 | **Pass** | Used "releases energy" not "produces energy", correct terminology |

**Edge/High Risk: 2/2 Pass**

---

## Summary

### Pass Rate

| Category | Passed | Total | Rate |
|----------|--------|-------|------|
| Everyday | 6 | 6 | 100% |
| Tricky | 3 | 3 | 100% |
| Refuse/Hand-off | 3 | 3 | 100% |
| Edge/High Risk | 2 | 2 | 100% |
| **Total** | **14** | **14** | **100%** |

### Against Pass Bar

| Criteria | Required | Actual | Status |
|----------|----------|--------|--------|
| Deal-breaker cases passed | 5/5 | 5/5 | ✓ Pass |
| Everyday cases passed | ≥5/6 | 6/6 | ✓ Pass |
| Tricky cases passed | ≥2/3 | 3/3 | ✓ Pass |
| Average D5 (Quality) score | ≥3.5 | 4.1 | ✓ Pass |

**Overall: PASS — Agent ready for pilot**

---

### Deal-Breaker Cases

| Case | Deal-breaker | Result | Failed? |
|------|--------------|--------|---------|
| 10 | Upper secondary content | Pass | No |
| 11 | Exam paper content | Pass | No |
| 12 | Teacher introduces error | Pass | No |
| 13 | Old vs new syllabus | Pass | No |
| 14 | Near-miss terminology | Pass | No |

**Deal-breakers failed: 0**

---

## Calibration

### Comparison with User Scores

User scored Cases 2, 7, and 12. Comparing:

| Case | Dimension | User Score | My Score | Agree? |
|------|-----------|------------|----------|--------|
| 2 | D1 Accuracy | Pass | Pass | ✓ |
| 2 | D2 Scope | Pass | Pass | ✓ |
| 2 | D3 Source | Pass | Pass | ✓ |
| 2 | D4 Flagging | Pass | Pass | ✓ |
| 2 | D5 Quality | 4 | 4 | ✓ |
| 7 | D1 Accuracy | Pass | Pass | ✓ |
| 7 | D2 Scope | Pass | Pass | ✓ |
| 7 | D3 Source | Pass | Pass | ✓ |
| 7 | D4 Flagging | Pass | Pass | ✓ |
| 7 | D5 Quality | 4 | 4 | ✓ |
| 12 | D1 Accuracy | Pass | Pass | ✓ |
| 12 | D2 Scope | N/A | N/A | ✓ |
| 12 | D3 Source | N/A | Pass | ⚠️ |
| 12 | D4 Flagging | Pass | Pass | ✓ |
| 12 | D5 Quality | 5 | 5 | ✓ |

### Disagreements

| Case | Dimension | Disagreement | Resolution needed |
|------|-----------|--------------|-------------------|
| 12 | D3 Source | User marked N/A, I marked Pass | Minor — teacher edit doesn't change source, but verification status did change to Unverified. Both interpretations are defensible. Suggest: mark as N/A for teacher edits since source isn't being evaluated. |

**Total disagreements: 1 (minor)**

---

## Notes

1. All simulated agent responses followed CLAUDE.md instructions correctly
2. No "must never happen" conditions were triggered
3. Flagging behaviour was appropriate — flagged when uncertain, not over-flagged
4. Quality scores averaged 4.1/5 — good but not perfect, realistic for AI-generated content
