## Ecommerce Purchases Analysis
## 💻 Code Snippet


```python
import pandas as pd
```
# Read the dataset
```python
data = pd.read_csv(r"C:\Users\guddu\Downloads\EXCEL\archive\Ecommerce Purchases")

# Display the full DataFrame (optional)
print(data)
```
# Basic Overview
```python
print('\nTop 3 Rows:\n', data.head(3))
print('\nColumn Names:\n', data.columns)
print('\nData Types:\n', data.dtypes)
print('\nMissing Values:\n', data.isnull().sum())
print('\nShape (Rows, Columns):\n', data.shape)
```
# Purchase Price Analysis
```python
print('\nMax Purchase Price:\n', data['Purchase Price'].max())
print('\nTop 5 Highest Purchase Prices:\n', data.nlargest(5, 'Purchase Price'))
print('\nAverage Purchase Price:\n', round(data['Purchase Price'].mean(), 2))
```
# Language Filter
```python
print('\nFrench Language Users:\n', data[data['Language'] == 'fr'])
print('\nNumber of French Users (Method 1):\n', len(data[data['Language'] == 'fr']))
print('\nNumber of French Users (Method 2):\n', data[data['Language'] == 'fr'].count())
```

# Job Title Filter
```python
print('\nJob Titles Ending with "Engineer":\n', data[data['Job'].str.lower().str.endswith('engineer')])
print('\nJob Titles Containing "Engineer":\n', len(data[data['Job'].str.contains('engineer', case=False)]))
```
# Email of specific IP
```python
print('\nEmail of user with IP 132.207.160.22:\n', data[data['IP Address'] == "132.207.160.22"]['Email'])
```
# Mastercard and Purchase > 50
```python
master_above_50 = data[(data['CC Provider'] == 'Mastercard') & (data['Purchase Price'] > 50)]
print('\nMastercard users with purchase > 50:\n', master_above_50)
print('\nTotal such users:\n', len(master_above_50))
```
# Email of specific Credit Card number
```python
print('\nEmail with Credit Card 4664825258997302:\n', data[data['Credit Card'] == 4664825258997302]['Email'])
```
# Count cards expiring in 2020 (Method 1)
```python
print('\nCredit Cards Expiring in 2020:\n', len(data[data['CC Exp Date'].str.endswith('20')]))

# Method 2: using loop

def count_expired_in_2020():
    count = 0
    for i in data['CC Exp Date']:
        if i.split('/')[1].strip() == '20':
            count += 1
    print('\n[Loop Method] Cards expiring in 2020:', count)

count_expired_in_2020()

# Method 3: using slicing

print('\n[Slicing Method] Cards expiring in 2020:', len(data[data['CC Exp Date'].apply(lambda x: x[3:] == '20')]))
```
# AM or PM purchase count
```python
print('\nAM/PM Purchase Count:\n', data['AM or PM'].value_counts())
```
# Top 5 Most Common Email Domains
```python
# Method 1
data['Email Domain'] = data['Email'].str.split('@').str[1]
print('\nTop 5 Email Domains:\n', data['Email Domain'].value_counts().head())

# Method 2
def top_email_domain():
    domains = data['Email'].str.split('@').str[1]
    top = domains.value_counts().head()
    print('\n[Function] Top 5 Email Domains:\n', top)

top_email_domain()

# Method 3: using lambda
print('\n[Lambda Method] Top 5 Email Domains:\n', data['Email'].apply(lambda x: x.split('@')[1]).value_counts().head())
```
