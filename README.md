# Animal Center


## Exploratory Data Analysis with Python

Going through kaggle.com, I came across this dataset for animal shelter in Austin, and I found it useful to practice my Python skills 

The following were covered:
- Grouping and Sorting
- Data Types and missing values
- Renaming and Combining



## Import the Libraries

Before tackling a project, you must first understand what you want to achieve and how to achieve it.
You have to import the important library you will need. For this dataset, i imported 

**Numpy**

**Matplotlib**

**Seaborn**

**Datetime (as we have a column "DATETIME")**

- Set the parameters for the visulaizations like the size, color, and the style of plot to use

## Import and Load the Data
We are working with a Comma Seperated Values file (CSV). To import into the notebook, we use

**pd.csv('name_of_file.csv')** and assign it to a variable named **df**, then run df

Going through the dataframe, we can see that some rows are empty, DATETIME and MONTHYEAR columns are the same, a name has an unwanted character. 

## Data Cleaning

Run 
```python
df.insna().sum() 
```
To know the number of empty cells in the dataframe.
Since the empty rows are just in columns NAME and SEX_UPON_INTAKE, we fill them with _Unknown_, then make sure it effects the dataframe

```python
df.fillna('Unknown', inplace=True)
```
To delete irrelevant columns, we use the drop method

```python
col = ['MONTHYEAR', 'ANIMAL ID']

df.drop(col, axis = 1, inplace=True)
```
Convert DATETIME to pandas _datetime_

```python
df['DATETIME'] = pd.to_datetime(df['DateTime'], format= '%m/%d/%Y %I:%M:%S %p')
```
Extract words into a new column. I wasn't satisfied with the SEX_UPON_INTAKE column, as i only needed to know if they were _male_ or _female_

```python
df['New_Sex'] = df['Sex upon Intake'].str.extract(r'(Male|Female|Unknown)')
```

I also converted the _Age_upon_Intake_ column to weeks and extracted into a new column, as this would be useful for visualizations. Any value above 200 means the animal is 3 years or older.

With these, I could visualize the data for Insights


  
