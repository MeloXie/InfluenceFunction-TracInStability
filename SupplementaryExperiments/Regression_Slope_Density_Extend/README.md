# Extended Density Regression-Slope Analysis

This supplementary experiment extends the density-contrast regression analysis by evaluating two additional density settings:

- **(2, 0.05)**
- **(3, 0.01)**

The workflow is identical to the regression-slope analysis described in the main paper, except that different density parameters are used during influence estimation.

## Folder Contents

```text
Regression_Slope_Density_Extend/
│
├── SmallLargeDensityExperiment-Newersetting.ipynb
├── SparseDenseLossDecileAndRegressionLine_5runs_IF.ipynb
├── SparseDenseLossDecileAndRegressionLine_5runs_TC.ipynb
│
├── IF_*.csv
├── TC_*.csv
├── loss_*.csv
├── label_*.csv
│
└── README.md
```

---

## Reproducing the Experiment

This experiment follows the same workflow as the **Multi Regression Slope** experiment in the main paper.

### Step 1. Generate influence, loss, and label files

Open

```
SmallLargeDensityExperiment-Newersetting.ipynb
```

Modify the density parameters according to the desired setting.

For example,

```python
std1_dense = 0.1
std1_sparse = 1.0
```

should be changed to either

- `(2, 0.05)`, or
- `(3, 0.01)`,

depending on the experiment being reproduced.

Run the notebook **five independent times** for each setting, saving the generated files with filenames matching those provided in the repository.

Since this stage requires five complete influence-estimation runs for each setting, reproducing everything from scratch can be time-consuming. The repository therefore provides all intermediate IF, TracIn, loss, and label files.

---

### Step 2. Compute the regression statistics

For FOIF, open

```
SparseDenseLossDecileAndRegressionLine_5runs_IF.ipynb
```

For TracIn, open

```
SparseDenseLossDecileAndRegressionLine_5runs_TC.ipynb
```

Before executing the notebook, ensure that the filenames match the density setting being analysed.

For example, the `(3, 0.01)` setting uses

```python
foif_df = pd.read_csv(
    f"IF_sp3_de001_run{run_id}.csv"
)

tracin_df = pd.read_csv(
    f"TC_sp3_de001_run{run_id}.csv"
)

loss_df = pd.read_csv(
    f"loss_sp3_de001_run{run_id}.csv"
)

label_df = pd.read_csv(
    f"label_sp3_de001_run{run_id}.csv"
)
```

For the `(2, 0.05)` setting, replace every occurrence of

```
sp3_de001
```

with

```
sp2_de005
```

throughout the notebook.

After confirming the filenames, execute all notebook cells sequentially.

---

## Expected Output

Running the notebooks reproduces the regression coefficients and slope statistics for:

- FOIF (2, 0.05)
- FOIF (3, 0.01)
- TracIn (2, 0.05)
- TracIn (3, 0.01)

The reported results are averaged over five independent runs.

---

## Notes

- This experiment extends the density regression analysis reported in the main paper.
- Five independent runs are required for each density setting.
- Before running either regression notebook, ensure that all input filenames consistently correspond to the selected density setting.
- Since reproducing all influence-estimation runs is computationally expensive, the repository provides all intermediate IF, TracIn, loss, and label files for direct reproduction.
