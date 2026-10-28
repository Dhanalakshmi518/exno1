# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd

df = pd.read_csv("Data_set.csv")

print("Missing values before cleaning:")
print(df.isnull().sum())

categorical_cols = ["show_name", "aired_on", "original_network"]

for col in categorical_cols:
    df[col] = df[col].fillna("Unknown")

numeric_cols = ["rating", "current_overall_rank", "watchers"]

for col in numeric_cols:
    df[col] = df[col].fillna(df[col].median())

df["current_overall_rank"] = df["current_overall_rank"].round().astype("Int64")

print("\nMissing values after cleaning:")
print(df.isnull().sum())

df.to_csv("Data_set_cleaned.csv", index=False)

print("\nCleaned dataset saved successfully!")
```
<img width="403" height="602" alt="Screenshot 2026-10-28 150516" src="https://github.com/user-attachments/assets/877d07ce-16d0-4443-9c72-7257ba9e8216" />


```
import pandas as pd

df = pd.read_csv("heights.csv")

Q1 = df["height"].quantile(0.25)
Q3 = df["height"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[(df["height"] < lower) | (df["height"] > upper)]

print("Unusual height measurements:")
print(outliers)
```
<img width="318" height="107" alt="Screenshot 2026-10-28 150525" src="https://github.com/user-attachments/assets/1ce9b813-5afd-46f7-ae03-f93b2bef681b" />


```
import pandas as pd

df = pd.read_csv("iris.csv")

cols = df.select_dtypes(include="number").columns

for col in cols:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)
    IQR = Q3 - Q1

    outliers = df[(df[col] < Q1 - 1.5 * IQR) |
                  (df[col] > Q3 + 1.5 * IQR)]

    print("IQR outliers in", col)
    print(outliers[col])

for col in cols:
    z = (df[col] - df[col].mean()) / df[col].std()

    print("Z-score outliers in", col)
    print(df.loc[z.abs() > 3, col])
```
<img width="506" height="501" alt="Screenshot 2026-10-28 150538" src="https://github.com/user-attachments/assets/9988f589-2d87-4b03-88d7-1b6070ca4d9c" />


```
import pandas as pd

df = pd.read_csv("Loan_data.csv")

num_cols = df.select_dtypes(include="number").columns

for col in num_cols:
    df[col] = df[col].fillna(df[col].median())

cat_cols = df.select_dtypes(include="object").columns

for col in cat_cols:
    if df[col].isnull().any():
        df[col] = df[col].fillna(df[col].mode()[0])

df = df.drop_duplicates()

print(df.isnull().sum())

df.to_csv("Loan_data_cleaned.csv", index=False)

print("Data cleaning completed!")
```
<img width="292" height="342" alt="Screenshot 2026-10-28 150601" src="https://github.com/user-attachments/assets/a6f026bb-4dd3-4db4-ac09-4cdd8c59b5af" />


```
import pandas as pd

df = pd.read_csv("SAMPLEIDS.csv")

df = df.drop_duplicates()

print("Missing values:")
print(df.isnull().sum())

print("Duplicate registration numbers:")
print(df[df.duplicated("REGNO", keep=False)])

marks = ["M1", "M2", "M3", "M4"]

print("Inconsistent total marks:")
print(df[df["TOTAL"] != df[marks].sum(axis=1, min_count=4)])

df.to_csv("SAMPLEIDS_cleaned.csv", index=False)

print("Cleaning completed!")
```

<img width="848" height="877" alt="Screenshot 2026-10-28 150839" src="https://github.com/user-attachments/assets/75e8c019-357e-4d9e-9cc1-f16f797192f2" />


            <<include your coding and its corressponding output screen shots here>>

# Summary

I learned how to perform data cleaning using Python and the Pandas library. First, I learned how to read a dataset from a CSV file and identify missing values in each column. I learned to handle missing values by filling numerical data with the median and categorical data with suitable values or the mode. I also learned how to identify and remove duplicate records using the drop_duplicates() function. In addition, I learned to detect outliers using the Interquartile Range (IQR) and Z-score methods. I understood how to check student records for missing values, duplicate registration numbers, and inconsistent total marks. After completing the data cleaning process, I learned to save the cleaned dataset into a new CSV file using the to_csv() function. Finally, this experiment helped me understand the importance of data cleaning in improving data quality and preparing datasets for further analysis.


# Result
          <<include your Result here>>
Thus the given data successfully performed data cleaning and saved the cleaned data to a file.
