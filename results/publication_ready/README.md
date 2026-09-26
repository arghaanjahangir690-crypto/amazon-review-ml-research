# Publication-Ready Results

This directory surfaces a small, reviewer-friendly subset of the final research evidence from the completed artifact archive.

## Authoritative headline result

Feature-Level Fusion:
- OOF MAE = **0.183839**
- OOF RMSE = **0.259551**
- OOF R² = **0.207595**

Structured CatBoost:
- OOF MAE = **0.189087**

Relative OOF MAE improvement:
- **2.78%**

Paired fold evidence:
- lower fusion MAE in **4/5** folds
- paired t-test p = **0.0991**
- Wilcoxon p = **0.1250**
- Cohen's dz = **0.9571**

**Publication-safe wording:** Feature-level fusion achieved the lowest observed OOF MAE among evaluated models, but paired fold-level tests did not reach the conventional 0.05 significance threshold.

## Files

- `Manuscript_Result_Fact_Sheet.txt`
- `tables/Table_01_Model_Performance.csv`
- `tables/Table_02_Statistical_Comparison.csv`
- `tables/Table_03_Ablation_Analysis.csv`
- `tables/Table_04_Feature_Group_Importance.csv`
- `tables/Table_05_Key_Research_Findings.csv`

These are copied from the completed publication-ready research artifacts; they are not newly generated results.
