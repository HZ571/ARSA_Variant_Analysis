# ARSA Variant Analysis

Machine-learning analysis of ARSA genetic variants using Python and scikit-learn.

## Overview

This project develops a machine-learning pipeline to classify genetic variants as pathogenic or benign and applies the resulting model to predict stability-related scores for ARSA variants.

The analysis was developed as part of a computational biology project and uses publicly available variant-prediction features alongside supervised machine-learning methods.

## Dataset

The primary training dataset contains **13,464 labeled genetic variants** with annotation and pathogenicity-prediction features.

The analysis uses features derived from multiple computational prediction tools, including:

* AlphaMissense
* CADD
* DANN
* Eigen
* FATHMM
* GERP++
* PROVEAN
* PolyPhen-2
* SIFT

An additional engineered feature identifies multi-nucleotide variants (MNVs).

Raw datasets are not included in this repository.

## Approach

The analysis pipeline consists of:

1. Loading and cleaning variant data
2. Handling multi-transcript feature values
3. Converting prediction scores to numeric values
4. Normalizing score direction where necessary
5. Engineering an MNV indicator
6. Median imputation of missing values
7. Feature scaling
8. Training and comparing multiple classification models
9. Evaluating model performance using cross-validation and a held-out self-test set
10. Generating predictions for the ARSA variant submission dataset

Two models were evaluated:

* Random Forest
* k-Nearest Neighbors (k-NN)

Both models were evaluated using **5-fold cross-validation with ROC-AUC** as the primary metric.

## Results

The Random Forest model achieved a mean 5-fold cross-validation ROC-AUC of:

**0.940**

The k-NN model achieved:

**0.912**

The Random Forest was therefore selected for the final prediction pipeline.

On a held-out self-test set, the Random Forest achieved a ROC-AUC of approximately **0.926**.

Feature-importance analysis indicated that AlphaMissense, CADD, and GERP++ were among the most influential predictors.

The final model was used to generate predictions for **2,491 ARSA variants**.

## Repository Structure

```text
ARSA_Variant_Analysis/
├── Documents/
├── Notebooks/
│   └── ARSA_analysis.ipynb
├── Results/
│   └── Figures/
├── src/
│   └── arsa_analysis.py
├── .gitignore
├── README.md
└── requirements.txt
```

## Technologies

* Python
* pandas
* NumPy
* scikit-learn
* Jupyter
* Matplotlib
* Seaborn

## Reproducibility

Install the required Python packages with:

```bash
pip install -r requirements.txt
```

The raw datasets are intentionally excluded from the repository. The analysis notebook expects the required input files to be available locally in the `Data/` directory.

## Limitations

The final stability-related prediction is derived from the model's pathogenicity prediction rather than being trained directly on an experimentally measured protein-stability phenotype.

Pathogenicity and structural stability are related but distinct biological concepts, and variants may affect protein function through mechanisms that are not captured by the available features.

Future work could incorporate stability-specific experimental data and additional features designed specifically to model protein stability.

## AI-Assisted Development

Generative AI was used during development to assist with portions of the Python implementation, debugging, and project development. Generated code was reviewed, tested, and modified as needed during development.

The final analysis, model selection, evaluation, interpretation, and submitted results were reviewed by the author.
