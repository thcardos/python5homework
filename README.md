## Pyhton Module 5
### Exercise 0: The Sealed Laboratory

This document provides a step-by-step checklist to test the project exercises during the peer evaluation.


#### Turn-in Files Verification

The subject strictly mandates checking that **only** the required files exist in the repository, with no residual virtual environments or untracked lock files.

```bash
ls -la ex0/
```

**Expected turn-in checklist:**
- [ ] `construct.py`
- [ ] `loading.py`
- [ ] `requirements.txt`
- [ ] `pyproject.toml`


#### Environment Isolation Verification (`construct.py`)

#### Scenario A: Global System Environment (Unsealed)

Ensure that no virtual environment is active in your current shell (run `deactivate` if needed):

```bash
python3 ex0/construct.py
```

* **Expected output:** The script detects that `sys.prefix == sys.base_prefix` and issues a warning stating that the laboratory is **not sealed** and that installing reagents directly into the global system is unsafe.

#### Scenario B: Sealed Laboratory (`venv`)

Create and activate a local virtual environment:

```bash
python3 -m venv lab_env
source lab_env/bin/activate
```

Run the script again:

```bash
python3 ex0/construct.py
```

* **Expected output:** The script confirms that the laboratory is **sealed**, displays the interpreter path pointing inside `lab_env/bin/python3`, and outputs the reagent directory (`site-packages`).


### Reagents Verification with `pip` and `requirements.txt`

Keep the `lab_env` environment active for this section:

#### Step 1: Execution before installing dependencies

```bash
python3 ex0/loading.py
```

* **Expected output:** The script gracefully handles missing third-party packages (`pandas`, `numpy`) by printing a clean informational warning without crashing or dumping an unhandled traceback (`ImportError` or `ModuleNotFoundError`).

#### Step 2: Install dependencies from requirements

```bash
pip install -r ex0/requirements.txt
```

#### Step 3: Execution after installation

```bash
python3 ex0/loading.py
```

* **Expected output:** Successfully loads the reagents, displays the required loading progress animation/indicator, and prints the detected package versions.


### Packaging and Dependency Management with Poetry (`pyproject.toml`)

Deactivate the previous virtual environment to verify Poetry independently:

```bash
deactivate
```

Navigate to `ex0` and install the environment managed by Poetry:

```bash
cd ex0
poetry install
```


> We set `package-mode = false` in `pyproject.toml` because this project uses Poetry strictly for dependency and environment management rather than packaging a distributable library for PyPI. This prevents Poetry from searching for a root package or an unnecessary `README.md` file."

#### Execution within the Poetry environment:

```bash
poetry run python loading.py
```

* **Expected output:** Poetry launches the script using its internal isolated environment and runs the loading sequence with all dependencies resolved.
