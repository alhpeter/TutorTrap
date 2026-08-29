# TutorTrap — Hackathon Slide Outline

Recommended deck: **6 slides**.

## Slide 1 — The hook

### TutorTrap
**Challenge the tutor. Reveal the misconception.**

**Speaker note:**

> “Most tutors can detect that an answer is wrong. TutorTrap tries to detect the mental model that produced the wrong answer.”

---

## Slide 2 — The problem

### A wrong answer is not a diagnosis

```text
Learner A → wrong for reason X
Learner B → wrong for reason Y

Traditional feedback → same generic explanation
```

**Speaker note:**

> “Two learners can produce the same wrong answer for completely different reasons.”

---

## Slide 3 — The TutorTrap loop

```text
Challenge
   ↓
Reason
   ↓
Diagnose
   ↓
Target
   ↓
Recover
```

**Speaker note:**

> “We deliberately introduce a plausible conceptual trap, inspect the learner's reasoning, target the resulting misconception, and test the learner again.”

---

## Slide 4 — What AI actually does

| AI | Python |
|---|---|
| Claim generation | Canonical truth |
| Reasoning analysis | Validation |
| Misconception diagnosis | Learner state |
| Targeted intervention | Mastery update |
| Recovery check | Session/UI |

**Speaker note:**

> “The LLM handles the semantic work. The learner model and ground truth remain transparent and inspectable.”

---

## Slide 5 — Live result

Show one before/after pair:

```text
MISCONCEPTION
      ↓
TARGETED QUESTION
      ↓
NEW EXPLANATION
      ↓
RECOVERY
```

Then show the learner-state change.

**Speaker note:**

> “The important result is not that the model generated text. The important result is that the learner reasoning changed after a targeted intervention.”

---

## Slide 6 — Why it matters

### TutorTrap closes the feedback loop

**Detect → Understand → Intervene → Verify**

**Closing line:**

> “TutorTrap doesn't just tell learners that they are wrong. It asks what they misunderstood, adapts the teaching, and checks whether they recovered.”
