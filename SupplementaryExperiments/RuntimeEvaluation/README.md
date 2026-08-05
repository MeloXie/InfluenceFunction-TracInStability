# Runtime Evaluation

This supplementary experiment measures the runtime of **First-Order Influence Functions (FOIF)** and **TracIn** under different dataset sizes and feature dimensionalities.

The experiment evaluates four configurations:

- 1,000 samples and 10 features
- 10,000 samples and 10 features
- 1,000 samples and 52 features
- 10,000 samples and 52 features

## Folder Contents

```text
RuntimeEvaluation/
│
├── RuntimeMeasurement.ipynb
└── README.md
```

---

## Reproducing the Experiment

Open

```text
RuntimeMeasurement.ipynb
```

The notebook measures the runtime of the FOIF and TracIn influence-estimation stages.

### Step 1. Select the feature dimensionality

Locate:

```python
features_to_test = 10
selected_features = [f"feature_{i+1}" for i in range(features_to_test)]
```

Set:

```python
features_to_test = 10
```

for the 10-feature setting, or:

```python
features_to_test = 52
```

for the 52-feature setting.

---

### Step 2. Select the training-set size

Locate:

```python
train_df = nested_train_dfs[9]
```

Use:

```python
train_df = nested_train_dfs[0]
```

for 1,000 training samples, or:

```python
train_df = nested_train_dfs[9]
```

for 10,000 training samples.

Repeat the notebook for all four combinations of dataset size and feature dimensionality.

---

### Step 3. Record the FOIF and TracIn runtimes

The FOIF runtime is printed by:

```python
end_if = time.perf_counter()
runtime_if = end_if - start_if
print(f"FOIF Runtime: {runtime_if:.4f} seconds")
```

The TracIn runtime is printed by:

```python
end_tc = time.perf_counter()
runtime_tc = end_tc - start_tc
print(f"TracIn Runtime: {runtime_tc:.4f} seconds")
```

Record both values after each execution.

Repeat each configuration multiple times and compute the mean and standard deviation of the recorded runtimes.

---

## Expected Output

The notebook reports the execution time, in seconds, for the FOIF and TracIn influence-estimation stages under each configuration.

The recorded values can be summarized as:

```text
mean ± standard deviation
```

over repeated runs.

---

## Notes

- Runtime values depend on hardware, operating-system activity, package versions, and other background processes.
- Therefore, the exact runtime values reported in the supplementary material may not be reproduced, even when using the same hardware.
- The reported runtimes measure only the influence-estimation stage.
- All runtime experiments reported in the supplementary material were executed three times, with the mean and standard deviation calculated across those runs.
- For a fair comparison, use the same machine and software environment for all four configurations.
