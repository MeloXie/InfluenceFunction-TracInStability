# Conditional Spearman Correlations

This supplementary experiment reports the **conditional Spearman correlations** between training loss and influence scores presented in the supplementary material.

## Folder Contents

```text
Conditional_Spearman/
│
├── Influence_Loss_Influence_Estimation_Adult.ipynb
├── InfluenceLossSummary.ipynb
│
├── *.csv
│
└── README.md
```

---

## Reproducing the Experiment

This experiment follows **exactly the same workflow** as the **Influence Loss Statistics** experiment in the main paper.

Please first refer to

```
PaperExperiments/Table3_Influence_Loss_Stats/README.md
```

for the complete reproduction procedure.

The provided synthetic and Diamonds datasets use exactly the same intermediate files as the main-paper experiment and therefore **do not need to be recomputed**.

The only additional experiment included here is the **Adult** dataset.

### Step 1. Generate Adult influence scores (optional)

Open

```
Influence_Loss_Influence_Estimation_Adult.ipynb
```

and simply execute the notebook.

The notebook generates:

- FOIF influence scores;
- TracIn influence scores;
- training-loss values;
- training labels.

The generated filenames are already compatible with the summary notebook and therefore require **no manual modification**.

> **Note:** The Adult dataset contains over **40,000 training samples**, so recomputing the influence scores from scratch may take a considerable amount of time. The repository already provides the generated CSV files, which are recommended for reproducing the supplementary results.

---

### Step 2. Compute the conditional Spearman statistics

Open

```
InfluenceLossSummary.ipynb
```

and execute all cells.

The notebook automatically reads the provided synthetic, Diamonds, and Adult CSV files and computes all reported statistics.

---

## Expected Output

Running the notebook reproduces the conditional Spearman statistics reported in the supplementary material, including:

- Spearman correlation between training loss and signed influence;
- class-conditional Spearman correlations;
- positive/negative influence conditional correlations;
- high-loss overlap statistics.

These statistics correspond to the supplementary Conditional Spearman table.

---

## Notes

- The workflow is identical to the **Influence Loss Statistics** experiment in the main paper.
- Only the Adult dataset requires an additional influence-estimation step.
- Since the Adult influence estimation is computationally expensive, using the provided intermediate CSV files is recommended for reproducing the reported results.
