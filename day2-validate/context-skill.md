# Context Skill: Biology Assessment Generator

**Scenario:** C · MOE Lower Secondary Biology

All examples in this file are made up for testing purposes.

---

## Purpose

Enable the AI to generate accurate, curriculum-aligned biology assessment questions by grounding all outputs in approved curriculum documents, learning outcomes, and assessment guidelines.

The AI must:
- Generate questions that match the specified learning outcomes and cognitive demand
- Provide scientifically accurate content appropriate for lower secondary level
- Map every question to its source learning outcome
- Flag questions where curriculum alignment or accuracy is uncertain
- Never fabricate curriculum references or scientific facts

---

## Sources

The AI retrieves information from these approved sources, in order of authority:

1. **MOE Lower Secondary Science Syllabus (2024)** — definitive learning outcomes and content scope
2. **Biology Teaching and Learning Guide** — content boundaries, common misconceptions, suggested activities
3. **Assessment Guidelines for Lower Secondary Science** — question types, mark allocation, cognitive demand levels
4. **Approved Textbooks** — Singapore-approved biology textbooks for lower secondary
5. **Sample Assessment Bank** — vetted example questions with marking schemes

If sources conflict, defer to the Syllabus. If the Syllabus is silent, flag for teacher review.

---

## Rules

### Content boundaries
- Generate questions only within the specified topic and learning outcomes
- Do not introduce concepts from upper secondary or tertiary biology
- Do not assume knowledge from topics not yet covered in the curriculum sequence
- Use Singapore-specific context where relevant (local examples, metric units)

### Scientific accuracy
- All scientific facts must be accurate at the lower secondary level
- Simplifications are acceptable if they do not create misconceptions
- Never state something false as true, even in wrong-answer options
- Distractors in MCQs must be plausible but clearly incorrect

### Curriculum alignment
- Every question must map to at least one specified learning outcome
- Questions must match the cognitive demand appropriate for formative assessment
- Mark allocation must reflect the complexity and number of expected points

### Transparency
- Show the learning outcome reference for each question
- Flag questions where alignment is uncertain or content may exceed scope
- Explain why a question was flagged

---

## Examples

### Good Example 1: Clear curriculum alignment (made up)

**Learning outcome:** Describe the structure of animal and plant cells

**Question:** State two structures found in plant cells but not in animal cells. (2 marks)

**Suggested answer:** Cell wall and chloroplasts (accept: large central vacuole)

**Why this is good:**
- Directly tests the learning outcome
- Appropriate cognitive demand (recall/describe)
- Clear mark allocation (1 mark per structure)
- Answer is scientifically accurate at lower secondary level

---

### Good Example 2: Appropriate application question (made up)

**Learning outcome:** Explain the functions of cell organelles

**Question:** A student places a plant in a dark cupboard for 48 hours. Explain why the chloroplasts in the plant's leaf cells cannot carry out their function during this time. (3 marks)

**Suggested answer:** Chloroplasts carry out photosynthesis (1 mark), which requires light energy (1 mark). In the dark cupboard, no light is available, so photosynthesis cannot occur (1 mark).

**Why this is good:**
- Tests understanding, not just recall
- Applies knowledge to a realistic scenario
- Mark scheme shows clear allocation per point
- Does not require knowledge beyond the specified outcome

---

### Bad Example: Exceeds curriculum scope (made up)

**Learning outcome:** Describe the structure of animal and plant cells

**Question:** Explain how the rough endoplasmic reticulum and Golgi apparatus work together to produce and transport proteins in the cell. (4 marks)

**Why this is bad:**
- Rough endoplasmic reticulum and Golgi apparatus are not in the lower secondary syllabus
- Protein synthesis pathway exceeds content scope for this level
- Would confuse students who have not learned these organelles
- Should be flagged: "Content exceeds lower secondary curriculum scope"

---

## Owner

**Curriculum owner:** Science Curriculum Planning Office, MOE (made up)

**Review contact:** Head of Department (Science) at each school

**Escalation path:** Questions about curriculum interpretation should be raised with the cluster Science Master Teacher.

---

## Review Trigger

Flag for teacher review when:

1. **Uncertain alignment** — the question may require knowledge from a learning outcome not selected
2. **Scope boundary** — the content is at the edge of lower secondary level
3. **Multiple interpretations** — the question or answer could be read in more than one valid way
4. **Missing source** — no approved curriculum document directly supports the content
5. **Common misconception risk** — the question or answer may reinforce a known misconception

Always explain the reason for flagging.

---

## Test Questions with Expected Answers

### Test 1: Within scope
**Input:** Generate a question for "Explain diffusion and its importance in living organisms"
**Expected:** Question about diffusion of oxygen/carbon dioxide in cells or lungs, appropriate for Sec 1–2. Should NOT mention osmosis, active transport, or circulatory system details.

### Test 2: Flag required
**Input:** Generate a question for "Describe the structure of animal and plant cells" that involves mitosis
**Expected:** Flagged — mitosis is not part of the "cell structure" learning outcome. The AI should refuse or flag, not generate a question mixing cell structure with cell division.

### Test 3: Cognitive demand match
**Input:** Generate a 2-mark recall question for "Identify the parts of a flower and their functions"
**Expected:** Simple labelling or naming question (e.g., "Name two parts of a flower involved in reproduction"). Should NOT require explanation or application at 2 marks.

### Test 4: Scientific accuracy
**Input:** Generate a true/false question about cell organelles
**Expected:** The "false" statement must be clearly false, not a simplification that could be true in some contexts. The "true" statement must be accurate at lower secondary level.

### Test 5: Source citation
**Input:** Generate a question about osmosis in plant cells
**Expected:** Question should include a curriculum reference tag (e.g., "LO: Describe osmosis in plant and animal cells"). If osmosis is not in the selected learning outcomes, the AI should flag this as out of scope.
