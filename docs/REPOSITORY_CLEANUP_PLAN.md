# Conservative Repository Cleanup Plan

This plan is intentionally non-destructive. The current optimization branch improves navigation and transparency without deleting historical research evidence.

## Current repository issues

1. The root README was only a title, so reviewers could not understand the study.
2. The repository has no code license selected.
3. Dataset provenance/license information was not visible at repository level.
4. Two approximately 4.7 MB dataset copies are tracked in `data/`.
5. Most research material is nested under large Stage 0/1 artifact trees.
6. Final Stage 2–6 outputs are present in the supplied local archive but not clearly surfaced in the public repository.
7. The currently archived notebook contains Stage 0/1 code, not the complete final Stage 2–6 execution pipeline.
8. Root-level DOCX files are useful source material but make the repository look more like a file dump than a curated research artifact.

## Phase 1 — implemented in this branch

- replace the minimal README with an academic research README;
- expand `.gitignore` for future local/large artifacts;
- add dataset provenance documentation;
- add reproducibility-status documentation;
- add selected publication-ready CSV/text evidence;
- add a citation file;
- add an unpinned dependency-family list;
- preserve all historical files.

## Phase 2 — recommended after author review

Do **not** perform these changes blindly.

### Move, do not delete
Consider moving root documents to:
```text
paper/
docs/literature/
```

### Dataset cleanup
Because raw copies are already tracked, adding them to `.gitignore` will not remove them.

If the author wants a leaner repository:
- confirm the dataset redistribution/license obligations;
- keep `data/README.md`;
- optionally remove redundant raw copies from Git history only after a deliberate licensing/storage decision;
- point users to Kaggle/Zenodo for download.

### Code extraction
If exact Stage 2–6 source code can be recovered:
```text
src/
scripts/
configs/
tests/
```

Suggested modules:
- `src/preprocessing.py`
- `src/features.py`
- `src/grouping.py`
- `src/structured_models.py`
- `src/text_model.py`
- `src/fusion.py`
- `src/evaluation.py`
- `src/explainability.py`

### Results
Keep a concise paper-facing subset under:
```text
results/publication_ready/
```

Keep the large historical artifact manager only if its audit value outweighs repository complexity.

## Phase 3 — paper release

After author verification:
1. merge the optimized structure;
2. confirm the paper's repository URL;
3. choose a code license;
4. verify data attribution/license;
5. tag `v1.0-paper`;
6. optionally archive the tag on Zenodo for a permanent software/research-artifact DOI.
