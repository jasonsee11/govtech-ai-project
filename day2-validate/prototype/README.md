# Biology Assessment Generator Prototype

A clickable prototype to test whether teachers will trust and use AI-generated assessment questions.

## What it does

1. **Select topic and learning outcomes** — Teacher picks a biology topic and 1–3 learning outcomes
2. **Review generated questions** — 5 sample questions appear with suggested answers, marking schemes, and curriculum references
3. **Decide on each question** — Keep, Edit, or Reject buttons for every question
4. **See retention summary** — After all decisions, shows how many questions were kept vs rejected

## Trust Lab (for testers)

A collapsible panel at the top with four test scenarios:

| Scenario | What it tests |
|----------|---------------|
| **Black Box** | Shows WHY AI selected each question |
| **Hallucination** | Contains 2 planted errors — can you spot them? |
| **Control** | Demonstrates edit and regenerate capabilities |
| **AI Uncertainty** | Shows how AI flags uncertain alignment |

**Testing features:**
- Toggle curriculum references on/off
- Reveal planted errors to check detection
- Auto-captured metrics: retention rate, errors caught, review time, confidence
- Copy results to clipboard for sharing

## How to run

Open `index.html` in a browser. No build step required.

## Limitations

- Only "Cells and Organisation" topic has sample questions
- Questions are pre-written, not AI-generated
- Edit and Regenerate buttons show placeholders only
- All data is synthetic

## What we're testing

**Riskiest assumption:** Teachers will trust AI-generated questions enough to use them rather than starting from scratch.

**Success signal:** ≥70% of questions retained with minor or no edits.

**Kill signal:** <50% retention, or teachers miss >5% of planted errors.
