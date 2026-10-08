# Trained Models

Serialized final model binaries for MLP, Random Forest, and XGBoost are not included in this repository.

The complete training, Active Learning, and evaluation implementation is provided in:

```text
notebooks/01_hybrid_active_learning_comparison.ipynb

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

## Reproducing the Models
The included final dataset and notebook are sufficient to retrain the models using the same documented experiment configuration.
The final model table is available at:

```text
data/ics_nad_model_table_v3.parquet
```
```text
notebooks/01_hybrid_active_learning_comparison.ipynb
```

## Model Artifact Policy

Pretrained serialized model files are not currently distributed with this repository.
If pretrained model artifacts are published separately in the future, they can be stored in this directory or hosted externally with a public download link.

Recommended structure:

```text
models/
├── MLP/
├── RandomForest/
├── XGBoost/
└── README.md
```

Retraining the models from the supplied notebook and dataset is not equivalent to distributing pretrained model binaries. This repository therefore provides the complete reproducible training procedure rather than claiming that pretrained model files are included.
