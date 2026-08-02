Please find How to Use.ipynb for detailed information for each folder and file.\
Each folder contains the respective experiment files and is set to the default synthetic experiment parameters.\
SimpleOverallFrameWork.ipynb provides the base code for training and estimating influence.\
The influence list for each experiment is provided within each folder.\
The usage of dataset is provided inside the Dataset Folder.


# Data-Side Robustness of Training-Data Influence Estimation

This repository contains the implementation and experimental framework accompanying our paper:
> **Data-Side Robustness of Training-Data Influence Estimation**  
> Tianyang Xie, Paolo Missier, and Huiping Chen

The project provides a reproducible notebook-based implementation for evaluating the data-side robustness of two representative training-data influence estimation methods:
- **First-Order Influence Function (FOIF)**
- **TracIn**

Implemented by Influenciae


The experiments study how influence estimates respond to changes in:

- training-set size;
- feature dimensionality;
- high-loss samples;
- local density;
- class imbalance.

The repository includes the code required to reproduce the experiments, figures, and tables reported in both the main paper and the supplementary material.

## Highlights

- Fully notebook-based experimental workflow
- Reproducible implementations of FOIF and TracIn
- Synthetic and real tabular datasets
- Stability and cross-method consistency evaluation
- Scripts and notebooks for reproducing paper figures and tables
- Additional analyses for noisy-label detection and data pruning

## Quick Navigation

- [Environment Setup](#environment-setup)
- [Requirements and Installation](#Requirements-and-Installation)
- [Reproducing the Paper](#reproducing-the-paper)
- [Repository Structure](#repository-structure)






# Environment Setup

The repository was developed and tested using the environment below. All experiments reported in the paper can be reproduced using this configuration.

| Component | Version |
|-----------|---------|
| Python | 3.10.8 |
| Jupyter Notebook | 7.3.2 |
| Operating System | Windows 11 |
| CUDA | Not required |
| GPU | Optional (all reported results in the paper were generated on CPU) |

The implementation is **fully notebook-based**. After installing the required dependencies, users can reproduce each experiment by opening the corresponding Jupyter notebook and executing all cells sequentially.



# Requirements and Installation

## 1. Install the common dependencies

The repository is designed to be executed using **Jupyter Notebook**.

Open any notebook in the repository and run the following cell to install the required Python packages:

```python
!python -m pip install --upgrade pip
!python -m pip install -r requirements.txt
```

After the installation is complete, restart the notebook kernel and execute all cells sequentially.

The `requirements.txt` file contains the packages used throughout the experiments, including TensorFlow, TensorFlow Datasets, NumPy, Pandas, SciPy, scikit-learn, Matplotlib, Seaborn, and Statsmodels.

## 2. Install an Influence-Estimation Implementation

The repository supports two closely related Influence Estimation implementations. The two options are provided because of compatibility differences between the original Influenciae package and the TensorFlow/TensorFlow Datasets versions used in this project.

The official Influenciae implementation does not support the TensorFlow Datasets (`tfds`) workflow adopted by several notebooks in this repository. Therefore, notebooks using the official implementation load the prepared CSV datasets included in the repository instead. These CSV files are directly converted from the corresponding TensorFlow Datasets and contain exactly the same data.

To support the original notebook workflow, we also provide a slightly modified version, **`influenciae_tabular`**, originally developed by CA-Fernandes. This implementation is compatible with the TensorFlow Datasets workflow, allowing datasets (e.g., `diamonds`) to be loaded directly through `tfds.load()`.

Both implementations support the same experimental pipeline and reproduce the results reported in the paper. The only difference is the dataset loading method.

| Implementation | Data-loading approach | Recommended use |
|---|---|---|
| Modified `influenciae_tabular` | TensorFlow Datasets (`tfds`) | Reproducing the original notebook workflow |
| Official Influenciae | Prepared CSV files | Simpler reproduction using the provided datasets |

> **Note:** Install only one Influenciae implementation in a given environment to avoid package conflicts.

### Option A: Modified `influenciae_tabular`

Open a Jupyter notebook from the repository and execute:

```python
!python -m pip install -e ./third_party/influenciae_tabular
```

Restart the notebook kernel after the installation is complete.

The corresponding notebooks use code such as:

```python
import tensorflow_datasets as tfds

ds, ds_info = tfds.load(
    "diamonds",
    split="train",
    with_info=True,
    as_supervised=True
)

df = tfds.as_dataframe(ds, ds_info)
```

### Option B: Official Influenciae with the provided CSV files

Open a Jupyter notebook from the repository and execute:

```python
!python -m pip install Influenciae
```

Restart the notebook kernel after the installation is complete.

The corresponding notebooks load the prepared datasets directly:

```python
import pandas as pd

df = pd.read_csv("data/diamonds.csv")
```

The CSV files are provided in this repository, so downloading the datasets through TensorFlow Datasets is not required.

## Which option should I use?

For the workflow closest to the one used during development, use the modified `influenciae_tabular` implementation with TensorFlow Datasets.

For the simplest reproduction path, use the official Influenciae package with the provided CSV files.




























