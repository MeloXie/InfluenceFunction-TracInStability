# MMD Sanity Check

This supplementary experiment measures the distributional similarity between datasets with different feature dimensionalities using the Maximum Mean Discrepancy (MMD).

## Folder Contents

```text
MMD_Sanity_Check/
│
├── NumberOfFeaturesExperiment-GetDataset.ipynb
├── DatasetClosenessMeasurement.ipynb
│
├── train_df_feature10.csv
├── train_df_feature20.csv
├── train_df_feature24.csv
├── train_df_feature28.csv
├── train_df_feature32.csv
├── train_df_feature36.csv
├── train_df_feature40.csv
├── train_df_feature44.csv
├── train_df_feature48.csv
├── train_df_feature52.csv
│
└── README.md
```

---

## Reproducing the Experiment

This experiment consists of two stages.

### Step 1. Generate datasets with different feature dimensionalities

Open

```
NumberOfFeaturesExperiment-GetDataset.ipynb
```

This notebook generates the training datasets used in the MMD analysis.

As in the **Feature Heatmap** experiment from the main paper, change the feature setting by modifying

- For the **10-feature** dataset, simply set

```python
k = 0
```

- For the remaining feature settings (14–52 features), use

```python
KS = [10,14,18,22,26,30,34,38,42]

...

k = KS[i]
```

where `i = 0, ..., 8` corresponds to feature dimensions 14, 18, 22, ..., 52.


Also remember to update the output filename accordingly. For example,

```python
train_df.to_csv("train_df_feature52.csv", index=False)
```

Repeat this procedure for all feature settings.

After completion, the folder should contain the ten provided training datasets corresponding to different feature dimensionalities.

---

### Step 2. Compute the MMD measurements

Open

```
DatasetClosenessMeasurement.ipynb
```

and execute all cells.

As long as the generated dataset filenames match those provided in this repository, no code modification is required.

The notebook automatically loads all generated datasets, computes the pairwise MMD measurements, and generates the supplementary figure.

---

## Expected Output

Running the notebook reproduces the supplementary MMD sanity-check figure and automatically saves the generated plot.

---

## Notes

- The dataset-generation procedure is identical to that used in the main-paper **Feature Heatmap** experiment.
- Once all ten dataset CSV files have been generated, no further code modification is required.
- The repository already provides the generated dataset CSV files, allowing users to reproduce the supplementary figure directly by running `DatasetClosenessMeasurement.ipynb`.
