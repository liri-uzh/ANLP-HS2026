# ANLP HS2026

These marerials are for the ZI course **Introduction to Natural Language Processing** (HS2026) at the University of Zurich.

The notebooks are designed to be run in **Google Colab** or locally on your own computer. The notebooks are self-contained and install all required packages automatically on Colab. On your own computer, you need to set up a Python 3.12 environment and install the packages listed in `requirements.txt` (see below).

## Google Colab

To open a notebook in Google Colab, navigate to the notebook and then change the domain in the URL from `github.com` to `githubtocolab.com`.

## Local Environment Setup

You need about 10 GB of free disk space and an internet connection. The first run of some notebooks downloads models and datasets.

First, download the course materials (step 1). Then set up the Python environment with **conda** (steps 2–4 below) or with **uv** (see [Alternative setup with uv](#alternative-setup-with-uv)). Choose one. Steps 5–7 are the same for both.

### 1. Download the course materials

**With git (recommended).** This makes it easy to get new notebooks and updates during the course:

```bash
git clone https://github.com/liri-uzh/ANLP-HS2026.git
cd ANLP-HS2026
```

To get the latest version later, run `git pull` in this folder.

**Without git.** On the [GitHub page](https://github.com/liri-uzh/ANLP-HS2026), click **Code → Download ZIP** and unzip the file. To get the latest version later, download the ZIP file again.

All the following commands are run in this project folder (`ANLP-HS2026`).

### 2. Install conda

If you do not have conda yet, install [Miniforge](https://github.com/conda-forge/miniforge) or [Miniconda](https://www.anaconda.com/docs/getting-started/miniconda/install).

### 3. Create the environment

The notebooks need **Python 3.12**.

```bash
conda create -n anlp-hs26 python=3.12 -y
conda activate anlp-hs26
```

### 4. Install the Python packages

Run the commands below from the folder that contains `requirements.txt`.

> **Only if you have a Linux computer without an NVIDIA GPU:** install the CPU version of `torch` first. Otherwise, several GB of GPU packages are installed that you do not need:
>
> ```bash
> uv pip install torch==2.12.1 --index-url https://download.pytorch.org/whl/cpu
> ```

On all computers, run:

```bash
uv pip install -r requirements.txt # uv is optional, it makes the output nicer
python -m spacy download en_core_web_sm-3.8.0 --direct
```

The second line downloads the small English model for spaCy. It is not part of `requirements.txt`.

### Alternative setup with uv

Use this instead of steps 2–4 if you prefer [uv](https://docs.astral.sh/uv/) over conda.

1. Install uv (see the [installation guide](https://docs.astral.sh/uv/getting-started/installation/)):
   ```bash
   # macOS / Linux
   curl -LsSf https://astral.sh/uv/install.sh | sh
   # Windows (PowerShell)
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```
2. Create a virtual environment with Python 3.12 in the project folder. uv downloads Python 3.12 for you if it is not installed.
   ```bash
   uv venv --python 3.12
   ```
   This creates a `.venv` folder.
3. Activate the environment:
   ```bash
   source .venv/bin/activate      # macOS / Linux
   .venv\Scripts\activate         # Windows
   ```
4. Install the Python packages and the spaCy English model.

   > **Only if you have a Linux computer without an NVIDIA GPU:** install the CPU version of `torch` first (see step 4):
   >
   > ```bash
   > uv pip install torch==2.12.1 --index-url https://download.pytorch.org/whl/cpu
   > ```

   On all types of computers, run:
   ```bash
   uv pip install -r requirements.txt
   python -m spacy download en_core_web_sm-3.8.0 --direct
   ```
   (The environment has no `pip`, but that is fine: `spacy download` then uses `uv pip install` automatically.)

Then continue with step 5. In VS Code, choose the `.venv` environment as kernel instead of `anlp-hs26`. Activate the environment (or prefix commands with `uv run`) before you run `jupyter lab` or the check in step 7.

### 5. Install Ollama

Ollama is not a Python package. You install it on your computer. It runs language models locally and is used in both `S4` notebooks.

1. Download and install it from <https://ollama.com/download>.
2. Start the server in a separate terminal and leave it open:
   ```bash
   ollama serve
   ```
   (If the Ollama desktop app is already running, skip this step.)
3. Download the models:
   ```bash
   ollama pull qwen2.5:1.5b             # S4 part 1
   ollama pull maternion/LightOnOCR-2   # S4 part 2
   ```

The S4 notebooks start `ollama serve` for you only on Google Colab. On your own computer, you do it yourself.

### 6. Open the notebooks

- **VS Code:** open a notebook in `notebooks/`, click **Select Kernel**, and choose `anlp-hs26` (conda) or `.venv` (uv).
- **JupyterLab:** run `jupyter lab` in the project folder, then open a notebook in `notebooks/`.

### 7. Check that it works

```bash
python -c "import spacy, torch, pymupdf, docling; spacy.load('en_core_web_sm'); print('OK')"
```

If you see `OK`, the setup is ready.

### Notes

- **Slow first run.** Some cells download models and datasets (Hugging Face, GloVe vectors, Docling). This can take several minutes. The next runs are faster.
- **Mac with Apple Silicon:** the pinned `torch` version needs macOS 14 or newer.
- **Google Colab** also works. The first code cell of each notebook installs the packages it needs (with pinned versions) when it detects Colab. On your own computer, this cell does nothing, so you can run it safely.
- **Ollama version.** The notebooks use Ollama 0.34.0 on Colab. On your computer, install this version or a newer one.

---

*Parts of this README were written with the help of Claude (Anthropic).*
