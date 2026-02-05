# Using `uv` Package Manager on Ubuntu 24.04

A practical, reproducible guide for installing and using **`uv`**, the ultra-fast Python package manager by Astral, on **Ubuntu 24.04**.

---

## 1. What is `uv`

`uv` is a modern, Rust-based Python package manager that acts as a fast replacement for:

* `pip`
* `pip-tools`
* `virtualenv`

### Key advantages

* ⚡ Extremely fast dependency resolution
* 🔒 Deterministic, reproducible installs
* 🧩 Single self-contained binary
* 🛡️ Safer than system `pip` on Ubuntu

---

## 2. Install `uv` on Ubuntu 24.04

### Official installer (recommended)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

This installs `uv` to:

```text
~/.local/bin/uv
```

### Ensure `uv` is on your PATH

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Verify installation:

```bash
uv --version
```

---

## 3. Create a Virtual Environment

### Create a project virtual environment

```bash
uv venv
```

This creates:

```text
.venv/
```

### (Optional) Activate the environment

```bash
source .venv/bin/activate
```

> Activation is optional when using `uv run`.

---

## 4. Install Packages (pip replacement)

### Install a single package

```bash
uv pip install numpy
```

### Install multiple packages

```bash
uv pip install numpy pandas matplotlib
```

### Install from `requirements.txt`

```bash
uv pip install -r requirements.txt
```

### Freeze installed packages

```bash
uv pip freeze > requirements.txt
```

---

## 5. Dependency Locking (pip-tools replacement)

### Compile dependencies from `pyproject.toml`

```bash
uv pip compile pyproject.toml -o requirements.txt
```

### Compile from `requirements.in`

```bash
uv pip compile requirements.in -o requirements.txt
```

### Install locked dependencies

```bash
uv pip install -r requirements.txt
```

---

## 6. Run Python Without Activating the venv (Recommended)

You can safely run Python commands without activating `.venv`.

```bash
uv run python script.py
```

Example:

```bash
uv run python train.py
```

This guarantees the correct virtual environment is used.

---

## 7. Python Version Management (Optional)

### Install a specific Python version

```bash
uv python install 3.11
```

### Create a venv with a specific Python version

```bash
uv venv --python 3.11
```

### List installed Python versions

```bash
uv python list
```

---

## 8. Recommended Project Workflow

```bash
mkdir myproject && cd myproject

uv venv
uv pip install fastapi uvicorn

uv run uvicorn main:app --reload
```

---

## 9. Ubuntu 24.04 System Safety Notes

* ❌ Do **not** use system `pip`
* ✔️ Always install packages inside `.venv`
* ✔️ `uv` avoids breaking `apt`-managed Python packages

This makes `uv` safer than traditional `pip` on Ubuntu.

---

## 10. Command Cheat Sheet

| Task              | Command                  |
| ----------------- | ------------------------ |
| Create venv       | `uv venv`                |
| Install package   | `uv pip install <pkg>`   |
| Run script        | `uv run python app.py`   |
| Lock dependencies | `uv pip compile`         |
| Install Python    | `uv python install 3.11` |

---

## 11. Recommended Use Cases

`uv` is particularly effective for:

* Machine Learning / PyTorch projects
* Research and reproducible experiments
* FastAPI backends
* CI/CD pipelines
* MLOps workflows

---

**Last updated:** Ubuntu 24.04
