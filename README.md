# DA7067-Machine-Learning-Exercise---Predicting-Breast-Cancer-Diagnosis
# Breast Cancer Classification Using Machine Learning

## Overview
This Project is base on the Exercise given in the course. I chose Breast Cancer Diagnosis Prediction.

This project investigates whether breast cancer diagnoses can be predicted from numerical cell-nucleus measurements using supervised machine learning. It compares a baseline classifier, logistic regression, and k-nearest neighbours (kNN), and examines how the choice of \(k\) affects model performance.

The project was completed as part of the **DA7067 Computational Mathematics ML exercise** at Stockholm University.

## Research Questions

1. How accurately can a model predict whether a tumour is benign or malignant?
2. How does kNN model complexity, controlled by \(k\), affect prediction performance and generalisation?

## Dataset

The project uses the [Breast Cancer Wisconsin (Diagnostic) dataset](https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic) from the UCI Machine Learning Repository.

- **Samples:** 569
- **Features:** 30 numerical cell-nucleus measurements
- **Target:** Diagnosis — benign (B) or malignant (M)
- **Benign cases:** 357 (approximately 63%)
- **Malignant cases:** 212 (approximately 37%)

The features describe cell-nucleus characteristics such as radius, texture, perimeter, area, smoothness, and concavity. Measurements include mean, standard error, and worst values. The patient ID was excluded from the features.

## Methods

The dataset was divided into 80% training data (455 samples) and 20% test data (114 samples), using stratified sampling and `random_state=42`.

Three classifiers were evaluated:

1. **Baseline:** predicts the most frequent class.
2. **Logistic regression:** a linear classification model.
3. **k-nearest neighbours (kNN):** a distance-based classifier evaluated at \(k=5\) and across values from 1 to 50.

Features were standardised for logistic regression and kNN. The scaler was fitted only on the training data to avoid data leakage.

## Results

| Model | Test accuracy | Test error |
|---|---:|---:|
| Baseline | 63.16% | 36.84% |
| Logistic regression | 96.49% | 3.51% |
| kNN (\(k=5\)) | 95.61% | 4.39% |

Logistic regression performed best on this test split, achieving 96.49% accuracy.

For the malignant class, logistic regression achieved a recall of 0.93, while kNN achieved 0.90. Logistic regression correctly identified 39 of the 42 malignant test cases, compared with 38 for kNN. The baseline failed to identify any malignant cases.

## Bias–Variance Trade-off

The value of \(k\) affected the performance of kNN:

- At \(k=1\), training error was 0%, while test error was approximately 7%, suggesting overfitting.
- The highest observed test error was approximately 8.8% at \(k=2\).
- The minimum test error was approximately 4.4%, achieved at both \(k=5\) and \(k=7\).
- I selected \(k=5\) as a tie-break.

At larger values of \(k\), the model becomes less flexible, and the results suggest possible underfitting. Cross-validation would provide a more reliable method for selecting \(k\).

## Key Takeaways

- Logistic regression slightly outperformed kNN in this experiment.
- Accuracy alone is insufficient; recall is important when identifying malignant cases.
- The choice of \(k\) affects the balance between overfitting and underfitting.
- Model performance should be evaluated on data not used for training or model selection.

## Limitations

The results are based on a single train–test split. Further evaluation using cross-validation and independent data would be needed to assess how reliably the models generalise.

This project is for educational purposes. The models have not been clinically validated and should not be used to diagnose patients or replace professional medical judgement.

## Technologies

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- Jupyter Notebook

## Acknowledgements

Dataset: [UCI Machine Learning Repository — Breast Cancer Wisconsin (Diagnostic)](https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic).

Course: DA7067 Computational Mathematics ML exercise, Stockholm University.
