# Figure 4: Relationship between Training Loss and Influence Scores

## Purpose

This experiment reproduces **Figure 4** in the paper, which investigates the relationship between the training loss of individual training samples and their corresponding influence scores estimated by **First-Order Influence Functions (FOIF)** and **TracIn**.

The analysis is performed on both the **synthetic dataset (SYN_A)** and the **Diamonds dataset**. For each dataset, the experiment computes the influence score and training loss of every training sample, followed by a regression analysis to visualise their relationship.

> **⚠️ Reproduction Recommendation**
>
> The synthetic dataset can be reproduced from scratch within a reasonable amount of time. However, reproducing the Diamonds experiment from scratch requires influence estimation on the full Diamonds dataset (over **50,000 training samples**) and may therefore take considerably longer.
>
> To facilitate reproducibility, the intermediate influence-score and training-loss files generated during our experiments are included in this repository. We recommend using these provided files when reproducing the Diamonds results, while users who wish to verify the complete experimental pipeline may still execute Stage 1 from scratch.
---

# Folder Contents

```text
Figure4_Influence_VS_Loss/
│
├── Influence_Loss_Influence_Estimation.ipynb
├── Influence_Loss_Influence_Estimation_Diamonds.ipynb
│
├── InfluenceVSLoss.ipynb
├── InfluenceVSLoss-Diamonds.ipynb
│
├── IF_Train_Set_1.csv
├── TC_Train_Set_1.csv
├── Train_Loss_Train_Set_1.csv
│
├── Diamonds_IF_Train_Set_1.csv
├── Diamonds_TC_Train_Set_1.csv
├── Diamonds_Train_Loss_Train_Set_1.csv
│
└── README.md
```

---

# Reproducing the Experiment

The experiment consists of two stages.

## Stage 1 – Generate Influence Scores and Training Loss

For the synthetic dataset, open

```
Influence_Loss_Influence_Estimation.ipynb
```

For the Diamonds dataset, open

```
Influence_Loss_Influence_Estimation_Diamonds.ipynb
```

Execute all notebook cells sequentially.

Each notebook computes:

- the FOIF influence scores;
- the TracIn influence scores; and
- the training loss for every training sample.

The generated intermediate files are:

### Synthetic Dataset

- `IF_Train_Set_1.csv`
- `TC_Train_Set_1.csv`
- `Train_Loss_Train_Set_1.csv`

### Diamonds Dataset

- `Diamonds_IF_Train_Set_1.csv`
- `Diamonds_TC_Train_Set_1.csv`
- `Diamonds_Train_Loss_Train_Set_1.csv`

> **Note:** Unlike some other experiments in this repository, the filenames do **not** need to be modified. Simply executing the notebooks once will generate the required intermediate files.

---

## Stage 2 – Generate Figure 4

For the synthetic dataset, open

```
InfluenceVSLoss.ipynb
```

For the Diamonds dataset, open

```
InfluenceVSLoss-Diamonds.ipynb
```

Execute all notebook cells sequentially.

These notebooks load the intermediate files generated in Stage 1, fit the regression models, and generate the final plots reported in the paper.

---

# Expected Output

Executing the complete pipeline reproduces **Figure 4** in the paper.

The following figures will be generated and saved in the experiment's root directory:

- `Outliers_Synthetic_IF.png`
- `Outliers_Synthetic_TC.png`
- `Outliers_Diamonds_IF_Large.png`
- `Outliers_Diamonds_TC_Large.png`

These four figures correspond to the relationship between training loss and influence score for:

| Output File | Dataset | Method |
|-------------|---------|--------|
| `Outliers_Synthetic_IF.png` | SYN_A | FOIF |
| `Outliers_Synthetic_TC.png` | SYN_A | TracIn |
| `Outliers_Diamonds_IF_Large.png` | Diamonds | FOIF |
| `Outliers_Diamonds_TC_Large.png` | Diamonds | TracIn |


---

# Notes

- Execute Stage 1 only if you wish to regenerate the influence scores and training losses from scratch.
- Stage 2 can be executed directly using the provided intermediate files.
- All notebooks assume that the required CSV files are located in the same directory as the notebooks.
