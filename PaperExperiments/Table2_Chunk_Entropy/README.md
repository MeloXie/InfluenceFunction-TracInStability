
# Table 2: Chunk-Contribution Entropy across Training-Set Sizes

## Purpose

This experiment reproduces **Table 2** in the paper, which reports the normalised chunk-contribution entropy of **First-Order Influence Functions (FOIF)** and **TracIn** under different:

- numbers of data chunks, \(n\); and
- Top-\(k\) thresholds.

The experiment evaluates whether influential training samples are distributed evenly across data chunks as the training set expands.

To account for variation caused by data partitioning and random initialisation, the complete experiment is repeated over **five independent large runs**. The final table reports the mean and standard deviation of the entropy values across these five runs.

> **⚠️ Reproduction Recommendation**
>
> Reproducing this experiment entirely from scratch is computationally expensive. It requires five independent large runs, each containing ten training-set-size settings and influence estimation with both FOIF and TracIn.
>
> In total, full reproduction generates **100 influence-score files**:
>
> - 5 large runs;
> - 10 training-set-size settings per run;
> - 1 FOIF and 1 TracIn file per setting.
>
> The influence-score files for all five runs are therefore provided in this repository. We recommend starting from **Stage 2** using these intermediate files unless full end-to-end reproduction is required.

---

# Folder Contents

```text
Table2_Chunk_Entropy/
│
├── NumberOfSamples-InfluenceEstimation.ipynb
├── ChunkAnalysis.ipynb
├── EntropyMeanSTDover5Runs.ipynb
│
├── Run1/
├── Run2/
├── Run3/
├── Run4/
├── Run5/
│
├── Entropy_Run_1.csv
├── Entropy_Run_2.csv
├── Entropy_Run_3.csv
├── Entropy_Run_4.csv
├── Entropy_Run_5.csv
│
├── Entropy_vs_chunks_Run_1.csv
├── Entropy_vs_chunks_Run_2.csv
├── Entropy_vs_chunks_Run_3.csv
├── Entropy_vs_chunks_Run_4.csv
├── Entropy_vs_chunks_Run_5.csv
│
└── README.md
```

Each `RunX/` folder contains the FOIF and TracIn influence-score files generated for the ten training-set-size settings.
The `Entropy_Run_X.csv` and `Entropy_vs_chunks_Run_X.csv` files contain the entropy summaries generated for each large run and are used by `EntropyMeanSTDover5Runs.ipynb` to compute the mean and standard deviation reported in Table 2.

---

# Reproducing the Experiment

The experiment consists of three stages.

## Stage 1 – Generate Influence Scores

Open

```text
NumberOfSamples-InfluenceEstimation.ipynb
```

This notebook generates the FOIF and TracIn influence scores for training-set sizes ranging from 1,000 to 10,000 samples.

### Step 1 – Select the Training-Set Size

Locate the following line:

```python
train_df = nested_train_dfs[9]
```

The index selects one of the ten nested training sets:

| Index | Training-set size |
|------:|------------------:|
| 0 | 1,000 |
| 1 | 2,000 |
| 2 | 3,000 |
| 3 | 4,000 |
| 4 | 5,000 |
| 5 | 6,000 |
| 6 | 7,000 |
| 7 | 8,000 |
| 8 | 9,000 |
| 9 | 10,000 |

Run the notebook once for each index from `0` to `9`.

For each training-set-size setting, the notebook generates:

- one FOIF influence-score file; and
- one TracIn influence-score file.

Therefore, one large run generates:

- 10 FOIF files;
- 10 TracIn files;
- 20 influence-score files in total.

> **Important:** Update the saved filenames for each training-set-size setting to avoid overwriting previously generated files.

### Step 2 – Select the Large Run

Locate the following configuration:

```python
train_pool = 10000
test_size = 500
train_sizes = [1000, 2000, 3000, 4000, 5000, 6000, 7000, 8000, 9000, 10000]
n_features = 10
seed = 42
sep = 3

times = 0
shuffle_seed = seed + times
```

Change `times` from `0` to `4` to generate the five independent large runs:

| `times` | Recommended folder |
|--------:|---------------|
| 0 | `Run1/` |
| 1 | `Run2/` |
| 2 | `Run3/` |
| 3 | `Run4/` |
| 4 | `Run5/` |

For each value of `times`, repeat the ten training-set-size settings described above.

Each large run generates:

- 10 FOIF influence-score files;
- 10 TracIn influence-score files.

> **Important:** The notebook saves all generated files into the **same directory as `NumberOfSamples-InfluenceEstimation.ipynb`**. It **does not automatically place them into the `Run1`–`Run5` folders**.
>
> After completing each large run (20 files), **manually move** the generated files into the corresponding run folder (`Run1`, `Run2`, ..., `Run5`) before starting the next large run. This prevents the files from being overwritten by subsequent runs.`

---

## Stage 2 – Compute Chunk-Contribution Entropy

Open

```text
ChunkAnalysis.ipynb
```

This notebook reads the FOIF and TracIn influence-score files from one large run and computes the chunk-contribution entropy under different numbers of chunks and Top-\(k\) thresholds.

### Step 1 – Select the Run Folder

Locate the cells that read the influence-score files:

```python
IF_1 = pd.read_csv("Run1/IF_Train_Set_1.csv")
IF_2 = pd.read_csv("Run1/IF_Train_Set_2.csv")
...
IF_10 = pd.read_csv("Run1/IF_Train_Set_10.csv")

TC_1 = pd.read_csv("Run1/TC_Train_Set_1.csv")
TC_2 = pd.read_csv("Run1/TC_Train_Set_2.csv")
...
TC_10 = pd.read_csv("Run1/TC_Train_Set_10.csv")
```

For each large run, replace `Run1` with the corresponding folder name:

```text
Run1
Run2
Run3
Run4
Run5
```

### Step 2 – Set the Run Identifier

Locate:

```python
run_id = 1
```

Update it to match the selected run:

| Folder | `run_id` |
|---|---:|
| `Run1/` | 1 |
| `Run2/` | 2 |
| `Run3/` | 3 |
| `Run4/` | 4 |
| `Run5/` | 5 |

### Step 3 – Save the Run-Level Entropy Results

The notebook generates two result files for each run:

```text
Entropy_Run_1.csv
Entropy_vs_Chunks_Run_1.csv
```

with the run number changing from `1` to `5`.

The first file stores entropy values across Top-\(k\) settings, while the second stores entropy values across different numbers of chunks.

> **Important:** `ChunkAnalysis.ipynb` must be executed separately for all five run folders. Ensure that both the input folder names and `run_id` are updated consistently.

After completing Stage 2, ten entropy-summary files should be available:

- 5 `Entropy_Run_X.csv` files;
- 5 `Entropy_vs_Chunks_Run_X.csv` files.

---

## Stage 3 – Generate Table 2 Statistics

Open

```text
EntropyMeanSTDover5Runs.ipynb
```

This notebook reads the ten run-level entropy-summary files generated in Stage 2 and computes the mean and standard deviation across the five large runs.

Execute all cells sequentially.

The resulting statistics correspond to the values reported in **Table 2** of the paper for:

- FOIF;
- TracIn;
- different Top-\(k\) thresholds; and
- different numbers of chunks.

---

# Expected Output

Running the complete pipeline reproduces the mean and standard-deviation values reported in **Table 2**.

The final output contains normalised chunk-contribution entropy values for:

| Method | Top-\(k\) values | Numbers of chunks |
|---|---|---|
| FOIF | 10, 50, 100, 500 | 2, 4, 6, 8, 10 |
| TracIn | 10, 50, 100, 500 | 2, 4, 6, 8, 10 |

The final values are reported as:

```text
mean ± standard deviation
```

over the five independent large runs.

---

# Notes

- Full end-to-end reproduction requires five large runs and 100 influence-score files.
- **After each large run, manually move the generated influence-score files into the corresponding `RunX/` folder before starting the next run.**
- The provided `Run1/` to `Run5/` folders allow users to skip the computationally expensive influence-estimation stage.
- For fast reproduction, begin with `ChunkAnalysis.ipynb` using the provided influence-score files.
- To regenerate only the final table statistics, run `EntropyMeanSTDover5Runs.ipynb` using the provided run-level entropy files.
- When processing each large run in `ChunkAnalysis.ipynb`, update both:
  - the folder name in all input paths; and
  - the corresponding `run_id`.
- All notebooks assume that the provided directory structure is preserved.
