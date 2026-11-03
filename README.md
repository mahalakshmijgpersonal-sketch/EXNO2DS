# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT

```
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
data = pd.read_csv("titanic_dataset.csv")
print("\nDataset Loaded Successfully\n")
print(data.head())
print("\nDataset Info:\n")
print(data.info())
print(data.describe())
```
<img width="774" height="672" alt="image" src="https://github.com/user-attachments/assets/d25dd044-0649-41e4-b2c9-d4d7315f84cd" />

```
for column in data.columns:
    if data[column].dtype == 'object':
        data[column] = data[column].fillna(data[column].mode()[0])   # Mode for categorical
    else:
        data[column] = pd.to_numeric(data[column], errors='coerce')
        data[column] = data[column].fillna(data[column].median())   # Median for numerical

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Age"])
plt.title("Boxplot - Age")
plt.show()

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Fare"])
plt.title("Boxplot - Fare")
plt.show()
```
<img width="585" height="410" alt="image" src="https://github.com/user-attachments/assets/fe5cf94a-2b8b-4742-ae16-ac3c481de0fb" />

<img width="558" height="399" alt="image" src="https://github.com/user-attachments/assets/e347a25d-7cc3-4319-878f-a4b6ae5338b5" />

```
# STEP 4 - Outlier Removal using IQR Method

def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

print("Outliers for Age:", remove_outliers_iqr(data, "Age").shape)
print("Outliers for Fare:", remove_outliers_iqr(data, "Fare").shape)

print("Outliers removed using IQR method.\n")
```
<img width="328" height="82" alt="image" src="https://github.com/user-attachments/assets/788384a3-f74f-42f7-a4d7-de7103c750d1" />

```
# STEP 5 - Data Visualization Using Countplots

plt.figure(figsize=(6,4))
sns.countplot(x="Survived", data=data)
plt.title("Countplot - Survival Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="SibSp", data=data)
plt.title("Countplot - Sibling/Spouse Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="Pclass", data=data)
plt.title("Countplot - Passenger Class Distribution")
plt.show()
```
<img width="598" height="390" alt="image" src="https://github.com/user-attachments/assets/8a562595-1ec1-4566-9a68-4d921a18fcb2" />
<img width="570" height="394" alt="image" src="https://github.com/user-attachments/assets/d6cd2213-911f-4e14-9f65-6da9e8207363" />
<img width="608" height="405" alt="image" src="https://github.com/user-attachments/assets/95e36c61-4b67-4304-b098-088950378f36" />
```
# STEP 6 - Data Visualization Using Displots

sns.displot(data["Age"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.show()

sns.displot(data["Fare"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Fare Distribution")
plt.show()
```
<img width="603" height="414" alt="image" src="https://github.com/user-attachments/assets/87bd1812-46e5-45d1-a421-e2fed0f9e2e3" />

<img width="630" height="414" alt="image" src="https://github.com/user-attachments/assets/b1d0af80-d5de-4139-8d88-043f5053cf52" />
```
# STEP 7 - Cross Tabulation

print("\nCross Tabulation: SibSp vs Survived\n")
print(pd.crosstab(data["SibSp"], data["Survived"]))

print("\nCross Tabulation: Pclass vs Survived\n")
print(pd.crosstab(data["Pclass"], data["Survived"]))
```
<img width="384" height="346" alt="image" src="https://github.com/user-attachments/assets/9a226131-05c7-48d5-8772-68f96a07d789" />
```
# STEP 8 - Heatmap of Correlation Analysis

plt.figure(figsize=(8,6))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap - Titanic Dataset")
plt.show()
```
<img width="604" height="512" alt="image" src="https://github.com/user-attachments/assets/a8f5f3fe-8223-44ef-b0d4-5c5f0387000e" />



# RESULT

Thus, the program to perform Exploratory Data Analysis, handle missing values, detect and remove outliers, and visualize the data was successfully executed.
