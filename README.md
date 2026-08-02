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


## Quick Start (Recommended)

The repository provides a notebook, **`00_Install_Requirements.ipynb`**, for quick installation of all required packages.

Simply open the notebook in Jupyter Notebook and execute cells sequentially. The notebook will install the common dependencies and provide the installation options for the supported influence-estimation implementations. Please only install one influence-estimation implementation.

After the installation is complete, **restart the notebook kernel** before running the experiment notebooks.

If you prefer to install the packages manually, the following instructions can be followed.

## 1. Install the Common Dependencies

The repository is designed to be executed using **Jupyter Notebook**.

Open any notebook in the repository and run the following cell to install the required Python packages:

```python
!python -m pip install --upgrade pip
!python -m pip install -r requirements.txt
```

After the installation is complete, restart the notebook kernel before executing the experiment notebooks.

The `requirements.txt` file contains the common dependencies used throughout the experiments, including TensorFlow, NumPy, Pandas, SciPy, scikit-learn, Matplotlib, Seaborn, and Statsmodels.

## 2. Install an Influence-Estimation Implementation


The experiments in this repository support two closely related implementations of the influence-estimation framework.

The modified **`influenciae_tabular`** implementation, originally developed by CA-Fernandes, incorporates updates to improve dependency compatibility (e.g., NumPy-related compatibility) while preserving the same influence estimation workflow. The official Influenciae package can also be used to reproduce all experiments reported in this repository. Therefore, users may choose either implementation according to their preference.

| Implementation | Recommended use |
|---|---|
| Modified `influenciae_tabular` | Reproducing the original development environment |
| Official Influenciae | Using the official package distribution |

The released notebooks use the prepared CSV datasets included in this repository. The CSV-based workflow simplifies the experimental setup by avoiding additional TensorFlow Datasets dependencies while reproducing the same experimental data used in the paper.

> **Note:** Install only one Influenciae implementation in a given environment to avoid package conflicts.

### Option A: Modified `influenciae_tabular`

Open a Jupyter notebook from the repository and run:

```python
!python -m pip install -e ./third_party/influenciae_tabular
```

Restart the notebook kernel after installation.

### Option B: Official Influenciae

Alternatively, install the official package:

```python
!python -m pip install Influenciae
```

Restart the notebook kernel after installation.

### Dataset loading

All notebooks load the prepared CSV datasets directly. For example:

```python
import pandas as pd

df = pd.read_csv("diamonds.csv")
```

To simplify execution, each notebook expects the required CSV datasets to be located in the same directory as the notebook.




# Reproducing the Paper

The repository is organised according to the figures and tables reported in the paper. Each experiment is contained in an individual folder under `PaperExperiments/`.

Each experiment folder is **self-contained** and includes:

- the Jupyter notebook used for the experiment;
- the required datasets and intermediate files;
- the generated outputs (where applicable); and
- a README describing the experiment and expected results.

This organisation provides two ways to reproduce the paper:

1. **Full reproduction:** Execute the notebook from beginning to end to regenerate all intermediate results and the final figures/tables.
2. **Fast reproduction:** Use the provided intermediate files to reproduce the final figures and tables without rerunning the complete experimental pipeline.

The following table maps each figure and table in the paper to its corresponding experiment folder.






















