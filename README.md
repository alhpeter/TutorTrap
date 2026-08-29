# 🪤 TutorTrap

## Challenge the tutor. Reveal the misconception.

TutorTrap is a compact AI-powered diagnostic learning experience for introductory physics.

Instead of stopping at **right/wrong**, TutorTrap asks a more useful question:

> **What misconception caused the learner to reason that way — and did the intervention actually change it?**

The prototype creates a plausible but incorrect physics claim, asks the learner to reason about it, diagnoses the underlying misconception from their natural-language explanation, generates a targeted follow-up challenge, and checks whether the learner's reasoning recovers.

## Notion
[https://app.notion.com/p/TutorTrap-3cb62c13fa84809fb251f44c9c804224?source=copy_link](https://season-shrimp-22c.notion.site/TutorTrap-3cb62c13fa84809fb251f44c9c804224?pvs=73)

## Video
https://vimeo.com/1222289326?share=copy&fl=sv&fe=ci

### The core loop

```text
Canonical concept truth
        ↓
AI Claim Generator
        ↓
AI Claim Validator
        ↓
Learner reasoning
        ↓
AI Reasoning Diagnostician
        ↓
AI Targeted Intervention
        ↓
Learner follow-up
        ↓
AI Recovery Check
        ↓
Transparent Learner Model Update
```

## Why TutorTrap?

Many educational systems can tell a learner that an answer is incorrect. That does not necessarily reveal the learner's mental model.

For example, two learners can both believe that a heavy object falls faster, but for different reasons. One may think gravity is stronger on heavier objects; another may confuse force with acceleration. Treating both as the same simple error can lead to a generic explanation that does not address the real reasoning problem.

TutorTrap makes the **misconception** the unit of adaptation.

### What the learner experiences

1. A tutor presents a plausible but incorrect claim.
2. The learner agrees/disagrees and explains why.
3. TutorTrap identifies the reasoning pattern and names the misconception.
4. TutorTrap creates a follow-up specifically aimed at that misconception.
5. The learner answers again.
6. TutorTrap checks whether the misconception appears resolved, partially improved, or persistent.
7. The learner model updates transparently.

## What is genuinely AI-driven?

TutorTrap is intentionally explicit about its AI/ML boundary.

### Generative AI handles

- misconception-oriented claim generation,
- natural-language reasoning analysis,
- misconception diagnosis,
- targeted intervention generation,
- recovery evaluation.

### Python handles

- canonical concept truth,
- claim validation plumbing and safety checks,
- learner-state bookkeeping,
- mastery updates,
- misconception history,
- session state,
- UI orchestration,
- error handling.

The learner model is **transparent adaptive logic**, not a black-box predictive ML model. This is deliberate: judges can inspect exactly how the learner state changes.

## Technology

- Python
- Groq API
- Groq generative chat model
- Gradio
- Matplotlib
- Jupyter Notebook / JupyterLab
- Transparent Python learner model

## Repository structure

```text
TutorTrap/
├── TutorTrap.ipynb
├── README.md
├── requirements.txt
├── .env.example
├── .gitignore
└── docs/
    ├── DEMO_SCRIPT.md
    ├── SETUP.md
    ├── NOTION_TEMPLATE.md
    ├── HACKATHON_SLIDES.md
    ├── ARCHITECTURE.md
    ├── SUBMISSION_CHECKLIST.md
    └── TROUBLESHOOTING.md
```

The notebook remains the primary executable artifact.

## Quick start

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

Or run the notebook's installation cell.

### 2. Configure Groq

Set the API key in your local environment. Do not commit the key.

Windows PowerShell:

```powershell
$env:GROQ_API_KEY="gsk_your_key_here"
```

Windows Command Prompt:

```cmd
set GROQ_API_KEY=gsk_your_key_here
```

macOS/Linux:

```bash
export GROQ_API_KEY="gsk_your_key_here"
```

Then, in Python:

```python
import os
from groq import Groq

GROQ_API_KEY = os.getenv("GROQ_API_KEY")

if not GROQ_API_KEY:
    raise EnvironmentError("GROQ_API_KEY is not configured.")

client = Groq(api_key=GROQ_API_KEY)
```

**Important:** `os.environ["GROQ_API_KEY"] = ...` creates an environment variable; it does not create a Python variable called `GROQ_API_KEY`. Retrieve it with `os.getenv()` before passing it to `Groq()`.

### 3. Run `TutorTrap.ipynb`

Run the notebook from top to bottom.

The recommended order is:

```text
Install → Imports/Config → Model → Concepts → Learner Model → AI Components → Session → UI → Smoke Test
```

### 4. Launch the interface

The final notebook cell launches Gradio locally.

## Recommended Groq model strategy

TutorTrap should select from known generative chat models rather than arbitrarily choosing any model whose name contains `llama`, `gemma`, or `mixtral`.

A safe preference list for the current notebook pattern is:

```python
MODEL_PREFERENCES = [
    "llama-3.3-70b-versatile",
    "llama-3.1-8b-instant",
]
```

This avoids accidentally selecting a specialized classification or safety model that cannot accept the notebook's chat-message structure.

## Demo scenario

The cleanest first demo uses **Gravity & Falling Objects**.

Example trap:

> “A heavier object falls faster than a lighter object because gravity pulls harder on it.”

Example learner reasoning:

> “I agree because heavier objects have more mass, so gravity pulls them harder, making them accelerate faster.”

TutorTrap should surface the misconception around conflating greater gravitational force with greater acceleration, then produce a targeted challenge.

The strongest final moment is the recovery check:

```text
Misconception detected
        ↓
Targeted intervention
        ↓
New reasoning
        ↓
Recovery detected
```

## Design principles

### 1. The AI is central, but not trusted as ground truth

The LLM generates and interprets language. The canonical physics truth stays in Python.

### 2. The system adapts around misconceptions

The intervention is generated from the diagnosed misconception rather than being a fixed explanation for every learner.

### 3. Recovery is measured

The demo does not end when the learner receives an explanation. A second response is used to estimate whether the misconception changed.

### 4. Keep the prototype small

TutorTrap intentionally avoids accounts, databases, authentication, large LMS features, and unnecessary deployment infrastructure. The core educational loop is the product.

## Reliability and fallbacks

The notebook should gracefully handle:

- missing API keys,
- unavailable models,
- transient API failures,
- malformed JSON responses,
- empty learner responses.

Fallback claims should remain **concept-specific**. A failure on Momentum must never fall back to a Gravity claim.

## Security

Never commit:

- `.env` files containing real keys,
- API keys in notebook cells,
- access tokens,
- personal learner data.

Use `.env.example` only as a template.

## Demo message

A strong one-line description for judges is:

> **TutorTrap doesn't just detect that a learner is wrong — it identifies the misconception causing the error, targets that misconception, and checks whether the learner actually recovered.**

## Status

Hackathon-ready prototype / single-notebook educational system.
