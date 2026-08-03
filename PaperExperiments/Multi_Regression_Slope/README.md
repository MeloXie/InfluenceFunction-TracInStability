# Additional Analysis: Multi-Regression Slope Analysis

## Purpose

This experiment reproduces the multiple linear regression analyses used to investigate how **minority status** and **local data density** affect influence scores after controlling for training loss.

Unlike the previous experiments, this analysis is **not presented as a standalone figure or table in the main paper**. Instead, it provides the statistical evidence supporting the discussions on the effects of class imbalance and density contrast.

Two independent analyses are included:

- **Class imbalance**
  - SYN_A
  - Diamonds
- **Density contrast**
  - SYN_A

For each setting, five independent runs are performed. The regression notebook then aggregates all runs and reports the regression coefficients together with their mean and standard deviation.

---

# Folder Structure

```text
Multi_Regression_Slope/
│
├── ClassImbalance/
│   ├── ClassImbalance-InfluenceEstimation.ipynb
│   ├── ClassImbalance-InfluenceEstimation-Diamonds.ipynb
│   ├── ClassImbalanceLossDecileAndRegressionLine_5runs_IF.ipynb
│   ├── ClassImbalanceLossDecileAndRegressionLine_5runs_IF_Diamonds.ipynb
│   ├── IF_*.csv
│   ├── TC_*.csv
│   ├── loss_*.csv
│   └── Class_label_*.csv
│
├── SparseDense/
│   ├── SmallLargeDensityExperiment-Newersetting.ipynb
│   ├── SparseDenseLossDecileAndRegressionLine_5runs_IF.ipynb
│   ├── IF_*.csv
│   ├── TC_*.csv
│   ├── loss_*.csv
│   └── label_*.csv
│
└── README.md
```

---

# Reproducing the Experiment

The workflow is identical for both the **Class Imbalance** and **Sparse–Dense** analyses.

Each analysis consists of two stages.

---

## Stage 1 – Generate Influence Scores

Run the corresponding influence-estimation notebook.

### Sparse–Dense Analysis

Open

```text
SmallLargeDensityExperiment-Newersetting.ipynb
```

### Class Imbalance (SYN_A)

Open

```text
ClassImbalance-InfluenceEstimation.ipynb
```

### Class Imbalance (Diamonds)

Open

```text
ClassImbalance-InfluenceEstimation-Diamonds.ipynb
```

Each notebook computes:

- FOIF scores
- TracIn scores
- Training losses
- Training labels

for one experimental setting.

Repeat the experiment for **five independent runs**, updating the output filenames each time to preserve the results from every run.

After Stage 1, each setting should contain:

- 5 FOIF files
- 5 TracIn files
- 5 loss files
- 5 label files

(20 intermediate files in total.)

---

## Stage 2 – Compute the Regression Statistics

Run the corresponding regression notebook.

### Sparse–Dense

```text
SparseDenseLossDecileAndRegressionLine_5runs_IF.ipynb
```

### Class Imbalance (SYN_A)

```text
ClassImbalanceLossDecileAndRegressionLine_5runs_IF.ipynb
```

### Class Imbalance (Diamonds)

```text
ClassImbalanceLossDecileAndRegressionLine_5runs_IF_Diamonds.ipynb
```

Before executing the notebook, verify that the filenames match those generated during Stage 1.

For example,

```python
foif_df = pd.read_csv(
    f"IF_9_1_run{run_id}.csv"
)

tracin_df = pd.read_csv(
    f"TC_9_1_run{run_id}.csv"
)

loss_df = pd.read_csv(
    f"loss_9_1_run{run_id}.csv"
)

label_df = pd.read_csv(
    f"Class_label_9_1_run{run_id}.csv"
)
```

If different filenames were used during Stage 1, update the file paths accordingly.

After the filenames have been verified, execute all notebook cells sequentially.

The notebook automatically fits the regression model for each run and reports the mean and standard deviation across the five runs.

---

# Expected Output

The regression notebooks report the estimated coefficients for:

- Intercept
- Log-loss coefficient
- Minority coefficient
- Interaction coefficient

together with the derived **minority slope**, reporting the mean and standard deviation across the five runs.

These statistics provide the quantitative evidence supporting the discussions on how minority status and local density influence the estimated training-data influence scores.

---

# Notes

- Both the **Sparse–Dense** and **Class Imbalance** analyses follow the same two-stage workflow.
- Each experimental setting requires five independent runs before the regression analysis can be performed.
- The regression notebooks only require the influence-score, loss, and label files generated during Stage 1.
- Before running the regression notebook, verify that the filenames in the notebook match those generated during the influence-estimation stage.
- The intermediate files for all five runs are provided in this repository. Users who only wish to reproduce the reported regression statistics may therefore skip Stage 1 and directly execute the corresponding regression notebook.
