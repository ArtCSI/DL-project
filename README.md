# YOLOv11n-CDL + Adaptive AGE — RDD2022

Local/Jupyter-ready version of the supplied **RDD2022 YOLOv11n-CDL + Adaptive AGE** deep
learning/computer-vision project.

The original notebook was designed around Google Colab and Google Drive. This repository
removes those environment-specific dependencies so the project can be opened as a normal
Jupyter Notebook on a CUDA-capable GPU machine.

## What was changed

- Removed `google.colab` imports and `drive.mount(...)`.
- Replaced `/content/...` paths with repository-relative paths.
- Replaced Colab `!pip` installation with a Jupyter `%pip` setup using `requirements.txt`.
- Moved the shared `ConvSmart`, `DSA`, augmentation, and test-corruption implementation to
  `src/common.py`.
- Moved the CDL, CDL+AGE, and CDL+gated-AGE YAML definitions to `configs/`.
- Moved the decisions log to `docs/decisions_log.md`.
- Kept generated data/checkpoints/results in `artifacts/` and `data/`, both excluded from Git.
- Preserved the existing notebook outputs.
- **No project cells were rerun during this conversion.**

## Experiment ladder

| Run | Configuration |
|---|---|
| R1 | Stock YOLOv11n |
| R2 | YOLOv11n + CDL (ConvSmart + DSA + P2 head) |
| R3 | R2 + low-light training augmentation |
| R4 | R3 + Adaptive Gamma Enhancement (AGE) |
| R5 | R3 + brightness-gated AGE |

The notebook contains the full training/evaluation ladder and the previously generated
outputs.

## Repository structure

```text
.
├── configs/
│   ├── cdl.yaml
│   ├── cdl_age.yaml
│   └── cdl_age_gated.yaml
├── data/
│   └── README.md
├── docs/
│   └── decisions_log.md
├── notebooks/
│   └── RDD2022_YOLOv11n_CDL_Adaptive_AGE_local.ipynb
├── src/
│   └── common.py
├── artifacts/                  # generated locally; gitignored
├── requirements.txt
├── REFERENCES.md
├── REPORT.md
└── README.md
```

## Local setup

### 1. Clone the repository

```bash
git clone <your-github-repo-url>
cd <your-repo-folder>
```

### 2. Create a Python environment

Use a fresh Python environment. The supplied notebook metadata targets Python 3, and the
original run used a CUDA-enabled PyTorch environment.

### 3. Install the GPU-enabled PyTorch build

Install the PyTorch/torchvision build appropriate for the CUDA driver and GPU on the
machine. Do this according to the machine's supported PyTorch/CUDA combination.

The project requirements intentionally do **not** pin a PyTorch wheel, because the correct
GPU build is machine-specific.

### 4. Install the project dependencies

```bash
pip install -r requirements.txt
```

### 5. Start Jupyter

```bash
jupyter lab
```

Open:

```text
notebooks/RDD2022_YOLOv11n_CDL_Adaptive_AGE_local.ipynb
```

Run cells sequentially when you are ready to reproduce the experiment.

## Important before running

- The RDD2022 download is large; the dataset is not stored in this repository.
- Training is GPU-intensive and can take substantial time.
- The notebook freezes the selected experiment split so downstream stages use the same
  data.
- Do not commit `.pt` checkpoints, the raw dataset, or generated artifacts.
- The notebook's displayed outputs are historical outputs from the supplied notebook.
  They are preserved for reference and were **not regenerated as part of this repository
  conversion**.

## Source papers

See `REFERENCES.md` for the two papers used by the supplied implementation.
