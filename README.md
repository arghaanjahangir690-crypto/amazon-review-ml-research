# Amazon Product Rating Prediction Using Multi-View Fusion of Metadata and Review Text

> Research and reproducibility repository for leakage-aware **product-level Amazon rating prediction** using structured metadata and aggregated review text.

## Research focus

This project asks one central question:

> **Can structured product metadata and aggregated review text be integrated through a leakage-aware feature-level fusion framework to reduce product-level Amazon rating prediction error relative to single-view and simple late-fusion alternatives?**

The study uses the Karkavelraja Amazon Sales Dataset and treats each row as a **product-level record**, not as a clean one-review-per-row user-item interaction. The final task is numerical rating regression.

## Evidence structure

The study is organized around three connected evidence layers:

1. **Descriptive** — dataset structure, target distribution, duplicate review text, feature groups, and leakage risks.
2. **Exploratory** — mean baseline, structured Ridge, structured CatBoost, text TF-IDF + Ridge, late fusion, and feature-level fusion under the same grouped OOF protocol.
3. **Explanatory / interpretive** — paired fold analysis, ablation, prediction/residual correlation, coefficient inspection, and local reconstruction fidelity.

These layers address the same research problem; the explanatory layer describes **model behavior and predictive complementarity**, not causality.

## Main result

| Model | OOF MAE | OOF RMSE | OOF R² |
|---|---:|---:|---:|
| **Feature-Level Fusion** | **0.183839** | **0.259551** | **0.207595** |
| Structured CatBoost | 0.189087 | 0.268810 | 0.150055 |
| Late Fusion (50/50) | 0.189640 | 0.264081 | 0.179695 |
| Text TF-IDF + Ridge | 0.199171 | 0.272373 | 0.127375 |

Feature-level fusion reduced pooled OOF MAE by approximately **2.78%** relative to structured CatBoost and achieved lower MAE in **4 of 5** grouped folds.

**Statistical qualification:** paired t-test p = 0.099080 and Wilcoxon p = 0.125. The paper therefore reports the fusion result as the **lowest observed OOF error**, not as statistically established superiority at α = 0.05.

## Dataset

- Original rows: **1,465**
- Valid modeling rows: **1,464**
- Target: numerical product rating
- Review groups used for leakage-aware validation: **1,193**
- Duplicate review groups: **144**
- Rows in duplicate groups: **415 (28.35%)**
- Group crossings between train and validation folds: **0**

Source:
- Kaggle: https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset
- Archived dataset record: https://zenodo.org/records/10157504

The archived record identifies the Amazon dataset as **CC BY-NC-SA 4.0**. Dataset files in this repository are third-party research data and remain governed by the original dataset license; repository code licensing must be handled separately.

## Final predictor views

### Structured view
- actual_price
- discounted_price
- discount_percentage
- rating_count
- price_difference
- log_rating_count
- rating_count_missing
- category_level_1
- category_level_2
- category_level_3

Identity/leakage-prone fields such as product ID/name, user ID/name, review ID, image link, and product link were excluded from predictive modeling.

### Text view
Primary text representation:

`review_text = review_title + review_content`

TF-IDF configuration used in the completed text model:
- lowercase: true
- n-grams: 1–2
- min_df: 2
- max_df: 0.98
- max_features: 15,000
- sublinear TF: true
- Ridge alpha: 10.0

## Validation design

The modeling protocol uses **5-fold GroupKFold** with a hash-based review-group identifier so that identical cleaned review text does not cross folds.

Fold-local learning is required for:
- numeric imputation,
- categorical encoding,
- TF-IDF vocabulary,
- inverse-document-frequency weights.

Validation fold sizes: 293, 293, 293, 293, and 292.

## Fusion strategies

**Late fusion**
- Structured CatBoost OOF prediction
- Text TF-IDF Ridge OOF prediction
- fixed 0.5 / 0.5 average
- weights were not optimized on OOF targets

**Feature-level fusion**
- fold-transformed structured representation
- fold-specific TF-IDF representation
- concatenation
- Ridge regression

The feature-level representation contained approximately 15,106–15,114 features across folds.

## Ablation evidence

| Removed information group | MAE change vs. full fusion |
|---|---:|
| Review text | **+5.90%** |
| Category | +4.16% |
| Price | +3.21% |
| Engagement | +0.73% |

This is interpreted as **incremental predictive contribution**, not causal importance.

## Repository map

```text
.
├── README.md
├── CITATION.cff
├── requirements-unpinned.txt
├── data/
│   ├── README.md
│   ├── dataset.csv
│   ├── dataset_for_stage_1.csv
│   ├── ML_Tool.ipynb
│   ├── stage0-launch-pad/
│   ├── stage1-dataset-intelligence/
│   └── Base_Folder_for_ML_Research_After_Stage_0_and_1/
├── docs/
│   ├── REPRODUCIBILITY.md
│   └── REPOSITORY_CLEANUP_PLAN.md
└── results/
    └── publication_ready/
        ├── README.md
        ├── Manuscript_Result_Fact_Sheet.txt
        └── tables/
```

## Reproducibility status

The repository currently preserves the Stage 0/1 notebook and extensive dataset-audit artifacts. The uploaded research archive also contains final Stage 2–6 **outputs** such as OOF predictions, tables, figures, fitted artifacts, and an internal 20/20 scientific-integrity audit.

However, the currently archived `data/ML_Tool.ipynb` contains the Stage 0/1 workflow and does **not** contain the complete executable Stage 2–6 modeling code that produced all final artifacts. Exact historical Python/library/OS/hardware versions were also not preserved.

Therefore this repository should currently be described as a **research-artifact repository with partial executable reproducibility**, not as a one-command full reproduction package.

See [docs/REPRODUCIBILITY.md](docs/REPRODUCIBILITY.md).

## Primary notebook

`data/ML_Tool.ipynb`

The notebook contains the dataset launch-pad and Stage 1 dataset-intelligence workflow. It should be retained as historical research code, while future cleanup can extract stable reusable code into `src/` and `scripts/` without changing the completed scientific results.

## Publication-ready evidence

Selected authoritative text/CSV outputs are available under:

`results/publication_ready/`

These files are copied from the completed research-artifact archive and are intended to make the main reported results easy to inspect without navigating hundreds of intermediate files.

## Scientific-integrity boundary

The completed audit reports:
- 20/20 checks passed
- 0 critical failures
- 0 important failures
- authoritative OOF metrics recomputed successfully
- no model retraining during the audit
- no prediction modification
- no performance-result modification

This is an **internal computational consistency audit**, not independent external validation.

## Important limitations

- 1,464 valid modeling rows limit statistical power.
- Review fields are aggregated at product level rather than clean one-review-per-row interactions.
- Ratings are concentrated near the upper end of the scale.
- Paired inference is based on only five grouped folds.
- The observed fusion improvement is not conventionally significant at 0.05.
- The study is predictive, not causal.
- The final text representation uses TF-IDF + Ridge rather than transformer models.
- No second independent dataset was used for external validation.
- Exact original environment versions are not preserved.
- Some review text contains explicit rating expressions; robustness to masking these expressions remains future work.

## Citation

A `CITATION.cff` file is provided for repository citation. Update journal/DOI fields when the paper receives final bibliographic metadata.

## Repository maintenance note

The repository contains historical raw/intermediate research artifacts that are useful for auditability but make the root harder to navigate. The optimization branch deliberately **does not delete or rewrite those artifacts**. See [docs/REPOSITORY_CLEANUP_PLAN.md](docs/REPOSITORY_CLEANUP_PLAN.md) for a conservative Phase-2 cleanup plan.

## Author verification still required

Before citing this repository in a submitted manuscript:
- verify that the branch/release corresponding to the paper is public;
- tag the paper version (for example `v1.0-paper`);
- confirm dataset-license attribution;
- choose a code license separately from the dataset license;
- archive the tagged release (e.g., Zenodo) if a permanent software DOI is desired.
