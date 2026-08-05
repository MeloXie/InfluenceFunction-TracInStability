# Distance Influence (Diamonds)

This supplementary experiment reproduces the distance-based influence analysis on the **Diamonds** dataset.

## Folder Contents

```text
Distance_Influence/
│
├── Distance_Influence_Estimation_Diamonds.ipynb
├── RadiusExperimentAnalysis-Diamonds.ipynb
├── Distance_Difference_Plot.ipynb
│
├── IF_Train_Set_Diamonds_Neighbor.csv
├── TC_Train_Set_Diamonds_Neighbor.csv
├── summary_if_dia.csv
├── summary_tc_dia.csv
│
├── diamonds.csv
└── README.md
```

---

## Reproducing the Experiment

This experiment follows the same workflow as the **Distance Influence** experiment in the main paper, but uses the **Diamonds** dataset.

### Step 1. Compute influence scores

Open

```
Distance_Influence_Estimation_Diamonds.ipynb
```

and execute all cells.

The notebook computes the FOIF and TracIn influence scores for the Diamonds dataset.

No code modification is required.

---

### Step 2. Compute the distance-band summaries

Open

```
RadiusExperimentAnalysis-Diamonds.ipynb
```

and execute the notebook.

The notebook computes the average influence differences within each distance band.

To generate the summaries separately for FOIF and TracIn, change the loaded influence file accordingly.

For TracIn:

```python
ranked_df = pd.read_csv("TC_Train_Set_Diamonds_Neighbor.csv")
```

For FOIF:

```python
ranked_df = pd.read_csv("IF_Train_Set_Diamonds_Neighbor.csv")
```

Also remember to save the corresponding summary file.

For example:

```python
summary.to_csv("summary_tc_dia.csv", index=False)
```

or

```python
summary.to_csv("summary_if_dia.csv", index=False)
```

---

### Step 3. Generate the final plot

Open

```
Distance_Difference_Plot.ipynb
```

Verify that the notebook loads the generated influence-score and summary files:

```python
IF_df = pd.read_csv("IF_Train_Set_Diamonds_Neighbor.csv")
TC_df = pd.read_csv("TC_Train_Set_Diamonds_Neighbor.csv")

summary_if = pd.read_csv("summary_if_dia.csv")
summary_tc = pd.read_csv("summary_tc_dia.csv")
```

Execute the notebook to generate and save the final distance-influence plot.

---

## Expected Output

Running the notebook reproduces the supplementary Diamonds distance-influence figure, showing the normalised mean absolute influence-score difference across different distance bands for both FOIF and TracIn.

---

## Notes

- This experiment follows the same workflow as the main-paper **Distance Influence** experiment.
- No filename modifications are required apart from switching between the FOIF and TracIn input files when generating the summary statistics.
- This experiment uses the **balanced Diamonds subset** provided in this repository rather than the full Diamonds dataset.
- The provided intermediate CSV files can be used directly to reproduce the reported results without rerunning the influence-estimation stage.
