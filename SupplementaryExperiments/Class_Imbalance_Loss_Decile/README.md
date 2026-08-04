# Class Imbalance Loss-Decile Analysis

This supplementary experiment extends the class-imbalance analysis presented in the main paper by reporting the **loss-decile statistics** for both **FOIF** and **TracIn** under the **1:9** and **3:7** class-imbalance settings on both the **SYN$_A$** and **Diamonds** datasets.

## Folder Contents

```text
Class_Imbalance_Loss_Decile/
│
├── ClassImbalance-InfluenceEstimation.ipynb
├── ClassImbalance-InfluenceEstimation-Diamonds.ipynb
│
├── ClassImbalanceLossDecileAndRegressionLine_5runs_IF.ipynb
├── ClassImbalanceLossDecileAndRegressionLine_5runs_IF_Diamonds.ipynb
│
├── *.csv
│
└── README.md
```

---

## Reproducing the Experiment

This experiment follows **almost exactly the same workflow** as the **Multi Regression Slope** experiment in the main paper.

Please first refer to

```
PaperExperiments/Multi_Regression_Slope/README.md
```

for the complete influence-estimation procedure.

The influence estimation stage is identical:

- perform **five independent runs**;
- generate the FOIF, TracIn, training-loss, and class-label files;
- update the filenames appropriately for each run and experimental setting.

Compared with the main-paper experiment, this supplementary experiment evaluates:

- two datasets (**SYN$_A$** and **Diamonds**);
- two class-imbalance settings (**1:9** and **3:7**).

Consequently, a substantially larger number of intermediate files is produced. Recomputing every setting from scratch is therefore **not recommended** unless necessary.

---

### Generate the loss-decile statistics

After the influence-estimation stage, open

```
ClassImbalanceLossDecileAndRegressionLine_5runs_IF.ipynb
```

or

```
ClassImbalanceLossDecileAndRegressionLine_5runs_IF_Diamonds.ipynb
```

These notebooks first compute the regression-slope statistics reported in the main paper and then automatically generate the **loss-decile analysis** reported in the supplementary material.

Before running the notebook, ensure that the filenames match the desired class-imbalance setting.

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

loads the **1:9** class-imbalance results.

To analyse the **3:7** setting, simply replace every occurrence of

```
9_1
```

with

```
7_3
```

while keeping the remaining filenames unchanged.

The notebooks will automatically load the corresponding FOIF, TracIn, training-loss, and label files and generate the appropriate loss-decile statistics.

---

## Expected Output

Running the notebooks produces:

- the regression-slope statistics reported in the main paper;
- the corresponding **loss-decile analysis tables** for FOIF and TracIn under the selected dataset and class-imbalance setting.

---

## Notes

- This experiment extends the **Multi Regression Slope** experiment in the main paper.
- Five independent runs are required for every experimental setting.
- The provided intermediate files can be used directly to reproduce the supplementary tables without recomputing the influence-estimation stage.
- Because this experiment includes multiple datasets, class-imbalance settings, and five independent runs, reproducing every configuration from scratch is computationally expensive and is generally **not recommended**.
