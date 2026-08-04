# Chunk Entropy on the Diamonds Dataset

This supplementary experiment evaluates the chunk-contribution entropy on the **Diamonds** dataset. The procedure follows the same workflow as the chunk entropy experiment in the main paper, except that the statistics are averaged over **three independent runs**.

## Folder Contents

```text
ChunkEntropy_Diamonds/
│
├── Run1/
├── Run2/
├── Run3/
│
├── NumberOfSamplesExperiment-Diamonds.ipynb
├── ChunkAnalysis-Diamonds-Newest.ipynb
├── EntropyMeanSTDover3Runs-diamonds.ipynb
│
├── Entropy_Run_1_diamonds.csv
├── Entropy_Run_2_diamonds.csv
├── Entropy_Run_3_diamonds.csv
│
├── Entropy_vs_chunks_Run_1_diamonds.csv
├── Entropy_vs_chunks_Run_2_diamonds.csv
├── Entropy_vs_chunks_Run_3_diamonds.csv
│
├── diamonds.csv
│
└── README.md
```

---

## Reproducing the Experiment

The experiment consists of **three stages**.

### Stage 1 – Compute influence scores

Open

```
NumberOfSamplesExperiment-Diamonds.ipynb
```

This notebook computes the FOIF and TracIn influence scores for different training-set sizes.

Within each large run, modify

```python
train_df = nested_train_dfs[0]
```

to generate the ten training-set sizes (1K–10K samples).

For each training-set size, remember to update the output filenames before running the notebook to avoid overwriting previous results.

Repeat this procedure for all ten training-set sizes.

The experiment is repeated for **three independent runs**.

After each large run, **manually move** the generated influence-score files into the corresponding folder:

```
Run1/
Run2/
Run3/
```

---

### Stage 2 – Compute chunk entropy

Open

```
ChunkAnalysis-Diamonds-Newest.ipynb
```

Before running the notebook:

- update the folder name (`Run1`, `Run2`, or `Run3`) when loading the influence-score files;
- update

```python
run_id = 1
```

to match the current run.

Execute all notebook cells.

Each run generates:

- `Entropy_Run_<run_id>_diamonds.csv`
- `Entropy_vs_chunks_Run_<run_id>_diamonds.csv`

After completing all three runs, a total of **six summary files** will be generated.

---

### Stage 3 – Compute the final statistics

Open

```
EntropyMeanSTDover3Runs-diamonds.ipynb
```

This notebook automatically reads all the entropy summary files and computes the mean and standard deviation over the three runs.

Simply execute all notebook cells sequentially.

---

## Expected Output

Running

```
EntropyMeanSTDover3Runs-diamonds.ipynb
```

reproduces the chunk-contribution entropy statistics (mean ± standard deviation over three runs) reported in the supplementary material.

---

## Notes

- This experiment follows the same workflow as the chunk entropy experiment in the main paper but uses the **Diamonds** dataset.
- Three independent runs are required.
- After each large run, remember to **manually move** the generated influence-score files into the corresponding `Run1`, `Run2`, or `Run3` folder before proceeding.
- The provided intermediate influence-score files allow the final entropy statistics to be reproduced directly without recomputing the influence estimation stage.
