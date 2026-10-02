# Data directory

The RDD2022 dataset is intentionally **not committed to GitHub** because it is large.

Run the data-download/extraction cells in the notebook to populate:

- `data/raw/` — downloaded/extracted source data
- `data/yolo/` — frozen YOLO-format dataset

The notebook freezes the selected ~4,000-image experiment split and stores the frozen
archive under `artifacts/rdd2022_project/frozen_split/`.
