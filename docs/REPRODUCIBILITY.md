# Reproducibility Status

## What is preserved

The supplied research archive preserves extensive evidence from the completed pipeline, including:
- cleaned/modeling datasets,
- leakage-safe grouped-fold definitions,
- OOF prediction files,
- model metadata,
- fitted model artifacts,
- final result tables,
- publication-ready figures,
- ablation outputs,
- coefficient-based explainability artifacts,
- local explanation fidelity checks,
- a final scientific-integrity audit.

The final audit reports **20/20 checks passed** with no critical or important failures.

## Important reproducibility gap

The currently archived `data/ML_Tool.ipynb` contains the Stage 0/1 workflow. It does **not** contain the complete executable Stage 2–6 modeling code that produced all final structured, text, fusion, statistical, ablation, and explainability artifacts.

The uploaded research archive contains the outputs of those stages, but no standalone `.py` source files for the final modeling pipeline were found.

Therefore the repository currently supports:

- **strong artifact-level traceability** for final results;
- **partial executable reproducibility** for the early audit/intelligence stages;
- **incomplete end-to-end code reproducibility** for the final Stage 2–6 experiments.

This limitation should be stated explicitly in the paper/repository rather than hidden.

## Environment

Exact historical versions of Python, NumPy, pandas, scikit-learn, SciPy, CatBoost, joblib, matplotlib, the operating system, and hardware were not preserved in the final research metadata.

A convenience file `requirements-unpinned.txt` lists the main package families implied by the completed artifacts, but it is **not** an exact environment lock file.

## Authoritative performance evidence

Feature-Level Fusion:
- pooled OOF MAE: 0.183839
- pooled OOF RMSE: 0.259551
- pooled OOF R²: 0.207595

Structured CatBoost:
- pooled OOF MAE: 0.189087

Relative pooled OOF MAE improvement:
- approximately 2.78%

Paired fold evidence:
- fusion lower MAE in 4/5 folds
- paired t-test p = 0.099080
- Wilcoxon p = 0.125
- Cohen's dz = 0.9571

The result must not be described as conventionally statistically significant at α = 0.05.

## Recommended next reproducibility step

Without changing any existing scientific result:

1. recover/export the exact Stage 2–6 code if it still exists in another notebook/session/file;
2. place reusable code under `src/`;
3. place execution entry points under `scripts/`;
4. create a fixed configuration file for the final paper experiment;
5. generate a fresh environment lock file from the original/reconstructed environment if possible;
6. add a script that reproduces paper tables from the already-saved OOF predictions;
7. tag the paper repository state as `v1.0-paper`.

Until this is completed, describe the repository as a **research artifact and partial reproducibility package**.
