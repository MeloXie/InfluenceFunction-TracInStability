# Code for 'Data-Side Robustness of Training-Data Influence Estimation'

The complete supplementary material accompanying the paper is available here:

**➡️ [SupplementaryPaper.pdf](SupplementaryPaper.pdf)**

## Quick Navigation

- [Repository Structure](#repository-structure)
- [Requirements and Installation](#requirements-and-installation)
- [Environment Setup](#environment-setup)
- [Reproducing the Paper](#reproducing-the-paper)
- [Repository Overview](#repository-overview)
- [Citation](#citation)


# Repository Structure

The repository is organized into reusable experiment modules together with the complete paper reproduction workflow.

```text
InfluenceFunction-TracInStability/
│
├── ClassImbalance/
├── Dataset/
├── NumOfFeatures/
├── NumOfSamples/
├── PaperExperiments/
├── SparsityAndDensity/
├── SupplementaryExperiments/
├── third_party/
│
├── 00_Install_Requirements.ipynb
├── README.md
├── SimpleOverallFrameWork.ipynb
├── SupplementaryMaterial_ver1.0.pdf
└── requirements.txt
```

## Top-Level Directories

| Directory | Description |
|-----------|-------------|
| `ClassImbalance/` | Contains the notebooks used to compute FOIF and TracIn influence scores under different class-imbalance ratios. These notebooks are reused by several experiments in the paper. |
| `Dataset/` | Contains the prepared datasets (`train.csv` and `diamonds.csv`) together with a notebook explaining how the datasets are loaded and prepared for the experiments. |
| `NumOfFeatures/` | Contains the notebook used to compute FOIF and TracIn influence scores under different feature dimensionalities. |
| `NumOfSamples/` | Contains the notebook used to compute FOIF and TracIn influence scores under different training dataset sizes. |
| `PaperExperiments/` | Contains the complete reproduction workflow for every figure, table, and additional analysis reported in the paper. Each experiment is self-contained and includes its own `README.md` with detailed reproduction instructions. |
| `SparsityAndDensity/` | Contains the notebook used to compute FOIF and TracIn influence scores under different sparsity and local-density settings. |
| `SupplementaryExperiments/` | Contains the experiments corresponding to the supplementary material. This section will be expanded as the supplementary experiments are released. |
| `third_party/` | Contains the modified `influenciae_tabular` implementation used during development. Users may alternatively install the official Influenciae package as described in the installation guide. |

---

## Root Files

| File | Description |
|------|-------------|
| `00_Install_Requirements.ipynb` | A one-click Jupyter notebook for installing the required Python packages directly from `requirements.txt`. |
| `README.md` | The main documentation for the repository, including installation instructions, repository organization, and paper reproduction guidance. |
| `SimpleOverallFrameWork.ipynb` | A simplified end-to-end example demonstrating the general workflow for computing FOIF and TracIn influence scores, together with explanatory comments describing the implementation pipeline. |
| `SupplementaryMaterial_ver1.0.pdf` | The supplementary material accompanying the paper, containing additional experimental results and analyses. |
| `requirements.txt` | Lists the Python packages required to execute the notebooks in this repository. |



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




# Environment Setup

The repository was developed and tested using the environment below. All experiments reported in the paper can be reproduced using this configuration.

| Component | Version |
|-----------|---------|
| Python | 3.10.8 |
| Jupyter Notebook | 7.3.2 |
| CUDA | Not required |
| GPU | Optional (all reported results in the paper were generated on CPU) |

The implementation is **fully notebook-based**. After installing the required dependencies, users can reproduce each experiment by opening the corresponding Jupyter notebook and executing all cells sequentially.
> **Development Environment:** All experiments in this repository were developed and validated on **Windows 11** using Jupyter Notebook.



# Reproducing the Paper

This repository is organized around the experiments reported in the paper. Each figure, table, and additional analysis is placed in an individual directory under `PaperExperiments/`.

Every experiment directory contains:

- the Jupyter notebooks required to reproduce the experiment;
- the intermediate files generated during development (where appropriate);
- all datasets required for execution; and
- a dedicated `README.md` describing the reproduction workflow, required parameter changes, expected outputs, and notes.

Most experiments can therefore be reproduced independently without interacting with the remaining folders.

> **Recommendation**
>
> Several experiments involve computationally expensive influence estimation (particularly those using the full Diamonds dataset or multiple repeated runs). Intermediate files generated during development are included whenever possible. Users interested in reproducing only the reported figures or tables are encouraged to use these provided files to avoid unnecessary recomputation.

---

## PaperExperiments Structure

```text
PaperExperiments/
│
├── Figure1_CaseStudy_Stability/
├── Figure2_CaseStudy_Consistency/
├── Figure3_Feature_Heatmap/
├── Figure4_Influence_VS_Loss/
├── Figure5_Distance_Influence/
├── Figure6_Rank_Position/
├── Figure7_Lift_Plot/
│
├── Table2_Chunk_Entropy/
├── Table3_Influence_Loss_Stats/
├── Table4_1_9_Lift/
├── Table5_Consistency/
├── Table6_Downstream/
│
└── Multi_Regression_Slope/
```

---

## Experiments Included

| Paper Result | Folder | Description |
|--------------|--------|-------------|
| Figure 1 | `Figure1_CaseStudy_Stability` | Stability of influence rankings under different age-imputation strategies on Titanic. |
| Figure 2 | `Figure2_CaseStudy_Consistency` | Rank consistency between FOIF and TracIn. |
| Figure 3 | `Figure3_Feature_Heatmap` | Stability under increasing feature dimensionality. |
| Figure 4 | `Figure4_Influence_VS_Loss` | Relationship between training loss and influence scores. |
| Figure 5 | `Figure5_Distance_Influence` | Influence-score differences across distance bands. |
| Figure 6 | `Figure6_Rank_Position` | Rank-position distributions under different density settings. |
| Figure 7 | `Figure7_Lift_Plot` | Minority-lift evaluation under varying class imbalance ratios. |
| Table 2 | `Table2_Chunk_Entropy` | Chunk-contribution entropy across different dataset partitions. |
| Table 3 | `Table3_Influence_Loss_Stats` | Correlation between training loss and influence statistics. |
| Table 4 | `Table4_1_9_Lift` | Sign-aware minority lift under 1:9 class imbalance. |
| Table 5 | `Table5_Consistency` | Consistency between FOIF and TracIn under different data properties. |
| Table 6 | `Table6_Downstream` | Noisy-label detection and downstream pruning evaluation. |
| Additional Analysis | `Multi_Regression_Slope` | Multiple linear regression analysis supporting the discussions on class imbalance and density effects. |

---

## General Reproduction Workflow

Although each experiment differs, most follow the same overall workflow:

1. **Generate influence scores**
   - Execute the corresponding influence-estimation notebook.

2. **Generate intermediate files**
   - Influence scores, losses, labels, or other experiment-specific outputs are produced.

3. **Run the analysis notebook**
   - The generated files are summarized to reproduce the reported figure, table, or statistical analysis.

Detailed instructions for each experiment are provided in the corresponding `README.md` within each folder.

---

## Computational Cost

Some experiments require substantially longer execution times than others.

| Computational Cost | Examples |
|--------------------|----------|
| **Low** | Figure 1, Figure 2 |
| **Medium** | Figure 4, Figure 5, Figure 6 |
| **High** | Figure 3 (5 repeated runs), Table 2 (5 large repeated runs), Table 6 (multiple retraining experiments) |
| **Very High** | Any experiment involving the full Diamonds dataset (approximately 54,000 training samples). |

For all computationally intensive experiments, intermediate files are provided whenever possible so that users may skip the influence-estimation stage and directly reproduce the reported results.

---

## Additional Notes

- Every experiment is completely self-contained.
- Each folder contains all notebooks and files required for reproduction.
- All experiments are notebook-based and can be executed sequentially by running the notebook cells.
- Unless otherwise stated in the experiment-specific README, the provided datasets should be placed in the same directory as the corresponding notebook.
- Experiment-specific parameter changes, filename updates, and expected outputs are documented in the individual `README.md` files.

## Supplementary Experiments

In addition to the experiments presented in the main paper, this repository also contains the complete implementation of all supplementary experiments described in the accompanying supplementary material.

The supplementary experiments are organised under:

```text
SupplementaryExperiments/
```

Each experiment has its own dedicated folder containing:

- a standalone `README.md` with detailed reproduction instructions,
- the corresponding Jupyter notebooks,
- any required intermediate files (where provided), and
- descriptions of the expected outputs.

The supplementary experiments include:

- Aggregation strategy comparison
- Additional class-imbalance lift evaluation (2:8 and 3:7)
- TracIn checkpoint effectiveness
- Diamonds chunk-entropy analysis
- Extended class-imbalance loss-decile analysis
- Conditional Spearman correlation analysis
- Distance-influence analysis on Diamonds
- Extended downstream evaluation
- Influence-versus-loss analysis on Adult
- Loss-decile analysis
- MMD sanity check
- Extended regression-slope analysis (class imbalance and density)
- Runtime evaluation
- Zero-padding feature heatmap

The overall reproduction workflow follows the same design as the main-paper experiments. Where experiments require extensive influence estimation (e.g., multiple independent runs or large real-world datasets), intermediate results are provided to enable fast and convenient reproduction.



# Repository Overview

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



# Citation

### GitHub Repository

```bibtex
@misc{OurRepo,
  author       = {Tianyang Xie and Paolo Missier and Huiping Chen},
  title        = {InfluenceFunction-TracInStability: Supplementary Material and Source Code},
  year         = {2026},
  howpublished = {\url{https://github.com/MeloXie/InfluenceFunction-TracInStability}},
  note         = {GitHub repository}
}
```












