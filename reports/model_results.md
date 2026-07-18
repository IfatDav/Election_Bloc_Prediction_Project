# Model Results — Concise Summary

Configuration: `random_state=99`, missingness threshold 30%, selective LOCF, coalitional bloc
definitions (Yisrael Beiteinu in Center-Left). Model selected on Knesset 24, tested once on Knesset 25.

## Selection phase (Knesset 24, trained on Knesset 21–23)

| Rank | Model | MAE | R² |
|---:|---|---:|---:|
| 1 | **Segmented CLR** (winner) | **4.635** | 0.899 |
| 2 | Segmented CLR + Druze Indicator | 4.645 | 0.897 |
| 3 | XGBoost + Locality Types — Post-hoc Normalized | 4.900 | 0.904 |
| 4 | CLR-XGBoost — Demographic + Locality Types | 4.975 | 0.882 |
| 5 | XGBoost — Demographic + Locality Types | 5.115 | 0.888 |
| 6 | XGBoost — Demographic | 5.384 | 0.869 |
| 7 | Random Forest — Demographic | 5.468 | 0.867 |
| 8 | MLP (CLR) — Neural Baseline | 6.663 | 0.812 |
| 9 | Linear Regression — Demographic | 11.747 | 0.529 |

## Final test (Knesset 25, retrained on Knesset 21–24)

| Metric | Value |
|---|---:|
| **Overall MAE** | **4.207** |
| **Overall R²** | **0.916** |
| Vote-weighted MAE | 2.723 |
| MAE Right / Center-Left / Haredi / Arab | 5.98 / 5.71 / 2.16 / 2.98 |

## Error concentration (test)

| Locality group | n | Mean MAE |
|---|---:|---:|
| Druze-majority | 15 | 10.70 |
| Moshavim | 13 | 10.63 |
| Arab (non-Druze) | 66 | 4.36 |
| Cities | 120 | 2.80 |
| Other | 5 | 2.45 |
| Kibbutzim | 7 | 2.30 |

## Headline conclusions

1. Segmentation (Arab / all-other localities) plus CLR compositional modeling is the decisive
   combination; either ingredient alone underperforms.
2. The reported 4.21 is a genuine held-out test metric (selection was done on Knesset 24 only).
3. Errors concentrate in small localities with idiosyncratic local politics; in cities, where most
   votes are, the model is accurate (MAE 2.80; vote-weighted overall 2.72).
4. A sensitivity rerun with the ideological bloc tagging (Yisrael Beiteinu in Right) yields a
   comparable test MAE (4.13) with a less stable model ranking; the coalitional definition is
   preferred for interpretability and selection stability.
5. The neural-network baseline (6.66) confirms tree ensembles as the right family for this
   small tabular dataset.
