# 🎓 Instructor Effectiveness Prediction using Machine Learning

<p align="center">

![Python](https://img.shields.io/badge/Python-3.13-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?logo=numpy)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-F7931E?logo=scikitlearn)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green)

</p>

---

## 📖 Project Overview

Educational platforms collect large amounts of learner data, but evaluating instructor performance objectively remains challenging.

This project develops a **Machine Learning framework** to analyze and classify **Instructor Effectiveness** using learner performance, engagement, and feedback metrics.

The project follows an end-to-end **Data Science workflow**, including:

- Data Cleaning
- Exploratory Data Analysis (EDA)
- Feature Engineering
- Feature Scaling
- Instructor-Level Aggregation
- Instructor Effectiveness Scoring
- Machine Learning Classification
- Model Evaluation
- Performance Analysis and Insights

---

## 📚 Table of Contents

- [Problem Statement](#-problem-statement)
- [Dataset](#-dataset)
- [Project Workflow](#-project-workflow)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Feature Engineering](#️-feature-engineering)
- [Machine Learning](#-machine-learning)
- [Model Evaluation](#-model-evaluation)
- [Key Findings](#-key-findings)
- [Limitations](#️-limitations)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Future Improvements](#-future-improvements)
- [Conclusion](#-conclusion)
- [Author](#-author)

---

# 🎯 Problem Statement

The objective of this project is to identify instructor effectiveness levels using learner-related performance and engagement metrics.

The framework aims to:

- Understand learner behaviour and performance.
- Analyze instructor-level teaching outcomes.
- Develop a business-driven instructor effectiveness score.
- Categorize instructors into effectiveness levels.
- Apply Machine Learning models to classify instructor effectiveness.

---

# 📊 Dataset

### Dataset Summary

| Property | Value |
|----------|-------|
| Records | **2,000** |
| Instructors | **120** |
| Courses | **25** |
| Features | **12** |

### Features

- Completion Rate
- Average Score Improvement
- Average Quiz Score
- Dropout Rate
- Average Watch Time
- Assignment Submission Rate
- Forum Activity Rate
- Average Feedback Score
- Feedback Response Rate

---

# 🔄 Project Workflow

The project follows a structured data processing and machine learning pipeline.

```text
Raw Dataset
     |
     ▼
Data Cleaning
     |
     ▼
Exploratory Data Analysis
     |
     ▼
Instructor-Level Aggregation
     |
     ▼
Feature Scaling
     |
     ▼
Feature Engineering
     |
     ▼
Instructor Effectiveness Score
     |
     ▼
Quantile-Based Classification
(Low / Medium / High)
     |
     ▼
Multiple ML Model Evaluation
     |
     ▼
Logistic Regression
     |
     ▼
Final Model Evaluation
```

---

# 📈 Exploratory Data Analysis

The following analyses were performed to understand the dataset and identify patterns:

- Dataset Inspection
- Missing Value Analysis
- Duplicate Check
- Numerical Feature Distributions
- Correlation Analysis
- Outlier Detection
- Feature Relationship Analysis

---

## 📷 Distribution of Numerical Features

![Histogram](images/distribution_hist.png)

---

## 🔥 Correlation Heatmap

![Heatmap](images/heatmap.png)

### Key Insight

- A strong negative correlation was observed between **Completion Rate** and **Dropout Rate (-0.95)**.
- This indicates that higher learner completion rates are associated with lower dropout rates.

---

## 📦 Outlier Analysis

Boxplots were used to identify potential outliers in numerical features.

**Observations:**

- Very few outliers were observed.
- The identified outliers were considered potentially genuine variations in instructor performance rather than data errors.

---

# ⚙️ Feature Engineering

The original dataset contained **batch-level records**, where multiple records were associated with individual instructors.

To enable instructor-level analysis, the dataset was transformed into **instructor-level profiles** using mean aggregation.

This allowed the analysis to focus on overall instructor performance rather than individual batch observations.

---

## Feature Scaling

Numerical features were normalized using:

> **MinMaxScaler**

Scaling was applied to bring numerical variables into a common range before calculating the effectiveness score.

---

## Instructor Effectiveness Score

A weighted scoring framework was developed using three intermediate scores.

### 📘 Learning Score

Based on:

- Completion Rate
- Average Score Improvement
- Average Quiz Score

### 📙 Engagement Score

Based on:

- Average Watch Time
- Assignment Submission Rate
- Forum Activity Rate

### 📗 Feedback Score

Based on:

- Average Feedback Score
- Feedback Response Rate

### Final Effectiveness Score

The final score was calculated using the following weighted formula:

```text
Effectiveness Score =

0.40 × Learning Score

+ 0.30 × Engagement Score

+ 0.20 × Feedback Score

− 0.10 × Dropout Rate
```

The scoring framework assigns the highest weight to learning outcomes, followed by engagement and feedback, while dropout rate contributes negatively.

---

# 🤖 Machine Learning

## Target Variable Generation

Instructor effectiveness was categorized into three classes:

- **Low**
- **Medium**
- **High**

Target labels were generated using:

> **Quantile-Based Binning (qcut)**

This approach divided the effectiveness scores into three approximately balanced categories.

## Model Selection

Multiple classification algorithms were evaluated to identify the most suitable baseline model.

The evaluation process used:

> **5-Fold Stratified Cross-Validation**

Stratified cross-validation maintains approximately the same class distribution across training and validation folds.

### Best Performing Model

**Logistic Regression** achieved the best baseline performance among the evaluated models.

It was selected for final evaluation based on its cross-validation performance.

---

# 📊 Model Evaluation

The final Logistic Regression model was evaluated using a held-out test dataset.

## Cross-Validation Performance

| Metric | Result |
|--------|--------|
| Validation Strategy | 5-Fold Stratified Cross-Validation |
| Mean Cross-Validation Accuracy | **91.67%** |
| Best Baseline Model | **Logistic Regression** |

## Final Test Performance

<details>
<summary><b>Model Performance Summary</b></summary>

| Metric | Result |
|--------|--------|
| Model | Logistic Regression |
| Test Accuracy | **87.50%** |
| Macro F1-Score | **0.88** |
| Total Test Samples | 24 |
| Correct Predictions | 21 |
| Incorrect Predictions | 3 |

</details>

### 🎯 Test Accuracy

**87.50%**

The model correctly classified 21 out of 24 test samples.

---

## Confusion Matrix

The confusion matrix illustrates the classification performance across Low, Medium, and High instructor effectiveness categories.

![Confusion Matrix](images/confusion_matrix.png)

### Classification Observations

- The model correctly classified **21 out of 24 test samples**.
- Three test samples were misclassified.
- Most classification errors occurred between neighboring effectiveness categories.
- The model demonstrated good classification performance on the held-out test set.

---

# 💡 Key Findings

The analysis produced the following findings:

1. **Instructor-Level Analysis:** Transforming batch-level records into instructor-level profiles enabled a more meaningful evaluation of instructor performance.

2. **Weighted Effectiveness Framework:** Learning outcomes, engagement, feedback, and dropout rate were combined into a single effectiveness score.

3. **Balanced Classification:** Quantile-based classification was used to categorize instructors into Low, Medium, and High effectiveness levels.

4. **Model Performance:** Logistic Regression achieved the best baseline performance, with a mean cross-validation accuracy of **91.67%**.

5. **Final Evaluation:** The selected model achieved **87.50% test accuracy** and a **macro F1-score of 0.88**.

6. **Classification Errors:** Most errors occurred between neighboring effectiveness categories, suggesting that some instructors had relatively similar effectiveness scores.

---

# ⚠️ Limitations

An important limitation of this project is related to the generation of the target variable.

- Instructor effectiveness labels were generated using a weighted scoring methodology rather than independently collected real-world labels.
- The scoring framework used learner performance, engagement, feedback, and dropout features.
- These same underlying features were also used as inputs to the machine learning models.
- Consequently, the model learns to reproduce the engineered effectiveness classification rather than independently measure real-world instructor effectiveness.
- The feature weights were based on domain assumptions and may require validation.

Therefore, the reported model performance should be interpreted as its ability to classify instructors according to the proposed scoring framework.

It should not be considered independent proof of actual teaching effectiveness.

---

# 📁 Project Structure

```text
Instructor-Effectiveness-Prediction/
│
├── data/
│   └── instructor_data.csv
│
├── notebooks/
│   └── Instructor_Effectiveness_Analysis.ipynb
│
├── images/
│   ├── distribution_hist.png
│   ├── heatmap.png
│   ├── confusion_matrix.png
│   └── feature_imp.png
│
├── README.md
├── requirements.txt
├── LICENSE
└── .gitignore
```

---

# 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yashawari31/instructor-effectiveness-prediction.git
```

### 2. Navigate to the Project Directory

```bash
cd instructor-effectiveness-prediction
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open the notebook inside the `notebooks` directory to explore the complete analysis and implementation.

---

# 📦 Requirements

The project uses the following Python libraries:

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
jupyter
```

---

# 🔮 Future Improvements

- Collect independent real-world instructor effectiveness labels through expert evaluations, learner surveys, and subsequent learner outcomes.
- Incorporate additional factors such as course difficulty, instructor experience, and learner demographics.
- Experiment with advanced classification algorithms such as Gradient Boosting and XGBoost.
- Increase the dataset size to improve the reliability and generalizability of the analysis.
- Validate the weighted effectiveness scoring framework against independently observed instructor performance.
- Explore model interpretability techniques to better understand the factors influencing predictions.

---

# 🏆 Conclusion

This project developed an end-to-end data science framework for analyzing and classifying instructor effectiveness using learner performance, engagement, and feedback metrics.

The framework transformed batch-level records into instructor-level profiles and introduced a weighted effectiveness scoring methodology to categorize instructors into Low, Medium, and High effectiveness levels.

Multiple machine learning models were evaluated using 5-fold stratified cross-validation. Logistic Regression achieved the best baseline performance with a mean cross-validation accuracy of **91.67%**.

The final model achieved **87.50% accuracy** and a **macro F1-score of 0.88** on the held-out test set, correctly classifying 21 out of 24 samples.

While the results demonstrate the ability of machine learning to reproduce the proposed effectiveness classification framework, independent real-world validation is necessary before applying it as an objective measure of instructor performance.

---

# 👨‍💻 Author

## **Yash Awari**

📧 Email: mr.yash3110@gmail.com

🔗 LinkedIn: https://www.linkedin.com/in/yash-awari-a33823329/

💻 GitHub: https://github.com/yashawari31

---

## ⭐ If you found this project useful, consider giving it a star!
