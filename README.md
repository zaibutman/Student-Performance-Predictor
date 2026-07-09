<div align="center">

# 🎓 Student Performance Predictor

### Predicting math scores from demographic and academic features using Linear Regression

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

</div>

---

## 📌 Overview

This project analyzes the **Students Performance in Exams** dataset to explore how demographic factors (gender, race/ethnicity, parental education, lunch type, test preparation) and academic scores relate to student performance, then builds a **Linear Regression** model to predict **math score**.

The notebook covers exploratory data analysis (gender vs. score, test-prep effect, correlation heatmap), feature engineering, encoding, model training, and evaluation.

> ⚠️ **Note on methodology:** An earlier version of this pipeline engineered an `average score` feature directly from `(math + reading + writing) / 3` and included it as a model input — since `math score` is the prediction target, this caused data leakage (the model could reverse-engineer the exact answer, producing an artificial R² of 1.0). This has been corrected: `average score` and its derived `performance` category are excluded from the feature set, and the model is trained only on genuinely independent features.

## 📊 Dataset

- **Source:** [Students Performance in Exams](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams) (Kaggle)
- **Rows:** 1,000 students
- **Columns:** 8 (5 categorical demographic features + 3 exam scores)

| Feature | Type | Values |
|---|---|---|
| `gender` | Categorical | female, male |
| `race/ethnicity` | Categorical | group A–E |
| `parental level of education` | Categorical | high school → master's degree |
| `lunch` | Categorical | standard, free/reduced |
| `test preparation course` | Categorical | none, completed |
| `math score` | Numeric (target) | 0–100 |
| `reading score` | Numeric | 17–100 |
| `writing score` | Numeric | 10–100 |

**Score distribution:** math (mean 66.1), reading (mean 69.2), writing (mean 68.1) — all with a standard deviation of ~15 points.

## 🧠 Approach

1. **EDA** — visualized score distributions by gender, the effect of test preparation on math score, and correlation between the three exam scores.
2. **Feature engineering** — categorical columns (`gender`, `race/ethnicity`, `parental level of education`, `lunch`, `test preparation course`) encoded with `LabelEncoder`.
3. **Leakage fix** — excluded `average score` and `performance` (both derived from the target) from the feature set.
4. **Modeling** — trained a `LinearRegression` model on an 80/20 train-test split (`random_state=42`) using `reading score`, `writing score`, and the encoded demographic features to predict `math score`.
5. **Evaluation** — assessed with MAE, MSE, RMSE, and R².

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat-square)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square)

## 📈 Results

| Metric | Score |
|---|---|
| **MAE** | 4.13 |
| **MSE** | 28.28 |
| **RMSE** | 5.32 |
| **R² Score** | 0.884 |

On average, predictions land within ~4 points of the true math score, and the model explains **88.4%** of the variance in math scores. The strongest predictors were `gender`, `lunch`, and `test preparation course`, followed by `writing score` and `reading score`.

## 📁 Project Structure

```
student-performance-predictor/
├── Student_performance_prediction.ipynb   # Main notebook (EDA + modeling)
├── StudentsPerformance.csv                # Dataset
├── README.md                              # Project documentation
└── LICENSE
```

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/zaibutman/student-performance-predictor.git
cd student-performance-predictor

# Install dependencies
pip install pandas numpy scikit-learn seaborn matplotlib jupyter

# Launch the notebook
jupyter notebook Student_performance_prediction.ipynb
```

## 🔮 Future Improvements

- Try non-linear models (Random Forest, Gradient Boosting) and compare against the linear baseline
- Add cross-validation instead of a single train-test split
- Engineer non-leaky features (e.g., reading/writing average, without touching the target)
- Predict all three scores (math, reading, writing) as a multi-output problem
- Deploy as a simple web app (Streamlit/Flask) for interactive predictions

## 🏷️ Tags

`machine-learning` `linear-regression` `education-analytics` `scikit-learn` `data-science` `python` `exploratory-data-analysis`

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

⭐ If you found this project useful, consider giving it a star!

</div>
