# SET-12: Student Data Preprocessing and Analysis

This repository contains a Jupyter Notebook that demonstrates core data preprocessing techniques on a student dataset. The project focuses on loading, cleaning, transforming, and preparing the data for further analysis.

## Repository Contents

- `set12_Juhaina.ipynb` – Jupyter Notebook containing the complete preprocessing steps
- `students_set2.csv` – Input dataset (assumed to be present in the working directory)

## Project Objectives

The following preprocessing tasks are performed in the notebook:

1. Load the dataset using pandas
2. Handle missing values by replacing them with the mean of each column
3. Identify and remove duplicate records
4. Normalize numerical columns using Min-Max scaling
5. Discretize the `score` column into three categories using binning
6. Remove noise values from the `score` column using binning-based methods

## Technologies Used

- Python 3.x
- pandas
- numpy
- scikit-learn
- Jupyter Notebook

## Instructions to Run

1. Clone the repository or download the files.

2. (Optional) Create and activate a virtual environment:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate

	3.	Install required packages:

pip install pandas numpy scikit-learn jupyter


	4.	Launch the Jupyter Notebook:

jupyter notebook set12_Juhaina.ipynb


	5.	Run each cell in the notebook to view the preprocessing steps and results.

## Key Code Snippets

Load the dataset:
```
import pandas as pd
df = pd.read_csv('students_set2.csv')
```
Fill missing values with column mean:
```
df.fillna(df.mean(numeric_only=True), inplace=True)
```
Remove duplicate records:
```
df.drop_duplicates(inplace=True)
```
Normalize numerical columns:
```
from sklearn.preprocessing import MinMaxScaler
scaler = MinMaxScaler()
numeric_cols = df.select_dtypes(include='number').columns
df[numeric_cols] = scaler.fit_transform(df[numeric_cols])
```
Discretize scores into 3 bins:
```
df['score_bin'] = pd.cut(df['score'], bins=3, labels=['Low', 'Medium', 'High'])
```
Remove noise using IQR method:
```
Q1 = df['score'].quantile(0.25)
Q3 = df['score'].quantile(0.75)
IQR = Q3 - Q1
df = df[(df['score'] >= Q1 - 1.5 * IQR) & (df['score'] <= Q3 + 1.5 * IQR)]
```
## Author

Prepared by Juhaina
