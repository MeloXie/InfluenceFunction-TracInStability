# Zero-Padding Feature Heatmap

This supplementary experiment evaluates the feature-dimensionality experiment using **zero-padding** instead of adding random noise features. The overall workflow is identical to the feature heatmap experiment in the main paper, except that additional feature dimensions are created by appending zero-valued columns.

Unlike the main paper experiment, this experiment only requires **one run** for each feature setting.

## Folder Contents

```text
ZeroPadding_Featuremap/
│
├── NumberOfFeatures0Padding/
│
├── NumberOfFeaturesExperiment-Pad0.ipynb
├── FeatureHeatmap-0padding.ipynb
│
└── README.md
```

---

## Reproducing the Experiment

### Step 1. Generate influence scores for different feature dimensions

Open

```text
NumberOfFeaturesExperiment-Pad0.ipynb
```

Run the notebook once for each feature dimensionality.

Locate the following code:

```python
KS = [10, 14, 18, 22, 26, 30, 34, 38, 42]

k = KS[8]

X_padding = np.zeros(
    (X.shape[0], k),
    dtype=X.dtype
)

X = np.hstack((X, X_padding))
# k = 0
```

To generate the desired feature dimension:

- **10 features:** set `k = 0`, comment above code
- **20 features:** set `k = KS[0]`
- **24 features:** set `k = KS[1]`
- **28 features:** set `k = KS[2]`
- **32 features:** set `k = KS[3]`
- **36 features:** set `k = KS[4]`
- **40 features:** set `k = KS[5]`
- **44 features:** set `k = KS[6]`
- **48 features:** set `k = KS[7]`
- **52 features:** set `k = KS[8]`

For each setting, also update the output filenames accordingly, for example:

```python
TracIn_sorted.to_csv("NumberOfFeatures0Padding/TC_Feature_Column_10_00_0padding.csv", index=False)
df_sorted.to_csv("NumberOfFeatures0Padding/IF_Feature_Column_10_00_0padding.csv", index=False)
```

After completing all feature settings, the folder should contain the IF and TracIn influence files for every feature dimension.

---

### Step 2. Generate the feature heatmaps

Open

```text
FeatureHeatmap-0padding.ipynb
```

Ensure that all generated influence files are correctly referenced, for example:

```python
IF_1 = pd.read_csv("NumberOfFeatures0Padding/IF_Feature_Column_10_00_0padding.csv")
...
IF_10 = pd.read_csv("NumberOfFeatures0Padding/IF_Feature_Column_10_42_0padding.csv")

TC_1 = pd.read_csv("NumberOfFeatures0Padding/TC_Feature_Column_10_00_0padding.csv")
...
TC_10 = pd.read_csv("NumberOfFeatures0Padding/TC_Feature_Column_10_42_0padding.csv")
```

Once the filenames are correct, simply execute all notebook cells.

---

## Expected Output

The notebook automatically generates and saves:

- FOIF zero-padding feature heatmap
- TracIn zero-padding feature heatmap

---

## Notes

- This experiment follows the same workflow as the feature heatmap experiment in the main paper, but uses **zero-padding** instead of random noisy features.
- Only **one run** is required for each feature setting.
- Remember to update the output filenames in the influence-estimation notebook for each feature dimensionality.
- Before running the heatmap notebook, ensure that all generated influence files are correctly referenced.
