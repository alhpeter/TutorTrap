# TutorTrap Architecture

## System boundary

TutorTrap is intentionally a single-notebook prototype. The notebook contains the application logic, AI orchestration, adaptive state, and Gradio interface.

## Components

### Canonical concept library

Python-owned educational truth. Each concept contains:

- canonical truth,
- common misconception seeds,
- concept-specific fallback content.

### Claim generator

The LLM creates a concise, plausible, incorrect claim rooted in the concept and misconception seeds.

### Claim validator

The generated claim is evaluated against the canonical concept before being shown to the learner.

### Reasoning diagnostician

The LLM analyzes the learner's natural-language explanation and returns structured fields such as:

- correctness,
- misconception,
- evidence,
- confidence,
- diagnosis,
- estimated mastery.

### Intervention generator

The LLM generates a follow-up question conditioned on the diagnosed misconception.

### Recovery checker

The learner answers the targeted follow-up. The LLM evaluates whether the original misconception is resolved, partial, or persistent.

### Adaptive learner model

Transparent Python logic updates:

- mastery,
- misconception history,
- misconception confidence,
- attempts,
- resolution state.

### Gradio interface

The UI presents the learning loop as a progressive sequence rather than as a generic chat window.

## Trust model

```text
Canonical Truth ───────────────┐
                               │
                               ▼
LLM generation → validation → learner
                               │
                               ▼
                         LLM diagnosis
                               │
                               ▼
                      targeted intervention
                               │
                               ▼
                         recovery check
                               │
                               ▼
                        learner state
```

The LLM is powerful but not treated as the sole source of truth.

## State model

Avoid having one logical state represented in both a global mutable variable and `gr.State`.

Preferred model:

```text
learner_gr
session_gr
   ↓
callback
   ↓
updated state
```

This is safer for multiple Gradio sessions and easier to reason about.
