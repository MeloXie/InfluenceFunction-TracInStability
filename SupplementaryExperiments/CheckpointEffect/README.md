# Checkpoint Effect

This supplementary experiment evaluates the effectiveness of reducing the number of TracIn checkpoints during influence estimation. The resulting influence rankings obtained using different checkpoint budgets are compared against the full **300-checkpoint TracIn** ranking using **Weighted Kendall Tau** and **Top-10% Overlap**.

## Folder Contents

```text
CheckpointEffect/
│
├── RealRun1/
├── RealRun2/
├── RealRun3/
│
├── CheckpointsExperiment.ipynb
├── CheckpointEffectiveness.ipynb
│
└── README.md
```

---

## Reproducing the Experiment

The experiment consists of **two stages**.

### Stage 1 – Compute TracIn influence using different checkpoint budgets

Open

```
CheckpointsExperiment.ipynb
```

This notebook computes the TracIn influence scores using different percentages of the available model checkpoints.

Modify

```python
model_list_selected_indices = select_checkpoints(
    model_list_full,
    0.05
)
```

to evaluate the desired checkpoint percentage.

The following checkpoint percentages are evaluated:

- 5%
- 10%
- 20%
- 40%
- 60%
- 80%
- 100% (Full 300 checkpoints)

For each checkpoint percentage, remember to update the output filename before running the notebook. For example,

```python
TracIn_sorted.to_csv(
    "RealRun1/TC_Train_Set_Checkpoints_05per.csv",
    index=False
)
```

should be modified accordingly so that every checkpoint budget is saved using a unique filename.

Repeat this process for all checkpoint percentages.

The experiment is repeated for **three independent runs**, producing the corresponding files inside

```
RealRun1/
RealRun2/
RealRun3/
```

---

### Stage 2 – Compute checkpoint effectiveness

Open

```
CheckpointEffectiveness.ipynb
```

If the generated filenames follow the provided naming convention, the notebook automatically reads all files from the three runs.

Simply execute all notebook cells sequentially.

The notebook compares each reduced checkpoint budget against the full **300-checkpoint** TracIn ranking and reports:

- Weighted Kendall Tau
- Top-10% Overlap

The final statistics correspond to the supplementary-material table.

---

## Expected Output

Running

```
CheckpointEffectiveness.ipynb
```

produces the average

- Weighted Kendall Tau
- Top-10% Overlap

between each checkpoint percentage and the full 300-checkpoint TracIn ranking.

---

## Notes

- The experiment should be repeated for **three independent runs**.
- Ensure that the generated filenames follow the provided naming convention so that `CheckpointEffectiveness.ipynb` can load them automatically.
- The runtime values reported in the supplementary material correspond to the hardware used in our experiments and therefore may not be reproduced exactly on different systems.
- If users simply wish to inspect the runtime of a particular checkpoint budget, the runtime is printed directly in `CheckpointsExperiment.ipynb` after each TracIn influence estimation run, for example:

```python
runtime = end - start
print(runtime)
```

The reported runtime measures **only the TracIn influence estimation stage**.
