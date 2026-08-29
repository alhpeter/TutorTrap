# TutorTrap Setup Guide

## A. Local Jupyter/JupyterLab setup

### 1. Create an environment

```bash
python -m venv .venv
```

Activate it.

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
source .venv/bin/activate
```

### 2. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Set the Groq key

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

### 4. Start Jupyter

```bash
jupyter notebook
```

or:

```bash
jupyter lab
```

Open `TutorTrap.ipynb`.

## B. The correct API-key pattern

The common error is:

```text
NameError: name 'GROQ_API_KEY' is not defined
```

This occurs when the environment variable is set but the Python variable is not retrieved.

Use:

```python
import os
from groq import Groq

GROQ_API_KEY = os.getenv("GROQ_API_KEY")

if not GROQ_API_KEY:
    raise EnvironmentError("GROQ_API_KEY is missing.")

client = Groq(api_key=GROQ_API_KEY)
```

Do not expose the key with:

```python
print(GROQ_API_KEY)
```

A safe diagnostic is:

```python
print("API key loaded:", bool(GROQ_API_KEY))
```

## C. Model configuration

Use a small, explicit set of known generative models:

```python
MODEL_PREFERENCES = [
    "llama-3.3-70b-versatile",
    "llama-3.1-8b-instant",
]
```

Do not use a generic fallback such as:

```python
if "llama" in model_id:
    return model_id
```

Groq can expose specialized models that contain `llama` in their names but are not chat generation models.

## D. Gradio 6 compatibility

For Gradio 6-style APIs, keep CSS/theme at launch time:

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

For the image component, do not pass a removed constructor argument such as:

```python
show_download_button=False
```

Use:

```python
progress_chart = gr.Image(label="Mastery by Concept")
```

## E. Notebook execution order

Run cells in order. If you have modified imports, API configuration, model selection, or function definitions, restart the kernel and rerun the notebook from the top.

Recommended order:

1. Install dependencies
2. Imports
3. API configuration
4. Groq client
5. Model discovery
6. LLM helpers
7. Concept library
8. Learner model
9. AI components
10. Session state
11. Visualisation
12. Gradio UI
13. Smoke test

## F. Final pre-demo verification

Run:

```python
print("MODEL =", MODEL)
```

Then:

```python
test = llm(
    "You are a helpful assistant.",
    "Reply with exactly: TutorTrap online.",
    temperature=0.1,
    max_tokens=20,
)

print(test)
```

Expected:

```text
TutorTrap online.
```

Then test structured output:

```python
test_json = llm_json(
    "Return only valid JSON.",
    'Return {"status": "ok"}',
    ["status"],
    temperature=0.1,
)

print(test_json)
```

Expected:

```text
{'status': 'ok'}
```
