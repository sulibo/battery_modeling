# Battery Modeling Task - Lithium Plating Analysis

**Author:** Libo Su (libo.su@outlook.com)

**Date:** November 23, 2025

## Task Description

This project simulates and analyzes lithium plating risk in a lithium-ion battery during a fast charging sequence. The task involves:

1. **Simulating a continuous charge sequence**:

   - 1C charge until 50% SOC (State of Charge)
   - Immediately apply a 5C pulse for 10 seconds
   - Followed by a rest period
2. **Analyzing lithium plating risk**:

   - Monitor anode potential during the charging sequence
   - Detect if the anode potential drops below 0 V vs. Li/Li+ reference (plating threshold)
   - Analyze the timing and duration of plating risk

### Key Results

- **Model**: Doyle-Fuller-Newman (DFN) model is used for accurate electrode potential predictions
- **Finding**: Plating risk is detected during the rest period (approximately 9.76 seconds after the pulse ends) and persists for ~590 seconds
- **Analysis Variables**:
  - SOC calculation: `X-averaged negative electrode extent of lithiation`
  - Plating analysis: `X-averaged negative electrode potential`

## Prerequisites

- Python 3.12
- `uv` package manager (installation instructions below)

## Setup Instructions

### 1. Install uv

`uv` is a fast Python package installer and resolver written in Rust. Install it using one of the following methods:

**Linux/macOS:**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows (PowerShell):**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Or if you're already in PowerShell:

```powershell
irm https://astral.sh/uv/install.ps1 | iex
```

**Alternative methods:**

- Using pip: `pip install uv`
- Using homebrew (Mac): `brew install uv`

After installation, restart your terminal and verify with:

```bash
uv --version
```

### 2. Set Up Virtual Environment

Create a virtual environment and install dependencies using `uv`:

```bash
# Sync dependencies from pyproject.toml
uv sync
```

This will:

- Create a virtual environment in `.venv/`
- Install PyBaMM and all required dependencies

### 3. Activate Virtual Environment

**Linux/macOS:**

```bash
source .venv/bin/activate
```

**Windows (PowerShell):**

```powershell
.venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**

```cmd
.venv\Scripts\activate.bat
```

Alternatively, you can use `uv run` to execute commands in the virtual environment without manual activation:

```bash
uv run python your_script.py
```

## Running the Jupyter Notebook

### Option 1: Using uv run (Recommended)

```bash

# Launch Jupyter Notebook
uv run jupyter notebook

# Or launch JupyterLab
uv run jupyter lab
```

### Option 2: With Activated Virtual Environment

1. Activate the virtual environment (see step 3 above)
2. Launch Jupyter:
   ```bash
   jupyter notebook
   # or
   jupyter lab
   ```
4. Open `solution_notebook.ipynb` from the Jupyter interface

## Project Structure

```
Battronics/
├── README.md                 # This file
├── pyproject.toml            # Project dependencies configuration
├── .python-version           # Python version control
├── solution_notebook.ipynb   # Main analysis notebook
├── solution_notebook.html    # Main analysis notebook html export
└── .venv/                    # Virtual environment (automatically created by uv sync)
```

## Dependencies

- **PyBaMM** (>=25.10.1): Python Battery Mathematical Modeling framework

All dependencies are specified in `pyproject.toml` and will be automatically installed when running `uv sync`.

## Notes

- The simulation uses the Chen2020 parameter set (LG M50 cell, 5.0 Ah)
- The DFN model is required for accurate electrode potential predictions needed for plating analysis
- Simulation runtime may take several minutes depending on your system
