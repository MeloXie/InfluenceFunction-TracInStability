# Figure 7: Minority Lift under Different Class Imbalance Ratios

## Purpose

This experiment reproduces **Figure 7** in the paper, which evaluates how effectively **First-Order Influence Functions (FOIF)** and **TracIn** identify minority-class training samples under different class imbalance settings.

The experiment is performed on both the **SYN_A** and **Diamonds** datasets. For each dataset, influence scores are computed under five different class ratios, after which the minority lift at different Top-\(k\) values is calculated and visualised.

---

# Folder Contents

```text
Figure7_Lift_Plot/
│
├── ClassImbalance/
├── ClassImbalance_Diamonds/
│
├── ClassImbalance-InfluenceEstimation.ipynb
├── ClassImbalance-InfluenceEstimation-Diamonds.ipynb
│
├── ClassImbalance-Lift.ipynb
├── ClassImbalance-Lift-Diamonds.ipynb
│
└── README.md
```

---

# Reproducing the Experiment

The experiment consists of two stages.

## Stage 1 – Generate Influence Scores

For the synthetic dataset, open

```
ClassImbalance-InfluenceEstimation.ipynb
```

For the Diamonds dataset, open

```
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

- FOIF influence scores;
- TracIn influence scores;
- training labels corresponding to each training sample.

### Step 3 – Repeat for All Class Ratios

Repeat Stage 1 for all five class ratios.

> **Important:** Update the output filenames when changing the class ratio to avoid overwriting previously generated results.

After completing this stage, each dataset (SYN_A and Diamonds) should contain fifteen intermediate files:

- 5 FOIF influence files;
- 5 TracIn influence files;
- 5 label files.

---

## Stage 2 – Generate Figure 7

For the synthetic dataset, open

```
ClassImbalance-Lift.ipynb
```

For the Diamonds dataset, open

```
ClassImbalance-Lift-Diamonds.ipynb
```

These notebooks compute the minority lift for different Top-\(k\) values and generate the final plots.

### Step 1 – Select the Influence Method

The notebook processes **one influence method at a time**.

Locate the following code block in the notebook:

```python
for i in range(num_lists):
    ranked = (
        sorted_TC_lists[i]
        .merge(sorted_label_lists[i], left_on="Train_ID", right_on="id", how="left")
    )
    ranked = ranked.drop(columns=["id"])
```

To generate the **TracIn** lift plots, keep the code unchanged.

To generate the **FOIF** lift plots, replace

```python
sorted_TC_lists
```

with

```python
sorted_IF_lists
```

so that the code becomes

```python
for i in range(num_lists):
    ranked = (
        sorted_IF_lists[i]
        .merge(sorted_label_lists[i], left_on="Train_ID", right_on="id", how="left")
    )
    ranked = ranked.drop(columns=["id"])
```

> **Important:** This code block appears **twice** in both `ClassImbalance-Lift.ipynb` and `ClassImbalance-Lift-Diamonds.ipynb`. Ensure that **both occurrences** are updated before running the notebook to generate the FOIF lift plots.

### Step 2 – Save the Figure

When generating the FOIF plots, remember to update the output filename accordingly.

For example,

```
Class_Imbalance_Synthetic_TC.png
```

should be changed to

```
Class_Imbalance_Synthetic_IF.png
```

Similarly, update the corresponding filenames for the Diamonds plots.

Execute the notebook twice, once for FOIF and once for TracIn.

---

# Expected Output

Running the complete pipeline reproduces **Figure 7** in the paper.

The following figures are generated in the experiment's root directory:

- `Class_Imbalance_Synthetic_IF.png`
- `Class_Imbalance_Synthetic_TC.png`
- `Class_Imbalance_Diamonds_IF.png`
- `Class_Imbalance_Diamonds_TC.png`

These correspond to the minority-lift curves for:

- SYN_A – FOIF
- SYN_A – TracIn
- Diamonds – FOIF
- Diamonds – TracIn

---

# Notes

- Execute Stage 1 for all five class imbalance ratios before generating the final plots.
- `ClassImbalance-Lift.ipynb` and `ClassImbalance-Lift-Diamonds.ipynb` should each be executed **twice**, once for FOIF and once for TracIn.
- When switching between FOIF and TracIn, remember to update both the loaded influence lists (`sorted_IF_lists` / `sorted_TC_lists`) and the output figure filename.
- All notebooks assume that the required files are located in the directory structure provided in this repository.
