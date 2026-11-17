# AI user flow: A lower secondary science teacher preparing for the revised biology curriculum selects the intended learning outcomes and generates a draft assessment, complete with questions, suggested answers, marking schemes and curriculum references. The teacher can confidently decide what to accept, refine or reject.

**Scenario:** C · MOE lower secondary biology

All data in this file is synthetic.

## The moment

A lower secondary science teacher preparing for the revised biology curriculum selects the intended learning outcomes and generates a draft assessment, complete with questions, suggested answers, marking schemes and curriculum references. The teacher can confidently decide what to accept, refine or reject.

## The iceberg

### Above the line: what the user sees

Selection of biology topics, learning outcomes, question types, difficulty levels and total marks.

A generated assessment with suggested answers and marking schemes.

Curriculum learning outcomes and supporting source references alongside each question.

Indicators highlighting uncertainties or potential curriculum misalignment.

Edit, Regenerate, Replace and Restore Previous Version buttons for individual questions.

A final review and approval step before exporting the assessment.

### Below the line

- Data: Approved MOE biology curriculum documents, learning outcomes, teaching resources, assessment guidelines and synthetic sample questions.
- Model: A language model that generates assessment questions and marking schemes grounded in approved curriculum resources.
- Rules: Respect curriculum content boundaries, student level and science strand. Never fabricate curriculum references. Protect student data and confidential assessment materials. Require teacher approval before use with students.
- Handoffs: Questions with uncertain curriculum alignment or scientific accuracy are flagged for teacher review. Unresolved curriculum ambiguities may require clarification from a curriculum specialist.

## The flow

1. **Trigger:** A teacher needs to prepare a formative assessment for the revised biology curriculum. The teacher selects the topic, learning outcomes and assessment requirements.
   - Trust gap: Control. The teacher cannot specify the learning outcomes, difficulty or assessment requirements.
2. **AI step:** The AI generates assessment questions, suggested answers and marking schemes, mapping each question to relevant curriculum learning outcomes.
   - Trust gap: Black box. The teacher does not understand why the AI selected certain questions or determined their cognitive demand.
3. **Human check:** The teacher reviews the generated assessment, checks curriculum alignment, and edits, replaces or regenerates individual questions.
   - Trust gap: Hallucination. The teacher cannot easily distinguish scientifically accurate and curriculum-aligned content from plausible but incorrect AI-generated content.
4. **Outcome:** The teacher approves and exports the final assessment for use with students.
   - Trust gap: Control. The teacher cannot easily adjust the final assessment to suit the learning needs of their students, such as changing question difficulty, rewording questions, adjusting mark allocations or replacing individual questions without regenerating the entire assessment.

## Fallback when the AI is unsure (Advanced)

When the AI is unable to confidently establish accuracy or curriculum alignment, it should:
- Flag the affected questions and explain what it is uncertain about.
- Surface the closest relevant curriculum references to support teacher verification.
- Allow the teacher to manually edit, remove or regenerate the affected questions without changing the rest of the assessment.
- If authoritative curriculum sources are unavailable, refrain from generating questions and ask the teacher to provide the relevant curriculum materials.
The teacher should still be able to continue working on the rest of the assessment.

## How we measure trust (Expert)

- Question retention rate: At least 70% of AI-generated questions are retained with no or minor edits.
- Teacher confidence: At least 85% of teachers feel confident in their ability to verify the scientific accuracy and curriculum alignment of generated questions.
- Perceived control: At least 90% of teachers feel they can easily customise assessments to suit their students' learning needs.
- Repeat usage rate: At least 80% of teachers voluntarily return to the tool to create another assessment.
- Appropriate rejection rate: At least 95% of deliberately introduced inaccurate questions are correctly identified and rejected by teachers during controlled testing.
