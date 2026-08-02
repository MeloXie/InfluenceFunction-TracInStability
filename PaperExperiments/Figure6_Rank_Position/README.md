
# Figure 6: Influence Rank Positions under Sparse and Dense Regions

## Purpose

This experiment reproduces **Figure 6** in the paper, which compares the distribution of training-sample influence ranks between sparse and dense regions.

The experiment first computes the influence scores for the synthetic sparse-dense dataset using **First-Order Influence Functions (FOIF)** and **TracIn**. The influence scores are then combined with the corresponding region labels to produce the rank-position histograms reported in the paper.

---

# Folder Contents

```text
Figure6_Rank_Position/
│
├── SmallLargeDensityExperiment-Newersetting.ipynb
├── SmallLargeDensity-RankPosition.ipynb
│
├── IF_sp1_de01_newset.csv
├── TC_sp1_de01_newset.csv
├── label_sp1_de01_newset.csv
│
└── README.md
```

---

# Reproducing the Experiment

The experiment consists of two stages.

## Stage 1 – Generate Influence Scores

Open

```
SmallLargeDensityExperiment-Newersetting.ipynb
```

Execute all notebook cells sequentially.

The notebook computes the influence scores for both methods and generates:

- `IF_sp1_de01_newset.csv`
- `TC_sp1_de01_newset.csv`

---

## Stage 2 – Generate Figure 6

Open

```
SmallLargeDensity-RankPosition.ipynb
```

This notebook loads the influence-score files together with the sparse/dense region labels and generates the rank-position histograms.

### Step 1 – Select the Influence Method

The notebook processes one influence method at a time.

For **FOIF**, use

```python
ranked_1 = IF_1.merge(Label_1, left_on="Train_ID", right_on="id", how="left")
```

For **TracIn**, replace `IF_1` with `TC_1`:

```python
ranked_1 = TC_1.merge(Label_1, left_on="Train_ID", right_on="id", how="left")
```

### Step 2 – Save the Figure

When generating the TracIn figure, remember to update the output filename accordingly.

For example,

```
SmallLargeDensity_IF_SparseDense_count_newsetting.png
```

should be changed to

```
SmallLargeDensity_TC_SparseDense_count_newsetting.png
```

Execute the notebook twice, once for FOIF and once for TracIn.

---

# Expected Output

Running the complete pipeline reproduces **Figure 6** in the paper.

The generated figures are saved in the experiment's root directory:

- `SmallLargeDensity_IF_SparseDense_count_newsetting.png`
- `SmallLargeDensity_TC_SparseDense_count_newsetting.png`

These correspond to the sparse-versus-dense influence-rank distributions for:

- FOIF
- TracIn

---

# Notes

- Execute Stage 1 before Stage 2 if reproducing the experiment from scratch.
- `SmallLargeDensity-RankPosition.ipynb` should be executed **twice**, once using the FOIF influence scores and once using the TracIn influence scores.
- When switching between FOIF and TracIn, remember to update both the loaded influence file and the output figure filename.
- All notebooks assume that the required CSV files are located in the same directory as the notebooks.
