
# Figure 3: Stability under Different Feature Dimensionality

## Purpose

This experiment reproduces the feature-dimensionality heatmaps reported in the paper. It evaluates how the stability of **First-Order Influence Functions (FOIF)** and **TracIn** changes as additional features are introduced into the training data.

To reduce the effect of randomness, the experiment is repeated over **five independent runs** with different random seeds. The final heatmaps are obtained by averaging the pairwise weighted Kendall's Tau matrices across all runs.

---

# Folder Contents

```text
Figure3_FeatureDimension/
│
├── NumberOfFeaturesExperiment.ipynb
├── FeatureHeatmap-5Runs.ipynb
├── Mean5RunsHeatmap.ipynb
│
├── FeatureRun1/
├── FeatureRun2/
├── FeatureRun3/
├── FeatureRun4/
├── FeatureRun5/
│
├── FOIF_TauMatrix_Run1.csv
├── ...
├── FOIF_TauMatrix_Run5.csv
│
├── TracIn_TauMatrix_Run1.csv
├── ...
├── TracIn_TauMatrix_Run5.csv
│
└── README.md
```

---

# Reproducing the Experiment

> **⚠️ Reproduction Recommendation**
>
> Reproducing this experiment entirely from scratch can be **computationally expensive**, as it requires repeatedly training models and computing influence scores across multiple experimental settings and random seeds.
>
> To facilitate reproducibility, this repository provides all intermediate results generated during our experiments. We therefore **recommend using the provided intermediate files** to reproduce the final figures and tables. This approach reproduces the published results while significantly reducing the required execution time.
>
> Users who wish to verify the complete experimental pipeline may still execute all stages from scratch following the instructions below.


The experiment consists of three stages.

## Stage 1 – Generate Influence Scores

Open

```
NumberOfFeaturesExperiment.ipynb
```

This notebook computes the FOIF and TracIn influence scores under different feature-dimensionality settings.

### Step 1 – Select the Feature Configuration

Modify the feature configuration in the notebook.

```python
KS = [10,14,18,22,26,30,34,38,42]

n_noise = 90
rng = np.random.RandomState(seed)

X_noise = rng.normal(
    loc=0.0,
    scale=1.0,
    size=(X.shape[0], n_noise)
)

k = KS[...]
X = np.hstack([X, X_noise[:, :k]])
# k = 0
```

Each value of `k` corresponds to one feature-dimensionality setting. For the 10-feature setting, uncomment the last line k = 0.

### Step 2 – Execute One Experimental Run

Run the notebook for all ten feature settings.

For each feature setting, the notebook generates:

- one FOIF influence file;
- one TracIn influence file.

> **Important:** Update the output filenames for different feature settings to avoid overwriting previously generated results.

### Step 3 – Repeat for Five Runs

Repeat the experiment using **five different random seeds**.

Each run produces influence files stored under

```
FeatureRun1/
...
FeatureRun5/
```

After completing this stage, there should be:

- 10 FOIF influence files;
- 10 TracIn influence files;

for each of the five runs.

---

## Stage 2 – Generate the Kendall's Tau Matrices

Open

```
FeatureHeatmap-5Runs.ipynb
```

This notebook reads the influence files from each experimental run and computes the pairwise weighted Kendall's Tau similarity matrices for:

- FOIF
- TracIn

One Kendall's Tau matrix is produced for each run.

The generated matrices are saved as

```
FOIF_TauMatrix_Run1.csv
...
FOIF_TauMatrix_Run5.csv

TracIn_TauMatrix_Run1.csv
...
TracIn_TauMatrix_Run5.csv
```

---

## Stage 3 – Generate the Final Heatmaps

Open

```
Mean5RunsHeatmap.ipynb
```

This notebook reads the five Kendall's Tau matrices generated in Stage 2, averages them element-wise, and produces the final mean heatmaps reported in the paper.

---

# Expected Output

Running the complete pipeline reproduces the feature-dimensionality heatmaps reported in the paper for:

- FOIF
- TracIn

The final figures visualise the average weighted Kendall's Tau similarity over five independent runs.

---

# Notes

- Execute the three stages sequentially when reproducing the experiment from scratch.
- If the intermediate influence files and Kendall's Tau matrices are already available, Stages 1 and 2 can be skipped, and Stage 3 can be executed directly to regenerate the final paper figure.
- All notebooks assume that the required files are located in the same directory structure provided in this repository.
