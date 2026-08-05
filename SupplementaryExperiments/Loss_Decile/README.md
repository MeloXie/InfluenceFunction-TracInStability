# Loss Decile Analysis

This supplementary experiment extends the **Influence Loss Statistics** experiment from the main paper by additionally computing **loss-decile statistics** for the Synthetic and Adult datasets.

## Folder Contents

```text
Loss_Decile/
│
├── Influence_Loss_Influence_Estimation.ipynb
├── Influence_Loss_Influence_Estimation_Adult.ipynb
├── InfluenceLossSummary.ipynb
│
├── IF_Train_Set_1.csv
├── TC_Train_Set_1.csv
├── Train_Loss_Train_Set_1.csv
├── train_labels.csv
│
├── IF_Train_Set_1_Adult.csv
├── TC_Train_Set_1_Adult.csv
├── Train_Loss_Train_Set_1_Adult.csv
├── train_labels_adult.csv
│
└── README.md
```

---

## Reproducing the Experiment

This experiment follows the same workflow as the **Influence Loss Statistics** experiment in the main paper.

Please first refer to

```
PaperExperiments/Table3_Influence_Loss_Stats/README.md
```

for the complete reproduction procedure.

### Step 1. Generate influence scores (optional)

Run

```
Influence_Loss_Influence_Estimation.ipynb
```

to generate the Synthetic dataset results, and

```
Influence_Loss_Influence_Estimation_Adult.ipynb
```

to generate the Adult dataset results.

Each notebook produces:

- FOIF influence scores;
- TracIn influence scores;
- training-loss values;
- training labels.

The generated filenames are already compatible with the summary notebook and require no manual modification.

> **Note:** The Adult dataset contains over **40,000 training samples**, so the influence-estimation stage may take a considerable amount of time. The provided CSV files can be used directly to reproduce the reported results.

---

### Step 2. Compute the loss-decile statistics

Open

```
InfluenceLossSummary.ipynb
```

and execute all cells.

In addition to the correlation and overlap statistics reported in the main-paper experiment, this notebook also computes **loss-decile summaries**, including the mean and median training loss, mean and median influence score, positive-influence fraction, and Spearman correlation within each loss decile.

---

## Expected Output

Running the notebook reproduces the supplementary loss-decile statistics for the Synthetic and Adult datasets together with the influence-loss summary statistics.

---

## Notes

- This experiment extends the **Influence Loss Statistics** experiment from the main paper.
- No code modifications are required; all notebooks can be executed directly.
- Since the Adult dataset uses the full training set, reproducing the influence-estimation stage may take a considerable amount of time. The provided intermediate CSV files are recommended for reproducing the reported results.
