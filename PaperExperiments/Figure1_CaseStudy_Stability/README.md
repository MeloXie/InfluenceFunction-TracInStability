
# Figure 1: Case Study – Stability under Different Age Imputation Strategies

## Purpose

This experiment reproduces **Figure 1** in the paper, which investigates the stability of training-data influence estimation under two commonly used age imputation strategies on the Titanic dataset:

- Rounded Mean Imputation
- Median Imputation

The experiment compares how the influence rankings produced by **FOIF** and **TracIn** change when only the age imputation strategy is modified.

---

# Folder Contents

```text
Figure1_CaseStudy_Stability/
│
├── CaseStudy-Stability_RoundupMean_Median_Influence_Estimation.ipynb
├── CaseStudy-Stability-RoundMeanVSMedian.ipynb
│
├── train.csv
│
├── IF_600_*.csv
├── TC_600_*.csv
│
├── README.md
```

---

# Reproducing the Experiment

The experiment consists of two stages.

## Stage 1 – Generate Influence Scores

Open

```
CaseStudy-Stability_RoundupMean_Median_Influence_Estimation.ipynb
```

This notebook computes the FOIF and TracIn influence scores under different age imputation strategies.

### Step 1 – Select the Imputation Strategy

Comment and uncomment the age imputation cells in the notebook.

For **Rounded Mean Imputation**

```python
df = df.copy()

df["Age"] = df["Age"].fillna(
    df.groupby(["Pclass", "Sex"])["Age"].transform("mean")
)

round_imputed_age = True
```

For **Median Imputation**

```python
df = df.copy()

df["Age"] = df["Age"].fillna(
    df.groupby(["Pclass", "Sex"])["Age"].transform("median")
)
```

### Step 2 – Update the Output Filenames

When switching between Rounded Mean and Median imputation, remember to update the output filenames before executing the notebook.

This prevents previously generated influence files from being overwritten.

### Step 3 – Execute the Notebook

Run all notebook cells sequentially.

The notebook generates:

- FOIF influence files
- TracIn influence files
- Original-data files

---

## Stage 2 – Generate Figure 1

Open

```
CaseStudy-Stability-RoundMeanVSMedian.ipynb
```

This notebook loads the influence files generated in Stage 1 and produces the final paper figure.

Execute the notebook from beginning to end.

---

# Expected Output

The notebook produces the final comparison figure reported as **Figure 1** in the paper, illustrating the normalised influence-rank displacement under Rounded Mean and Median age imputation for both:

- FOIF
- TracIn

---

# Notes

- Execute **Stage 1** before **Stage 2** if reproducing the experiment from scratch.
- If the generated influence files are already available in this folder, Stage 1 can be skipped and Stage 2 can be executed directly to reproduce the published figure.
- All notebooks assume that the required CSV files are located in the same directory as the notebook.
