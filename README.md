# 📊 Student Performance Analysis (EDA Project)

# Import Libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns# 📊 Student Performance Analysis (EDA Project)

## 🚀 Project Overview
This project focuses on analyzing student performance data using Python. The goal is to identify patterns and factors affecting student scores.

## 🛠️ Tools & Technologies
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn

## 🔍 Steps Performed
- Data loading and cleaning
- Handling missing values and duplicates
- Feature engineering (Average Score)
- Exploratory Data Analysis (EDA)
- Data visualization
- Correlation analysis

## 📈 Key Insights
- Students who completed the test preparation course scored higher
- Reading and Writing scores are highly correlated
- Lunch type and parental education impact performance

## 📂 Files Included
- `Developer_Assessment.ipynb` → Main analysis notebook
- Dataset (StudentsPerformance.csv)

## 🎯 Conclusion
This project helped in understanding real-world data analysis workflow and improving skills in Python and data visualization.

## 📬 Contact
Feel free to connect with me on LinkedIn!

# Load Dataset
df = pd.read_csv("StudentsPerformance.csv")

# -----------------------------
# Data Understanding
# -----------------------------
print("First 5 Rows:\n", df.head())
print("\nDataset Info:\n")
df.info()

print("\nMissing Values:\n", df.isnull().sum())
print("\nDuplicate Values:", df.duplicated().sum())

# -----------------------------
# Feature Engineering
# -----------------------------
df['average_score'] = (
    df['math score'] + df['reading score'] + df['writing score']
) / 3

print("\nUpdated Data:\n", df.head())

# -----------------------------
# Exploratory Data Analysis
# -----------------------------

# Distribution of Average Score
plt.figure()
sns.histplot(df['average_score'], kde=True)
plt.title("Distribution of Average Score")
plt.show()

# Boxplot for Scores
plt.figure()
sns.boxplot(data=df[['math score', 'reading score', 'writing score']])
plt.title("Score Distribution")
plt.show()

# Gender vs Average Score
plt.figure()
sns.barplot(x='gender', y='average_score', data=df)
plt.title("Average Score by Gender")
plt.show()

# Test Preparation Impact
plt.figure()
sns.barplot(x='test preparation course', y='average_score', data=df)
plt.title("Impact of Test Preparation Course")
plt.show()

# Lunch Impact
plt.figure()
sns.barplot(x='lunch', y='average_score', data=df)
plt.title("Impact of Lunch Type")
plt.show()

# -----------------------------
# Group Analysis
# -----------------------------
print("\nAverage Score by Gender:\n", df.groupby('gender')['average_score'].mean())

print("\nTest Preparation Count:\n",
      df.groupby('gender')['test preparation course'].value_counts())

print("\nLunch Count:\n",
      df.groupby('gender')['lunch'].value_counts())

# -----------------------------
# Correlation Analysis
# -----------------------------
corr = df[['math score', 'reading score', 'writing score']].corr()
print("\nCorrelation Matrix:\n", corr)

# Heatmap
plt.figure()
sns.heatmap(corr, annot=True)
plt.title("Correlation Heatmap")
plt.show()

# -----------------------------
# Conclusion
# -----------------------------
print("\nKey Insights:")
print("- Students who completed test preparation scored higher")
print("- Reading and writing scores are highly correlated")
print("- Lunch type impacts performance")
