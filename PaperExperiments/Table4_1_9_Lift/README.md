
# Table 4: Sign-Aware Minority Lift under Different Class Imbalance Ratios

## Purpose

This experiment reproduces **Table 4** in the paper, which evaluates the **sign-aware minority lift** of **First-Order Influence Functions (FOIF)** and **TracIn** under different class imbalance settings.

The experiment is performed on both the **SYN_A** and **Diamonds** datasets. For each class ratio, the notebook computes:

- Lift@Top
- Lift@Bottom
- Lift@AbsTop

Although the paper reports only the **1:9** class imbalance setting, the notebooks compute these statistics for **all five class ratios (1:9 to 5:5)**.

---

# Folder Contents

```text
Table4_1_9_Lift/
│
├── ClassImbalance/
├── ClassImbalance_Diamonds/
│
├── ClassImbalance-InfluenceEstimation.ipynb
├── ClassImbalance-InfluenceEstimation-Diamonds.ipynb
│
├── ClassImbalance-Lift-SignAware.ipynb
├── ClassImbalance-Lift-Diamonds-SignAware.ipynb
│
└── README.md
```

---

# Reproducing the Experiment

The experiment consists of two stages.

## Stage 1 – Generate Influence Scores

For the synthetic dataset, open

```text
ClassImbalance-InfluenceEstimation.ipynb
```

For the Diamonds dataset, open

```text
ClassImbalance-InfluenceEstimation-Diamonds.ipynb
```

These notebooks compute the FOIF and TracIn influence scores under different class imbalance settings.

### Step 1 – Select the Class Ratio

Modify

```python
cur_ratio = ratios[...]
```

The available settings are:

| Index | Class Ratio |
|------:|-------------|
| 0 | 1:9 |
| 1 | 2:8 |
| 2 | 3:7 |
| 3 | 4:6 |
| 4 | 5:5 |

### Step 2 – Execute the Notebook

Run all notebook cells sequentially.

For each class ratio, the notebook generates:

- FOIF influence-score files;
- TracIn influence-score files;
- training-label files.

### Step 3 – Repeat for All Class Ratios

Repeat the notebook for all five class ratios.

> **Important:** Update the output filenames when changing the class ratio to avoid overwriting previously generated files.

After completing this stage, each dataset (SYN_A and Diamonds) should contain:

- 5 FOIF influence-score files;
- 5 TracIn influence-score files;
- 5 training-label files.

---

## Stage 2 – Generate the Sign-Aware Lift Statistics

For the synthetic dataset, open

```text
ClassImbalance-Lift-SignAware.ipynb
```

For the Diamonds dataset, open

```text
ClassImbalance-Lift-Diamonds-SignAware.ipynb
```

Execute all notebook cells sequentially.

The notebooks automatically read the intermediate files generated in Stage 1 and compute the sign-aware minority lift statistics for all five class imbalance settings.

No code modifications are required.

---

# Expected Output

Running the complete pipeline reproduces the sign-aware minority lift statistics reported in the paper.

The notebooks generate a summary table containing the following statistics for each class ratio:

- Lift@Top
- Lift@Bottom
- Lift@AbsTop

for:

- SYN_A – FOIF
- SYN_A – TracIn
- Diamonds – FOIF
- Diamonds – TracIn

Although the output includes results for all five class imbalance ratios (**1:9 to 5:5**), **Table 4** in the paper reports only the **1:9** results.

---

# Notes

- Stage 1 is identical to the influence-estimation stage used for **Figure 7**.
- If the intermediate influence-score and label files have already been generated while reproducing **Figure 7**, Stage 1 can be skipped.
- No parameter changes or filename modifications are required in the sign-aware summary notebooks.
- All notebooks assume that the provided directory structure is preserved.
