# Data and Dataset Provenance

## Source dataset

This research uses the **Karkavelraja J. Amazon Sales Dataset**.

Official / archival references:
- Kaggle: https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset
- Zenodo archival collection: https://zenodo.org/records/10157504

The archival record states that the Amazon dataset contains product ratings and reviews scraped from Amazon in **January 2023** and identifies the dataset license as **CC BY-NC-SA 4.0**.

## Unit of analysis

The study treats each row as a **product-level record**. Review-related fields may aggregate multiple IDs, users, titles, or text fragments; they are not treated as clean independent one-review-per-row user-item events.

## Files currently tracked

- `dataset.csv` — original project dataset copy
- `dataset_for_stage_1.csv` — Stage 1 project copy
- `ML_Tool.ipynb` — Stage 0/1 dataset-intelligence notebook
- `stage0-launch-pad/` — historical Stage 0 audit artifacts
- `stage1-dataset-intelligence/` — historical Stage 1 artifacts
- `Base_Folder_for_ML_Research_After_Stage_0_and_1/` — handover/intelligence artifacts

## Licensing and redistribution

The dataset is third-party data. Do not assume that a future code license for this repository also licenses the dataset.

If the repository is reorganized later, a cleaner research-software layout would usually:
1. keep this provenance README,
2. provide download instructions,
3. avoid unnecessary duplicate dataset copies,
4. retain only small derived metadata/results when redistribution is appropriate.

Existing tracked files are preserved in the current optimization branch to avoid destructive changes.
