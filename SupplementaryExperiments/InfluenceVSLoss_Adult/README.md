# Influence Score vs. Training Loss (Adult)

This supplementary experiment reproduces the relationship between training loss and influence scores on the **Adult** dataset.

## Folder Contents

```text
InfluenceVSLoss_Adult/
│
├── Influence_Loss_Influence_Estimation_Adult.ipynb
├── InfluenceVSLoss-Adults.ipynb
│
├── IF_Train_Set_1_Adult.csv
├── TC_Train_Set_1_Adult.csv
├── Train_Loss_Train_Set_1_Adult.csv
│
└── README.md
```

---

## Reproducing the Experiment

This experiment follows the same workflow as the **Influence Score vs. Training Loss** experiment in the main paper, but uses the **Adult** dataset.

### Step 1. Compute influence scores and training loss

Open

```
Influence_Loss_Influence_Estimation_Adult.ipynb
```

and execute all cells.

The notebook computes the FOIF and TracIn influence scores together with the training loss for every training sample.

The generated files are:

- `IF_Train_Set_1_Adult.csv`
- `TC_Train_Set_1_Adult.csv`
- `Train_Loss_Train_Set_1_Adult.csv`

No code modifications are required.

---

### Step 2. Generate the influence-versus-loss plots

Open

```
InfluenceVSLoss-Adults.ipynb
```

and execute all cells.

The notebook automatically reads the generated CSV files and produces the FOIF and TracIn influence-versus-training-loss plots.

---

## Expected Output

Running the notebook generates and saves two plots:

- `Outliers_Adult_IF_new.png`
- `Outliers_Adult_TC_new.png`

showing the relationship between training loss and influence scores on the Adult dataset.

---

## Notes

- This experiment follows the same workflow as the main-paper **Influence Score vs. Training Loss** experiment.
- The Adult dataset contains over **40,000 training samples**, so the influence-estimation stage may take a considerable amount of time.
- The repository provides the generated intermediate CSV files, which can be used directly to reproduce the plots without rerunning the influence-estimation notebook.
