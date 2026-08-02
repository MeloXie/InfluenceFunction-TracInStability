# Figure 5: Influence Difference across Distance Bands

## Purpose

This experiment reproduces **Figure 5** in the paper, which investigates how the average difference in influence scores changes as the distance between training samples increases.

The experiment first computes the influence scores using **First-Order Influence Functions (FOIF)** and **TracIn**, then groups pairs of training samples into predefined distance bands and computes the average influence difference within each band. Finally, the results are visualised as the line plot reported in the paper.

---

# Folder Contents

```text
Figure5_Distance_Influence/
│
├── Distance_Influence_Estimation.ipynb
├── RadiusDistanceSummary.ipynb
├── Distance_Difference_Plot.ipynb
│
├── IF_Train_Set_8_seed42.csv
├── TC_Train_Set_8_seed42.csv
│
├── summary_if.csv
├── summary_tc.csv
│
└── README.md
```

---

# Reproducing the Experiment

The experiment consists of three stages.

## Stage 1 – Generate Influence Scores

Open

```
Distance_Influence_Estimation.ipynb
```

Execute all notebook cells sequentially.

The notebook computes the influence scores for both methods and generates:

- `IF_Train_Set_8_seed42.csv`
- `TC_Train_Set_8_seed42.csv`

---

## Stage 2 – Generate Distance-Band Summaries

Open

```
RadiusDistanceSummary.ipynb
```

This notebook regenerates the same training and test sets used in Stage 1 in order to compute the pairwise distances between training samples.

Using the influence-score files generated in Stage 1, the notebook computes the average influence difference within each predefined distance band.

### Step 1 – Generate the FOIF Summary

Load

```
IF_Train_Set_8_seed42.csv
```

and save the result as

```
summary_if.csv
```

### Step 2 – Generate the TracIn Summary

Comment the FOIF loading code and enable the TracIn loading code.

Load

```
TC_Train_Set_8_seed42.csv
```

and save the result as

```
summary_tc.csv
```

> **Important:** The notebook should be executed twice: once for FOIF and once for TracIn.

---

## Stage 3 – Generate Figure 5

Open

```
Distance_Difference_Plot.ipynb
```

Execute all notebook cells sequentially.

The notebook reads:

- `IF_Train_Set_8_seed42.csv`
- `TC_Train_Set_8_seed42.csv`
- `summary_if.csv`
- `summary_tc.csv`

and generates the final figure reported in the paper.

---

# Expected Output

Running the complete pipeline reproduces **Figure 5** in the paper.

The generated figure is saved in the experiment's root directory.


---

# Notes

- Execute the three stages sequentially when reproducing the experiment from scratch.
- `RadiusDistanceSummary.ipynb` must be executed **twice**, once for FOIF and once for TracIn, by switching the input influence file and output summary filename.
- All notebooks assume that the required CSV files are located in the same directory as the notebooks.
