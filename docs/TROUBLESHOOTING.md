# TutorTrap Troubleshooting

## `NameError: name 'GROQ_API_KEY' is not defined`

### Cause

You created an environment variable but did not assign its value to a Python variable.

### Fix

```python
GROQ_API_KEY = os.getenv("GROQ_API_KEY")
client = Groq(api_key=GROQ_API_KEY)
```

## Groq `400 BadRequestError` mentioning text classification models

### Symptom

```text
messages must contains a single user message for text classification models
```

### Cause

Model discovery selected a specialized classification/safety model instead of a generative chat model.

### Fix

Use an explicit generative model preference list and remove arbitrary substring matching:

```python
MODEL_PREFERENCES = [
    "llama-3.3-70b-versatile",
    "llama-3.1-8b-instant",
]
```

Then restart the notebook kernel and rerun model discovery.

## `cannot access local variable 'raw' where it is not associated with a value`

### Cause

The JSON parser's exception handler attempted to report `raw` before the first LLM call assigned it.

### Fix

Initialize:

```python
raw = ""
last_error = None
```

before the retry loop.

## Gradio `show_download_button` error

If you see:

```text
TypeError: Image.__init__() got an unexpected keyword argument 'show_download_button'
```

remove that constructor argument:

```python
progress_chart = gr.Image(label="Mastery by Concept")
```

## Gradio warning about `css` and `theme`

If Gradio says these parameters moved to `launch()`, use:

```python
with gr.Blocks(title="TutorTrap") as app:
    ...

app.launch(
    share=False,
    inbrowser=True,
    css=CUSTOM_CSS,
    theme=gr.themes.Soft()
)
```

## Claim-generation fallback appears repeatedly

First test the raw model directly:

```python
print(MODEL)

print(llm(
    "You are a helpful assistant.",
    "Reply with exactly: TutorTrap online.",
    temperature=0.1,
    max_tokens=20,
))
```

Then test `llm_json()` separately.

Do not debug the complete UI until the raw model and JSON helper both work.

## Wrong concept appears in fallback

Never use a single Gravity fallback for all concepts.

Store fallback claims by concept:

```python
CONCEPTS[concept]["fallback_claim"]
CONCEPTS[concept]["fallback_misconception"]
```

A failure while testing Momentum should not display a Gravity claim.

## Session state behaves strangely

Avoid mixing a global `SESSION` dictionary with `gr.State`.

Preferred design:

```text
Gradio session
     ↓
session_gr
     ↓
callbacks
     ↓
updated session state
```

Do not maintain the same logical session state in both a global mutable object and `gr.State`.

## Demo/API failure

The UI should fail gracefully. Prefer a controlled message such as:

> TutorTrap could not reach the language model. Please check the Groq configuration and retry.

Avoid exposing a Python traceback during the judge-facing demo.
