# Animal Center
<img src="https://images.unsplash.com/photo-1583337130417-3346a1be7dee?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OHx8YW5pbWFsc3xlbnwwfHwwfHx8MA%3D%3D" alt="drawing" width="500"/>

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
Find the total number of animals brought in each year.
```python
df['Year'] = df['DateTime'].dt.year #extract only the year into a new column

df.groupby(['Year','Animal Type']).size()
```

I also converted the _Age_upon_Intake_ column to weeks and extracted into a new column, as this would be useful for visualizations. Any value above 200 means the animal is 3 years or older.

With these, I could visualize the following for Insights:
- Total number of animals in the shlter
- Animals brought in by their conditions (normal, sick, injured, etc)
- Percentage of the types of animals taken in (stray, wildlifee, abandoned, etc)
- Age upon Intake (in weeks)
- Sex of animals (male, female)
- Total number of animals brought in yearly


  
