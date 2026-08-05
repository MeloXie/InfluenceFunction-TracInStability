# Extended Class-Imbalance Regression-Slope Analysis

This supplementary experiment extends the class-imbalance regression analysis presented in the supplementary material by reporting the regression results for both **FOIF** and **TracIn** under the **1:9** and **3:7** class-imbalance settings.

## Folder Contents

```text
Regression_Slope_Class_Imbalance_Extend/
│
├── ClassImbalance-InfluenceEstimation.ipynb
├── ClassImbalanceLossDecileAndRegressionLine_5runs_IF.ipynb
├── ClassImbalanceLossDecileAndRegressionLine_5runs_TC.ipynb
│
├── IF_*.csv
├── TC_*.csv
├── loss_*.csv
├── Class_label_*.csv
│
└── README.md
```

---

## Reproducing the Experiment

This experiment follows the same workflow as the supplementary **Class Imbalance Loss-Decile Analysis**.

Please first refer to

```text
SupplementaryExperiments/Class_Imbalance_Loss_Decile/README.md
```

for the complete influence-estimation procedure.

The influence-estimation notebook generates all required FOIF, TracIn, training-loss, and class-label files for:

- class imbalance ratios **1:9** and **3:7**;
- five independent runs (**Run1–Run5**).

---

### Step 1. Generate the regression statistics

For the FOIF analysis, open

```
ClassImbalanceLossDecileAndRegressionLine_5runs_IF.ipynb
```

For the TracIn analysis, open

```
ClassImbalanceLossDecileAndRegressionLine_5runs_TC.ipynb
```

Before executing either notebook, make sure that the filenames correspond to the class-imbalance setting being analysed.

For the **3:7** setting, use filenames containing:

```python
foif_df = pd.read_csv(
    f"IF_7_3_run{run_id}.csv"
)

tracin_df = pd.read_csv(
    f"TC_7_3_run{run_id}.csv"
)

loss_df = pd.read_csv(
    f"loss_7_3_run{run_id}.csv"
)

label_df = pd.read_csv(
    f"Class_label_7_3_run{run_id}.csv"
)
```

For the **1:9** setting, simply replace every occurrence of:

```
7_3
```

with

```
9_1
```

throughout the notebook.

After confirming the filenames, execute all notebook cells sequentially.

---

## Expected Output

Running the notebooks reproduces the regression coefficients and slope statistics for:

- FOIF (1:9)
- FOIF (3:7)
- TracIn (1:9)
- TracIn (3:7)

The reported results are averaged over five independent runs.

---

## Notes

- This experiment reuses the influence-estimation procedure described in the supplementary **Class Imbalance Loss-Decile Analysis**.
- Five independent runs are required for each class-imbalance setting.
- Before running either regression notebook, ensure that all input filenames consistently use either `9_1` or `7_3`.
- The repository already provides all intermediate CSV files, allowing the regression statistics to be reproduced directly without rerunning the influence-estimation stage.
