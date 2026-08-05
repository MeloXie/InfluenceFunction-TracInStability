# Downstream Evaluation (Extended Settings)

This supplementary experiment extends the downstream noisy-label detection and pruning evaluation presented in the main paper by including three additional experimental settings.

## Folder Contents

```text
Downstream_Extend/
│
├── Flip20-Features52/
├── Flip20-Sparse2Dense005-HalfDenseSparseInBothLabel/
├── Flip20-Sparse3Dense001-HalfDenseSparseInBothLabel/
│
└── README.md
```

---

## Reproducing the Experiment

This experiment follows **exactly the same workflow** as the downstream evaluation described in

```
PaperExperiments/Table6_Downstream/README.md
```

Each subfolder contains one additional experimental setting. The notebooks and execution procedure are identical to those used in the main-paper downstream experiments.

Simply open the corresponding experiment folder and follow the instructions provided in the main-paper README.

---

## Additional Experimental Settings

This supplementary folder includes three additional settings:

- **52-feature synthetic dataset**
- **Density contrast:** (2.0, 0.05)
- **Density contrast:** (3.0, 0.01)

All other experimental procedures remain unchanged.

---

## Notes

- For experimental settings that are **not included** in this supplementary folder, please refer to the corresponding folders under

```
PaperExperiments/Table6_Downstream/
```

- The execution order, generated intermediate files, and evaluation procedure are identical to those described in the main-paper downstream experiment.
