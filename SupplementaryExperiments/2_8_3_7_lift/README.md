# Sign-aware Lift under Moderate Class Imbalance (2:8 and 3:7)

This supplementary experiment reports the sign-aware minority lift results for the **2:8** and **3:7** class-imbalance settings, corresponding to Table 8 in the supplementary material.

## Folder Contents

```text
2_8_3_7_Lift/
│
├── ClassImbalance/
├── ClassImbalance_Diamonds/
│
├── ClassImbalance-InfluenceEstimation.ipynb
├── ClassImbalance-InfluenceEstimation-Diamonds.ipynb
├── ClassImbalance-Lift-SignAware.ipynb
├── ClassImbalance-Lift-Diamonds-SignAware.ipynb
│
├── diamonds.csv
│
└── README.md
```

---

## Reproducing the Experiment

This experiment uses **exactly the same implementation and workflow** as **Table 4 (Sign-aware Minority Lift)** in the main paper.

Please refer to:

```
PaperExperiments/Table4_1_9_Lift/README.md
```

for the complete reproduction instructions.

The provided implementation computes the sign-aware lift statistics for **all class-imbalance ratios (1:9 to 5:5)**. The supplementary material simply reports the results corresponding to the **2:8** and **3:7** settings.

---

## Notes

- No additional code or parameter modifications are required beyond those described in the main-paper experiment.
- The provided intermediate files can be used directly without recomputing the influence estimation stage.
