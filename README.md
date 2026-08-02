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
- [Installation](#installation)
- [Reproducing the Paper](#reproducing-the-paper)
- [Repository Structure](#repository-structure)








































