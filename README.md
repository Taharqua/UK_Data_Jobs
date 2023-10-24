# Analysing the UK Data Job Market in 2021

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

![image](https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/c682730b-803e-45ed-aca1-6fb9be98feda)


### Distribution Exploration

A key component of the looking at factors which influence the pay rates is looking at the distribution of the data ensuring we are able to use the correct statistical methods to gain insight. This is extremely common when finding outliers and test for correlation as methods such as Grubbs' test for Outliers or Pearson's Correlation Coefficient work on the presumption of normailty, meaning if the data is not at a normal distribution, these methods are not applicable.

Here is an example of using statistical methods to look the distribution of a certain population in my data.

<img width="870" alt="Screenshot 2023-10-20 at 20 53 55" src="https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/fe3f213a-9134-4051-9ede-5795e9409fa3">

### Hypothesis Testing

Hypothesis Testing is a byproduct of Distribution Exploration as we need to know the distribution of our data to properly use the correct test.

The null hypothesis of the test is that there is a correlation between the total number of skills required for the role and the salary. The alternate hypothesis (rejecting the null hypothesis) is that there isn't a correlation between the total number of skills required for the role and the salary.

We interpret this result using the p-value from the test. A p-value below a threshold (such as 5% or 1%) suggests we reject the null hypothesis, otherwise a p-value above the threshold suggests we fail to reject the null hypothesis ).

p-value > 0.05: There is no siginificance (H0).

p-value <= 0.05: There is significance (H0)

<img width="889" alt="Screenshot 2023-10-20 at 20 52 52" src="https://github.com/Taharqua/UK_Data_Jobs/assets/56850203/c18f0bf3-c657-4b39-a0fd-c4a689ac19dc">

To gain a full understanding, please read the entirity of my project
