# Results

The final notebook writes all reproduced experiment outputs to:

```text
results/combined_hybrid_open_set_mlp_rf_xgb/
```

The directory is generated automatically when the notebook is run.

Expected outputs include:

- per-run summaries
- per-round Active Learning metrics
- query logs
- per-class metrics
- strategy aggregates
- Hybrid cross-model comparison
- Hybrid-vs-Random comparison
- metric leaders
- acquisition-channel effectiveness
- Version-B external evaluation
- paper-ready comparison table
- target checklist
- plots
- experiment configuration
- audit copies
- final results ZIP

## Published Hybrid Result Summary

| Metric | MLP | Random Forest | XGBoost |
|---|---:|---:|---:|
| UADR | 1.000 | 1.000 | 1.000 |
| Labels to Full Discovery | 25.3 | 57.3 | 102.3 |
| Unknown Query Yield | 27.1% | 31.7% | 33.7% |
| Macro-F1 | 0.886 | 0.994 | 0.995 |
| Accuracy | 0.894 | 0.993 | 0.994 |
| Hidden Macro Recall | 0.999 | 0.998 | 1.000 |
| Teardrop Recall | 0.996 | 1.000 | 1.000 |
| ACK Pair Macro-F1 | 0.933 | 0.991 | 0.995 |
| Representation Redundancy | 0.171 | 0.178 | 0.680 |
| Binary F1 | 0.995 | 0.998 | 0.998 |
| External Macro-F1 | 0.842 | 0.889 | 0.884 |


