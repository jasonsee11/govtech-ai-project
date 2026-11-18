# Prompt chain

**Scenario:** C · MOE Biology Assessment
**Prototype today:** A clickable prototype to test whether teachers will trust and use AI-generated assessment questions.

All data is synthetic and labelled as made up.

## 1. Expand

**Prompt:** Enhance the existing assessment generator with an interactive review and refinement experience. Enable teachers to verify curriculum alignment, inspect supporting references, review marking schemes and customise individual questions without regenerating the entire assessment.

Preserve the existing prototype functionality and make the review process intuitive, with minimal additional workload for teachers.

**Business rules:**
- Every generated question must be mapped to a relevant curriculum learning outcome.
- Teachers can inspect the curriculum source and rationale for each question.
- Unverified or uncertain content must be clearly flagged.

**Edge cases:**
- The AI generates a scientifically plausible but incorrect answer.
- The question is scientifically accurate but outside the prescribed syllabus.
- The curriculum reference is missing, incorrect or cannot be verified.

**Result:** _fill in after you run it: what worked, what broke._

## 2. Behavior

**Prompt:** Enhance the existing prototype to handle AI failures, uncertain curriculum alignment and inaccurate assessment content.

Make failures visible, explain what went wrong and provide actionable recovery options. Allow teachers to continue working without losing their existing assessments or edits.

Add a clickable forced-failure scenario to the Trust Lab to demonstrate this behaviour.

**Forced failure:** Simulate a curriculum knowledge base retrieval failure when a teacher attempts to regenerate an individual assessment question. The AI cannot verify the relevant learning outcome. Instead of generating an unsupported question, the system explains the issue and offers the teacher three options: Retry, Edit Manually or Keep Original Question. All existing questions and teacher-made edits remain intact.

**Business rules:**
- Clearly communicate what failed, what could not be verified and what the teacher can do next.

**Edge cases:**
- The AI retrieves content from the wrong science strand or syllabus version.

**Result:** _fill in after you run it: what worked, what broke._

## 3. Refine

**Prompt:** Polish the existing prototype to deliver a cohesive, intuitive and professional teacher experience.

Simplify the user experience: Reduce unnecessary clicks, visual clutter and cognitive load. Make generating, verifying, refining and finalising assessments feel like a seamless workflow.

**Business rules:**
- Maintain consistent typography, spacing, colours and interaction patterns across all screens.
- Make primary actions prominent and secondary actions easily accessible.
- Minimise unnecessary clicks, information overload and repetitive confirmation steps.

**Edge cases:**
- The teacher has not selected any learning outcomes.
- The generated assessment contains lengthy questions or curriculum references that disrupt the layout.
- The teacher generates an assessment with many questions and needs to navigate between them easily.

**Result:** _fill in after you run it: what worked, what broke._
