# Table 5: Consistency between FOIF and TracIn under Different Data Properties

## Purpose

This experiment reproduces **Table 5** in the paper, which compares the consistency between **First-Order Influence Functions (FOIF)** and **TracIn** under different data properties.

The consistency is evaluated using:

- Weighted Kendall's Tau (τw)
- Top-10% Overlap

The experiment considers four different data properties:

- Dataset size
- Feature dimensionality
- Density contrast
- Class imbalance

For each setting, the corresponding FOIF and TracIn influence scores are first generated, after which the summary notebook computes the consistency metrics.

---

# Folder Contents

```text
Table5_Consistency/
│
├── NumberOfSamples-InfluenceEstimation.ipynb
├── NumberOfFeaturesExperiment.ipynb
├── SmallLargeDensityExperiment-Newersetting.ipynb
├── ClassImbalance-InfluenceEstimation.ipynb
│
├── ConsistencySummary.ipynb
│
├── IF_*.csv
├── TC_*.csv
│
└── README.md
```

---

# Reproducing the Experiment

The experiment consists of two stages.

## Stage 1 – Generate Influence Scores

Four different influence-estimation notebooks are used, each corresponding to one data property.

### A. Dataset Size

Open

```text
NumberOfSamples-InfluenceEstimation.ipynb
```

Modify

```python
train_df = nested_train_dfs[...]
```

Generate the following three settings:

| Index | Dataset size |
|------:|-------------|
| 1 | 2K samples |
| 5 | 6K samples |
| 9 | 10K samples |

Remember to update the saved FOIF and TracIn filenames for each setting to avoid overwriting previously generated files.

---

### B. Feature Dimensionality

Open

```text
NumberOfFeaturesExperiment.ipynb
```

Modify

```python
k = ...
```

using

| Setting | Configuration |
|---------|---------------|
| 10 features | `k = 0` |
| 32 features | `k = KS[3]` |
| 52 features | `k = KS[8]` |

Remember to update the saved filenames for each feature setting.

---

### C. Density Contrast

Open

```text
SmallLargeDensityExperiment-Newersetting.ipynb
```

Modify

```python
std1_dense
std1_sparse
```

using

| Setting | Dense | Sparse |
|---------|------:|-------:|
| (1, 0.1) | 0.1 | 1 |
| (3, 0.01) | 0.01 | 3 |
| (10, 0.0001) | 0.0001 | 10 |

Again, remember to update the saved filenames.

---

### D. Class Imbalance

Open

```text
ClassImbalance-InfluenceEstimation.ipynb
```

Modify

```python
cur_ratio = ratios[...]
```

using

| Index | Ratio |
|------:|-------|
| 0 | 1:9 |
| 2 | 3:7 |
| 4 | 5:5 |

Remember to update the saved filenames for each class ratio.

---

After completing Stage 1, the repository should contain one FOIF file and one TracIn file for every setting reported in Table 5.

---

## Stage 2 – Generate Table 5

Open

```text
ConsistencySummary.ipynb
```

This notebook computes the consistency metrics using all influence-score files generated in Stage 1.

Locate the experiment configuration:

```python
experiments = [
    ...
]
```

Update the `"IF File"` and `"TC File"` entries so that they correspond to the filenames generated during Stage 1.

For example,

```python
{
    "Data Property": "Dataset size",
    "Setting": "2K samples",
    "IF File": "IF_Train_Set_2k.csv",
    "TC File": "TC_Train_Set_2k.csv",
}
```

Repeat this for all settings included in Table 5.

After the filenames have been updated, execute all notebook cells sequentially.

The notebook automatically computes:

- Weighted Kendall's Tau
- Top-10% Overlap

for every data property and setting.

---

# Expected Output

Running the complete pipeline reproduces **Table 5** in the paper.

The notebook reports the consistency statistics for:

| Data Property | Settings |
|--------------|----------|
| Dataset size | 2K, 6K, 10K |
| Feature dimensionality | 10, 32, 52 features |
| Density contrast | (1, 0.1), (3, 0.01), (10, 0.0001) |
| Class imbalance | 1:9, 3:7, 5:5 |

For each setting, the following metrics are reported:

- Weighted Kendall's Tau (τw)
- Top-10% Overlap

---

# Notes

- This experiment reuses the influence-estimation notebooks from previous experiments.
- The provided influence-score files allow users to skip Stage 1 and directly execute `ConsistencySummary.ipynb`.
- When generating influence scores, remember to update the output filenames for every experimental setting to avoid overwriting previous results.
- Before running `ConsistencySummary.ipynb`, ensure that all `"IF File"` and `"TC File"` entries correctly reference the generated filenames.
- All notebooks assume that the required CSV files are located in the same directory as the notebooks.
