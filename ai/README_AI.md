# Assignment 5b — AI-Assisted Machine Learning in R

This folder contains an AI-assisted machine learning workflow for the Iris classification task. It complements the manual tutorial in `manual/ml_r.ipynb` with a focused pipeline: load data, split train/validation, train classifiers, evaluate, and select the best model.

## Dataset

- **Source:** `manual/iris.csv` (150 observations, 4 features, 3 species)
- **Features:** Sepal.Length, Sepal.Width, Petal.Length, Petal.Width
- **Target:** Species (Iris-setosa, Iris-versicolor, Iris-virginica)

The notebook reads the CSV via a relative path (`../manual/iris.csv`) so the data stays in the manual folder.

## Environment

Reproduce the conda environment with:

```bash
cd assignment5b
conda env create -f ai/environment.yml
conda activate ml-r
```

If the environment already exists, update it with:

```bash
conda env update -f ai/environment.yml --prune
```

### Packages

| Package | Purpose |
|---------|---------|
| r-base, r-irkernel | R runtime and Jupyter kernel |
| jupyter, jupyter_client | Notebook interface |
| r-caret | Data partitioning, model training, evaluation |
| r-kernlab | SVM (svmRadial) support for caret |
| r-randomforest | Random Forest support for caret |
| r-ggplot2, r-lattice | Plotting (used by caret visualizations) |
| r-tidyverse | General data utilities |

## How to Run

```bash
conda activate ml-r
cd assignment5b
jupyter lab
```

Open `ai/notebook.ipynb` and run all cells with the **R** kernel.

## Methods

1. **Load** `manual/iris.csv` and set column names.
2. **Split** 80% training / 20% validation using stratified sampling (`createDataPartition`, `set.seed(7)`).
3. **Train** five classifiers on the training set with 10-fold cross-validation:
   - Linear Discriminant Analysis (LDA)
   - Classification and Regression Trees (CART / rpart)
   - k-Nearest Neighbors (kNN)
   - Support Vector Machine with radial kernel (SVM)
   - Random Forest (RF)
4. **Compare** models by mean cross-validation accuracy.
5. **Select** the model with the highest mean CV accuracy.
6. **Evaluate** the chosen model on the held-out validation set using a confusion matrix.

## Results

| Model | Mean CV Accuracy |
|-------|------------------|
| **LDA** | **0.975** |
| kNN | 0.967 |
| Random Forest | 0.950 |
| SVM | 0.933 |
| CART | 0.917 |

**Best model:** LDA (Linear Discriminant Analysis)

**Holdout validation accuracy:** 100% (30/30 correct on the 20% validation set)

LDA achieved the highest cross-validation accuracy and generalized perfectly to the held-out data. For this well-separated dataset, a simple linear classifier matches or outperforms more complex models. All models exceed 91% mean CV accuracy, which is expected for Iris.

## Verification

Tested on 2 August 2026:

- **End-to-end:** `notebook.ipynb` executes with zero errors in both the existing `ml-r` environment and a fresh env created from `environment.yml`.
- **Reproducibility:** `conda env create -f ai/environment.yml -n ml-r` installs all packages needed for every classifier (including SVM and Random Forest).
- **Performance:** Results are stable across runs (`set.seed(7)`); LDA mean CV accuracy = 0.975, holdout accuracy = 1.0.

## File Layout

```
assignment5b/ai/
├── environment.yml   # Reproducible conda environment (ml-r)
├── notebook.ipynb    # R notebook with full ML pipeline
├── README_AI.md      # This file
└── PROMPTS.md        # Prompts used to generate this work
```

## References

- Jason Brownlee, [Your First Machine Learning Project in R Step-By-Step](https://machinelearningmastery.com/machine-learning-in-r-step-by-step/)
- Manual tutorial notebook: `manual/ml_r.ipynb`

## License

Created for BSGP 7030 (Assignment 5b).
