# TutorTrap Submission Checklist

## Notebook

- [ ] `TutorTrap.ipynb` is included
- [ ] Notebook runs from top to bottom after a fresh kernel restart
- [ ] Dependencies install cleanly
- [ ] Groq API key is not embedded
- [ ] Model selection only chooses compatible generative chat models
- [ ] `llm()` works
- [ ] `llm_json()` works
- [ ] Claim generation works
- [ ] Claim validation works
- [ ] Reasoning diagnosis works
- [ ] Intervention generation works
- [ ] Recovery check works
- [ ] Learner state updates correctly
- [ ] Gradio UI launches
- [ ] Smoke test passes

## Product

- [ ] The educational problem is immediately understandable
- [ ] AI has a meaningful role
- [ ] Misconception is visible
- [ ] Intervention is visibly conditioned on the misconception
- [ ] Recovery is visibly checked
- [ ] Before/after state is visible

## Reliability

- [ ] Missing API key produces a helpful message
- [ ] API/model errors are caught
- [ ] Malformed JSON is handled
- [ ] Fallback claims are concept-specific
- [ ] UI does not expose raw tracebacks during the demo
- [ ] Session state is not unexpectedly global

## Repository

- [ ] `README.md`
- [ ] `requirements.txt`
- [ ] `.gitignore`
- [ ] `.env.example`
- [ ] `docs/`
- [ ] license added
- [ ] no secrets
- [ ] no unnecessary large files

## Demo

- [ ] 2-minute demo rehearsed
- [ ] first challenge prepared
- [ ] example misconception prepared
- [ ] corrected follow-up prepared
- [ ] backup path tested
- [ ] screenshots/video captured if required

## Final judge-facing message

> TutorTrap doesn't just detect that a learner is wrong — it identifies the misconception causing the error, targets that misconception, and checks whether the learner actually recovered.
