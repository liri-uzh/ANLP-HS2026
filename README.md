# ANLP HS2026

## Environment setup

You need about 10 GB of free disk space and an internet connection. The first run of some notebooks downloads models and datasets.

### 1. Install conda

If you do not have conda yet, install [Miniforge](https://github.com/conda-forge/miniforge) or [Miniconda](https://www.anaconda.com/docs/getting-started/miniconda/install).

### 2. Create the environment

The notebooks need **Python 3.12**.

```bash
conda create -n anlp-hs26 python=3.12 -y
conda activate anlp-hs26
```

### 3. Install the Python packages

Run this from the folder that contains `requirements.txt`:

```bash
uv pip install -r requirements.txt # uv is optional, it makes the output nicer
python -m spacy download en_core_web_sm-3.8.0
```

The second line downloads the small English model for spaCy. It is not part of `requirements.txt`.

### 4. Install Ollama

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

### 5. Open the notebooks

- **VS Code:** open a notebook in `notebooks/`, click **Select Kernel**, and choose `anlp-hs26`.
- **JupyterLab:** run `jupyter lab` in the project folder, then open a notebook in `notebooks/`.

### 6. Check that it works

```bash
python -c "import spacy, torch, pymupdf, docling; spacy.load('en_core_web_sm'); print('OK')"
```

If you see `OK`, the setup is ready.

### Notes

- **Slow first run.** Some cells download models and datasets (Hugging Face, GloVe vectors, Docling). This can take several minutes. The next runs are faster.
- **Mac with Apple Silicon:** the pinned `torch` version needs macOS 14 or newer.
- **Google Colab** also works. The first code cell of each notebook installs the packages it needs (with pinned versions) when it detects Colab. On your own computer, this cell does nothing, so you can run it safely.
- **Ollama version.** The notebooks use Ollama 0.34.0 on Colab. On your computer, install this version or a newer one.
