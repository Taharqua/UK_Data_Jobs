# UK Data Jobs

## Data Analytics

![image](https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/30689b8c-6de3-4a5a-8e4c-3a2000e3eebd)

This is a look at the UK Data Job market an some of the influences around salary using Python and libraries within Python.

As someone who is looking to formally enter the Data Market, despite having experience working with Data throughout my career.

I was able to use a lot of my knowledge with libraries such as Pandas, NumPy, and more; whilst, showing my understanding of distributions, statistical method, and their applications.

### Daatset

The dataset contains Data job information in the UK in 2021. 
Here is a link to the original dataset: https://www.kaggle.com/datasets/devario/uk-data-science-jobs-dataset

### Cleaning and Transforming Data

I used a multitude of different methods to clean and transform the dataset.

Here are some examples:

```python
# Ensuring all cities and locations are in the same letter case.
df['location'] = df['location'].str.lower()
df['city'] = df['city'].str.lower()

# Making sure any place within London, changes their city to London and Location to South East England.
df['city'] = np.where((df['location'] == 'london'), "london", df['city'])
df['city'] = np.where((df['city'] == 'uxbridge'), "london", df['city'])
df['location'] = np.where((df['location'] == 'london') & (df['city'] == 'london'),
                          "south east england", df['location'])

# Capitalising all locations
df['location'] = df['location'].str.title()
df['city'] = df['city'].str.title()
```

```python
# Creating a new column.
df['job_category'] = ''

# Ensuring all titles are the same letter case.
df['title'] = df['title'].str.lower()

# Giving jobs the appropriate job category.
df['job_category'] = np.where((df['title'].str.contains('sql')), "data", df['job_category'])
df['job_category'] = np.where((df['title'].str.contains('dba')), "data", df['job_category'])
df['job_category'] = np.where((df['title'].str.contains("data")), "data", df['job_category'])
df['job_category'] = np.where((df['title'].str.contains("recruitment")), "recruitment", df['job_category'])
df['job_category'] = np.where((df['title'].str.contains("recruiter")), "recruitment", df['job_category'])

# Grouping all entries that are not considered "data"
df1 = df[~(df['job_category'] == "data")].index

# Removing all jobs which are not in the "data" job category.
df.drop(df1, inplace=True)

# Ensuring all entries are of the "data" job category.
pd.crosstab(index=df['job_category'], columns='count')
```

```python
# Removing all unnecessary columns.
df.drop(['reference','salary_currency','date_posted', 'date_ending','country','salary_frequency', 'salary_min', 'salary_max'], axis=1, inplace=True)
```

### Data Visualisations 

Here are some of the visualations that I have been using during the process.

![image](https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/528acef5-b464-442b-ba9b-901766fbacd4)
![image](https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/a7a92c4a-9cc6-4a45-a73b-2d19a1d9c98a)
![image](https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/c682730b-803e-45ed-aca1-6fb9be98feda)


### Distribution and Correlation Exploration

Here are examples of using statistical methods to look at distribution of certain populations in my data and looking at the correlation of two factors using the knowledge of the distribution:

<img width="889" alt="Screenshot 2023-10-20 at 20 52 52" src="https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/c18f0bf3-c657-4b39-a0fd-c4a689ac19dc">

<img width="870" alt="Screenshot 2023-10-20 at 20 53 55" src="https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/fe3f213a-9134-4051-9ede-5795e9409fa3">

Hypothesis Testing

The null hypothesis of the test is that the time series can be represented by a unit root, that it is not stationary (has some time-dependent structure). The alternate hypothesis (rejecting the null hypothesis) is that the time series is stationary.

Null Hypothesis (H0): If failed to be rejected, it suggests the time series has a unit root, meaning it is non-stationary. It has some time dependent structure.
Alternate Hypothesis (H1): The null hypothesis is rejected; it suggests the time series does not have a unit root, meaning it is stationary. It does not have time-dependent structure. We interpret this result using the p-value from the test. A p-value below a threshold (such as 5% or 1%) suggests we reject the null hypothesis (stationary), otherwise a p-value above the threshold suggests we fail to reject the null hypothesis (non-stationary).

p-value > 0.05: Fail to reject the null hypothesis (H0), the data has a unit root and is non-stationary.

p-value <= 0.05: Reject the null hypothesis (H0), the data does not have a unit root and is stationary.

To gain a full understanding, please read the entirity of my project
