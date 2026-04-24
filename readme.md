# Anthropic course examples

Jupyter notebooks for working through Anthropic API examples. This repo expects a local Python virtual environment (`.venv`), a Jupyter kernel pointed at that environment, and an API key in `.env`.

## VS Code / Cursor: Jupyter extensions

Install these extensions so notebooks open and run cleanly in the editor:

| Extension | ID (for CLI) | Purpose |
|-----------|----------------|---------|
| **Jupyter** | `ms-toolsai.jupyter` | Notebook UI, kernels, run cells |
| **Python** | `ms-python.python` | Interpreter selection, debugging, IntelliSense |

**From the command line** (with `code` or `cursor` on your `PATH`):

```bash
cursor --install-extension ms-toolsai.jupyter
cursor --install-extension ms-python.python
```

Replace `cursor` with `code` if you use VS Code.

After opening a notebook, choose the kernel that matches this project’s `.venv` (**Python: Select Interpreter** → pick `.venv/bin/python`, then pick the same interpreter as the notebook kernel).

## Environment variables (`.env`)

Create a file named `.env` in the **repository root** (same folder as the notebooks). `.env*` is gitignored so secrets are not committed.

**Minimum content:**

```env
ANTHROPIC_API_KEY=sk-ant-api03-...
```

Get a key from the [Anthropic Console](https://console.anthropic.com/). The notebooks use `python-dotenv` and `load_dotenv()` so variables in `.env` are loaded when cells run.

## Python virtual environment (`.venv`)

Run these from the repository root (`Antropic-course-examples`).

### 1. Create the virtual environment

```bash
python3 -m venv .venv
```

### 2. Activate it

**macOS / Linux (zsh/bash):**

```bash
source .venv/bin/activate
```

**Windows (cmd):**

```cmd
.venv\Scripts\activate.bat
```

**Windows (PowerShell):**

```powershell
.venv\Scripts\Activate.ps1
```

### 3. Install packages (API client, dotenv, Jupyter tooling)

```bash
python -m pip install --upgrade pip
pip install anthropic python-dotenv ipykernel jupyter
```

(`anthropic` and `python-dotenv` match the notebooks; `ipykernel` and `jupyter` register and run the kernel.)

### 4. Register a Jupyter kernel for this venv

Still with `.venv` activated:

```bash
python -m ipykernel install --user --name=antropic-course-examples --display-name="Python (antropic-course-examples)"
```

In VS Code / Cursor, open a `.ipynb` file and select the kernel **Python (antropic-course-examples)**.

### 5. (Optional) One-shot verification

```bash
python -c "from dotenv import load_dotenv; import os; load_dotenv(); print('ANTHROPIC_API_KEY set:', bool(os.getenv('ANTHROPIC_API_KEY')))"
```

You should see `ANTHROPIC_API_KEY set: True` after `.env` is filled in.

## Quick reference (copy-paste, macOS/Linux)

```bash
cd /path/to/Antropic-course-examples
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install anthropic python-dotenv ipykernel jupyter
python -m ipykernel install --user --name=antropic-course-examples --display-name="Python (antropic-course-examples)"
```

Then create `.env` with `ANTHROPIC_API_KEY=...`, install the Jupyter + Python extensions above, open a notebook, and select the **Python (antropic-course-examples)** kernel.
