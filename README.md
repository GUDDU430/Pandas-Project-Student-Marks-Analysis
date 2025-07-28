# Pandas-Project-Student-Marks-Analysis

```python
import pandas as pd

# Creating DataFrame
data = {
    'Name': ['Priyanka', 'Aadhya', 'Krisha', 'Vedant', 'Parshv', 'Mittal', 'Archana'],
    'Marks': [98, 89, 99, 87, 90, 83, 99],
    'Gender': ['Male', 'Female', 'Female', 'Male', 'Male', 'Female', 'Female']
}
df = pd.DataFrame(data)
```
# Display the complete DataFrame
print("Complete DataFrame:\n", df)

# Q1: Top 3 rows
print("\nTop 3 rows:\n", df.head(3))

# Q2: Last 3 rows
print("\nLast 3 rows:\n", df.tail(3))

# Q3: Shape of the DataFrame
print("\nShape (rows, columns):", df.shape)
print("Number of Rows:", df.shape[0])
print("Number of Columns:", df.shape[1])

# Q4: Info about DataFrame
print("\nDataFrame Info:",)
df.info()

# Q5: Null value check
print("\nNull values column-wise:\n", df.isnull().sum())
print("Null values row-wise:\n", df.isnull().sum(axis=1))

# Q6: Summary statistics
print("\nSummary statistics (numeric only):\n", df.describe())
print("\nSummary statistics (all columns):\n", df.describe(include='all'))

# Q7: Unique values in 'Gender'
print("\nUnique values in Gender:", df['Gender'].unique())

# Q8: Number of unique values in 'Gender'
print("Number of unique genders:", df['Gender'].nunique())

# Q9: Count of each unique gender
print("Gender count:\n", df['Gender'].value_counts())

# Q10: Students with marks between 90 and 100
filtered_df = df[df['Marks'].between(90, 100)]
print("\nStudents scoring between 90 and 100:\n", filtered_df)
print("Total students in that range:", len(filtered_df))

# Alternate way
print("Total (using sum):", sum(df['Marks'].between(90, 100)))

# Q11: Average marks
print("\nAverage Marks:", round(df['Marks'].mean(), 2))

# Apply function: Add Half Marks column
df['Half Marks'] = df['Marks'].apply(lambda x: x / 2)
print("\nDataFrame with Half Marks:\n", df)

# Name length using apply
print("\nLength of each Name:\n", df['Name'].apply(len))

# Map function: Gender to binary
df['Male_Female'] = df['Gender'].map({'Male': 1, 'Female': 0})
print("\nDataFrame with Male_Female column:\n", df)

# Drop column (create new df)
df2 = df.drop('Male_Female', axis=1)
print("\nDrop 'Male_Female' column (df2):\n", df2)
print("Original DataFrame remains unchanged:\n", df)

# Drop multiple columns (new df)
df3 = df.drop(['Male_Female', 'Half Marks'], axis=1)
print("\nDrop 'Male_Female' and 'Half Marks' columns (df3):\n", df3)

# Drop columns in original DataFrame
df.drop(['Male_Female', 'Half Marks'], axis=1, inplace=True)
print("\nOriginal DataFrame after dropping columns:\n", df)

# Display column names and index
print("\nColumn names:", df.columns.tolist())
print("Index:\n", df.index)

# Sort by Marks (descending)
print("\nSorted by Marks (descending):\n", df.sort_values('Marks', ascending=False))

# Display Name & Marks of Female students
female_students = df[df['Gender'] == 'Female'][['Name', 'Marks']]
print("\nFemale students (Name & Marks):\n", female_students)

# Alternative using isin
print("\nFemale students using isin:\n", df[df['Gender'].isin(['Female'])][['Name', 'Marks']])
