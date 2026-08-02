
# Figure 2: Case Study – Consistency between FOIF and TracIn

## Purpose

This experiment reproduces **Figure 2** in the paper, which compares the consistency between **First-Order Influence Functions (FOIF)** and **TracIn** on the Titanic dataset.

The notebook computes the influence scores produced by both methods and evaluates their agreement using multiple complementary metrics, including:

- Rank-Rank Plot
- Weighted Kendall's Tau
- Top-10% Overlap
- Percentage of Training Samples with Different Influence Signs

---

# Folder Contents

```text
Figure2_CaseStudy_Consistency/
│
├── CaseStudy_Consistency.ipynb
├── README.md
├── train.csv
```

---

# Reproducing the Experiment

Open

```
CaseStudy_Consistency.ipynb
```

and execute all notebook cells sequentially.

The notebook will:

1. Load the Titanic dataset.
2. Train the neural network used in the paper.
3. Compute the FOIF influence scores.
4. Compute the TracIn influence scores.
5. Compare the two methods using:
   - Rank-Rank Plot
   - Weighted Kendall's Tau
   - Top-10% Overlap
   - Percentage of Different Influence Signs
6. Generate the final paper figure.

---

# Expected Output

Running the notebook reproduces **Figure 2** in the paper, showing the percentile-rank comparison between FOIF and TracIn.

The notebook also reports the quantitative consistency metrics used in the paper, including:

- Weighted Kendall's Tau
- Top-10% Overlap
- Percentage of Different Influence Signs

---

# Notes

- The notebook is self-contained and does not require any intermediate files.
- Execute all cells sequentially to reproduce the reported results.
