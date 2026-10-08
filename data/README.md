# Dataset

## Included Final Experiment Dataset

The repository includes the final model table used by the reproducibility
notebook:

```text
ics_nad_model_table_v3.parquet
```

Dataset summary:

- 67,801 rows
- 17 classes
- 86 approved behavior features
- target: `attack_type`
- binary target: `is_attack`
- hidden classes:
  - `land`
  - `ackpflood`
  - `teardrop`

The feature definitions, forbidden predictors, split-control columns, and
Active Learning query-group column are documented in:

```text
feature_spec_v3.json
```

The high-level dataset readiness summary is stored in:

```text
data_readiness_summary.json
```

## Original Dataset Access

This work is based on the ICS-NAD dataset:

**A network attack detection dataset collected from multiple real-world
industrial control systems**

Dataset page:

https://www.scidb.cn/en/detail?dataSetId=380298d0714740dd91413b5db6305dfd

The original data contains traffic from multiple industrial control system
vendors, including ABB, Schneider, and Siemens.

Users should follow the original dataset provider's current access, license,
and usage conditions.

## Why the Repository Includes the Parquet Model Table

The final notebook operates directly on the polished model table rather than
requiring users to repeat every earlier dataset-remediation experiment.

The included Parquet file is substantially smaller than the equivalent CSV
while preserving the final experiment table.

## Feature Policy

The final experiment uses the behavior feature block defined in
`feature_spec_v3.json`.

The notebook verifies that forbidden predictors are excluded and that the
Active Learning query-group field is not used as a model input feature.

## Split Policy

The final notebook uses the split columns already present in the model table:

- primary comparable split for the main train/validation/test experiment
- temporal split for robustness diagnostics
- Version-B external/source-file-disjoint split where supported

## Important Limitation

`land`, `ackpflood`, and `teardrop` each have only one independent source
capture in the supplied data. Source-file-disjoint generalization cannot be
claimed specifically for those hidden classes.
