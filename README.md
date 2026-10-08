# Hybrid Open-Set Active Learning for Unknown Attack Discovery in ICS-NAD

This repository contains the final reproducibility package for the experiment
comparing **MLP**, **Random Forest**, and **XGBoost** under the same
**Hybrid Open-Set Active Learning** pipeline.

## Research Objective

The objective is not only to classify known Industrial Control System (ICS)
network attacks, but also to discover attack classes that are hidden from the
initial labeled training set while minimizing analyst labeling effort.

The final experiment compares three query strategies for each model:

- Random Sampling
- Uncertainty Sampling
- Hybrid Open-Set Active Learning

The Hybrid strategy combines:

- uncertainty
- novelty
- post-discovery expansion
- random exploration
- density awareness
- representation-space diversity
- query-group redundancy control

## Final Experiment Configuration

- Dataset: polished ICS-NAD model table
- Rows: 67,801
- Classes: 17
- Behavior features: 86
- Hidden classes: `land`, `ackpflood`, `teardrop`
- Models: MLP, Random Forest, XGBoost
- Seeds: `42`, `2026`, `31415`
- Initial labeled samples: 50 per known class
- Active Learning budget: 300 labels
- Query batch size: 25
- Hybrid quota:
  - uncertainty: 8
  - novelty: 7
  - expansion: 7
  - random exploration: 3
- Total main Active Learning runs:
  - 3 models × 3 strategies × 3 seeds = 27 runs

## Main Hybrid Results

| Metric | MLP | Random Forest | XGBoost |
|---|---:|---:|---:|
| UADR | 1.000 | 1.000 | 1.000 |
| Labels to discover all hidden | 25.3 | 57.3 | 102.3 |
| Unknown Query Yield | 27.1% | 31.7% | 33.7% |
| Macro-F1 | 0.886 | 0.994 | 0.995 |
| Accuracy | 0.894 | 0.993 | 0.994 |
| Hidden Macro Recall | 0.999 | 0.998 | 1.000 |
| Teardrop Recall | 0.996 | 1.000 | 1.000 |
| ACKPFlood Precision | 0.847 | 1.000 | 1.000 |
| ACKPFlood Recall | 1.000 | 0.993 | 1.000 |
| ACKFlood Recall | 0.921 | 0.985 | 0.987 |
| ACK Pair Macro-F1 | 0.933 | 0.991 | 0.995 |
| Representation Redundancy | 0.171 | 0.178 | 0.680 |
| Group Redundancy | 0.019 | 0.021 | 0.000 |
| Binary F1 | 0.995 | 0.998 | 0.998 |
| External Macro-F1 | 0.842 | 0.889 | 0.884 |
| Full Discovery Success | 3/3 | 3/3 | 3/3 |

### Interpretation

- **MLP**: fastest hidden-attack discovery and lowest model-specific
  representation redundancy.
- **Random Forest**: strongest overall balance between classification,
  discovery efficiency, low redundancy, and external generalization.
- **XGBoost**: strongest final classifier, but its Hybrid representation
  redundancy is higher and full discovery requires more labels.

Representation redundancy should be interpreted as a model-specific diversity
indicator because each model uses a different internal representation space.

## Repository Structure

```text
ics-nad-hybrid-active-learning/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   └── 01_hybrid_active_learning_comparison.ipynb
│
├── data/
│   ├── README.md
│   ├── feature_spec_v3.json
│   ├── data_readiness_summary.json
│   └── ics_nad_model_table_v3.parquet
│
├── reports/
│   ├── class_capture_coverage.csv
│   ├── manual_label_review.csv
│   ├── version_A_comparable_class_counts.csv
│   ├── version_A_temporal_class_counts.csv
│   ├── version_B_class_counts.csv
│   ├── version_B_external_diagnostic.csv
│   ├── version_B_external_per_class_diagnostic.csv
│   ├── ack_pair_core_collision_bound.csv
│   ├── class_uniqueness_and_provenance.csv
│   ├── core_cross_label_conflicts.csv
│   ├── ontology_family_summary.csv
│   ├── representation_validation_diagnostic.csv
│   ├── representation_temporal_validation_diagnostic.csv
│   └── source_file_provenance_audit.csv
│
├── models/
│   └── README.md
│
└── results/
    └── README.md
```

## Environment Setup

Python 3.10+ is recommended.

### 1. Clone the repository

```bash
git clone https://github.com/XnayeemX/ics-nad-hybrid-active-learning.git
cd ics-nad-hybrid-active-learning
```

### 2. Create a virtual environment

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

Linux/macOS:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Start Jupyter

From the repository root:

```bash
jupyter lab
```

Open:

```text
notebooks/01_hybrid_active_learning_comparison.ipynb
```

Run all cells from top to bottom.

The notebook automatically detects the repository root and reads the included
dataset and audit files using repository-relative paths.

## Reproducing the Results

The notebook is already configured in `research` mode.

The final experiment uses:

```python
EXPERIMENT_SEEDS = [42, 2026, 31415]
INITIAL_PER_KNOWN_CLASS = 50
LABEL_BUDGET = 300
QUERY_BATCH_SIZE = 25
```

The notebook performs all 27 Active Learning runs and the Version-B external
evaluation. Generated CSV files, plots, audit copies, and the final ZIP of
results are written to:

```text
results/combined_hybrid_open_set_mlp_rf_xgb/
```

The complete research run is computationally heavier than a normal notebook
test. The MLP automatically uses CUDA when a compatible GPU is available.

For a quick code check only, change:

```python
RUN_MODE = "research"
```

to:

```python
RUN_MODE = "smoke"
```

Do not use smoke-mode outputs as paper results.

## Dataset

The final model table needed by the experiment is included as:

```text
data/ics_nad_model_table_v3.parquet
```

It contains the polished experiment table used by the final notebook. See
`data/README.md` for the original dataset access information and data notes.

### Original Dataset

This study uses the ICS-NAD dataset:

**A network attack detection dataset collected from multiple real-world
industrial control systems**

Dataset access:
https://www.scidb.cn/en/detail?dataSetId=380298d0714740dd91413b5db6305dfd

## Trained Models

Serialized pretrained model binaries are not currently stored in this
repository. The complete training pipeline is provided in the final notebook,
allowing the MLP, Random Forest, and XGBoost models to be regenerated using
the documented experiment configuration.

Model artifacts, if published separately, will be linked in
`models/README.md`.

## Reports

The `reports/` directory contains dataset auditing, class coverage,
representation diagnostics, split diagnostics, provenance checks, and
ACKFlood/ACKPFlood collision analysis used to validate the final experiment.

## Important Data Limitation

The hidden classes `land`, `ackpflood`, and `teardrop` each have only one
independent source capture in the supplied dataset. Therefore the experiment
can evaluate discovery and subsequent learning of those hidden classes, but it
cannot establish source-file-disjoint generalization specifically for those
hidden classes from this dataset alone.

## Reproducibility Notes

- The same initial labeled indices are used across the three models for each
  seed.
- The same random-query sequence is used across models in the Random Sampling
  baseline.
- The preprocessing pipeline is fitted only on the primary training partition.
- Leakage-prone metadata and control columns are not used as model predictors.
- The final sealed test partition is not used for model fitting.
- Version-B provides a source-file-disjoint external diagnostic for classes
  where such a split is supported by the available source captures.


## License and Dataset Terms

No separate license is asserted here for the upstream ICS-NAD dataset.
Users should follow the original dataset provider's access and usage terms.
