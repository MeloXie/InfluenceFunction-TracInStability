
# Table 3: Relationship between Training Loss and Influence Scores

## Purpose

This experiment reproduces **Table 3** in the paper, which summarizes the relationship between training loss and influence scores for **First-Order Influence Functions (FOIF)** and **TracIn** on both the **SYN_A** and **Diamonds** datasets.

Using the influence scores, training losses, and training labels, the notebook computes:

- Spearman correlation between training loss and signed influence score;
- Spearman correlation between training loss and influence magnitude;
- HL@Top10%;
- HL@Bottom10%; and
- HL@AbsTop10%.

> **⚠️ Reproduction Recommendation**
>
> The synthetic dataset can be reproduced from scratch within a reasonable amount of time. However, reproducing the Diamonds experiment requires influence estimation on the full Diamonds dataset (over **50,000 training samples**) and may therefore take considerably longer.
>
> The intermediate influence-score, training-loss, and training-label files for the Diamonds dataset are therefore provided in this repository. We recommend using these files when reproducing the reported results.

---

# Folder Contents

```text
Table3_Influence_Loss_Stats/
│
├── Influence_Loss_Influence_Estimation.ipynb
├── Influence_Loss_Influence_Estimation_Diamonds.ipynb
├── InfluenceLossSummary.ipynb
│
├── IF_Train_Set_1.csv
├── TC_Train_Set_1.csv
├── Train_Loss_Train_Set_1.csv
├── train_labels.csv
│
├── Diamonds_IF_Train_Set_1.csv
├── Diamonds_TC_Train_Set_1.csv
├── Diamonds_Train_Loss_Train_Set_1.csv
├── train_labels_diamonds.csv
│
└── README.md
```

---

# Reproducing the Experiment

The experiment consists of two stages.

## Stage 1 – Generate Influence Scores, Training Losses and Labels

For the synthetic dataset, open

```text
Influence_Loss_Influence_Estimation.ipynb
```

For the Diamonds dataset, open

```text
Influence_Loss_Influence_Estimation_Diamonds.ipynb
```

Execute all notebook cells sequentially.

The notebooks generate the following intermediate files.

### Synthetic Dataset

- `IF_Train_Set_1.csv`
- `TC_Train_Set_1.csv`
- `Train_Loss_Train_Set_1.csv`
- `train_labels.csv`

### Diamonds Dataset

- `Diamonds_IF_Train_Set_1.csv`
- `Diamonds_TC_Train_Set_1.csv`
- `Diamonds_Train_Loss_Train_Set_1.csv`
- `train_labels_diamonds.csv`

> **Note:** No parameter modifications or filename changes are required. Simply execute both notebooks sequentially.

---

## Stage 2 – Generate Table 3

Open

```text
InfluenceLossSummary.ipynb
```

Execute all notebook cells sequentially.

The notebook automatically reads all intermediate files generated in Stage 1 and computes the summary statistics reported in the paper.

No code modifications are required.

---

# Expected Output

Running the complete pipeline reproduces **Table 3** in the paper.

The notebook reports the following statistics for both **FOIF** and **TracIn** on the **SYN_A** and **Diamonds** datasets:

- ρₛ(L, I)
- ρₛ(L, |I|)
- HL@Top10%
- HL@Bottom10%
- HL@AbsTop10%

These statistics correspond directly to the values reported in **Table 3** of the paper.

---

# Notes

- The two influence-estimation notebooks only need to be executed once.
- No parameter changes or filename modifications are required throughout the experiment.
- The provided Diamonds intermediate files allow users to skip the computationally expensive influence-estimation stage.
- All notebooks assume that the required CSV files are located in the same directory as the notebooks.
