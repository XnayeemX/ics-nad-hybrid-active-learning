# Trained Models

The files supplied for this GitHub-ready package did **not** include serialized
final MLP, Random Forest, or XGBoost model binaries.

The complete training and Active Learning implementation is contained in:

```text
notebooks/01_hybrid_active_learning_comparison.ipynb
```

Running the notebook in `research` mode reproduces the final model-training
process for:

- MLP
- Random Forest
- XGBoost

across the three experiment seeds:

```text
42
2026
31415
```

## Model Artifact Policy

If serialized models are published later, place them in this directory or host
them externally and add the public download link here.

Recommended structure:

```text
models/
├── MLP/
├── RandomForest/
├── XGBoost/
└── README.md
```

For a paper submission, do not claim that pretrained model binaries are
included unless the actual files or a working public download link are added.

The notebook is sufficient to retrain the models from the included final model
table, but retraining is not the same as distributing pretrained binaries.
