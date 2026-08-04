# Aggregation Strategy

This experiment compares the **median aggregation strategy** proposed in our work with the **Fragile aggregation strategy** introduced in the Fragile paper. Both methods are evaluated under increasing training-set sizes to compare the stability of their influence rankings.

## Folder Contents

```text
AggregationStrategy/
│
├── SyntheticRealStart-TrainSize.ipynb
├── SyntheticRealStart-TrainSize-Fragile.ipynb
├── FragileVSOurMedian.ipynb
│
├── TrainSet_Syn_Median/
│
├── TrainSet_Fragile/
│
└── README.md
```

## Reproducing the Experiment

The experiment consists of **three stages**.

### Stage 1 – Compute influence scores using the proposed median aggregation

Open

```
SyntheticRealStart-TrainSize.ipynb
```

This notebook computes the FOIF and TracIn influence scores using the proposed **median aggregation** strategy.

The experiment is repeated for five training-set sizes.

Modify

```python
train_df = nested_train_dfs[4]
```

to select

| Index | Training-set size |
|------:|------------------:|
| 0 | 1,000 |
| 1 | 2,000 |
| 2 | 4,000 |
| 3 | 8,000 |
| 4 | 16,000 |

For each training-set size, update the output filenames before running the notebook to avoid overwriting previous results.

For example,

```python
TracIn_sorted.to_csv("TrainSet_Syn_Median/TC_Train_Set_1.csv", index=False)
df_sorted.to_csv("TrainSet_Syn_Median/IF_Train_Set_1.csv", index=False)
```

should be updated so that each training-set size is saved using a unique filename.

After completing all five runs, the folder

```
TrainSet_Syn_Median/
```

should contain ten files (five FOIF files and five TracIn files).

---

### Stage 2 – Compute influence scores using the Fragile aggregation

Open

```
SyntheticRealStart-TrainSize-Fragile.ipynb
```

This notebook follows the same procedure but adopts the **highest-loss aggregation strategy** used in the Fragile paper.

Again, repeat the experiment for the five training-set sizes by modifying

```python
train_df = nested_train_dfs[4]
```

For each run, update the output filenames before execution, for example,

```python
df_influence.to_csv("TrainSet_Fragile/IF_Train_Set_Fragile_5.csv", index=False)
TracIn_sorted.to_csv("TrainSet_Fragile/TC_Train_Set_Fragile_5.csv", index=False)
```

After all five runs, the folder

```
TrainSet_Fragile/
```

should contain ten files (five FOIF files and five TracIn files).

---

### Stage 3 – Generate the comparison figure

Open

```
FragileVSOurMedian.ipynb
```

This notebook reads the influence-score files from

```
TrainSet_Fragile/
```

and

```
TrainSet_Syn_Median/
```

No parameter changes are required.

Simply execute all notebook cells sequentially.

---

## Expected Output

Running

```
FragileVSOurMedian.ipynb
```

generates the Kendall Tau comparison plot between the Fragile aggregation strategy and the proposed median aggregation strategy across different training-set sizes, corresponding to the figure reported in the supplementary material.

---

## Notes

- Five separate runs are required, corresponding to training-set sizes of **1K, 2K, 4K, 8K, and 16K**.
- Remember to update the output filenames after each run to prevent previously generated influence scores from being overwritten.
- The provided intermediate influence-score files allow the comparison figure to be reproduced directly without recomputing the influence estimation stage.
