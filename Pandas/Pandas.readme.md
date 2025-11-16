# Pandas Tutorial:

Here I'm going to make my own Pandas Cheat sheet.

### DataFrame()

- constructor to generate these DataFrame objects.
- Syntax for declaring a new one is a **dictionary** whose keys are the column names, and whose values are a **list** of entries.
- Use the _index_ parameter to assign index values.

Example:
`pd.DataFrame(
{
'Job':['ML eng','DS','AY Re'],
'Salary': [3000,2500,5400]
},
index=['A','B','C'])`

### Series()

- constructor to generate a single column of a DataFrame.
- Syntax for declaring a new one is a **List** with all values.
- Use the _index_ parameter to assign index values.
- Use the _name_ parameter to assign series name.

Example:
`pd.Series([500,800,900],index=[1,2,3] , name="MySeries")`

### read_csv()

- Reads .csv files
- File's url is passed as parameter

Example:
`data = pd.read_csv('c\:Files\data.csv')`

Notes:

- index_col=False can be used to force pandas to not use the first column as the index.
- index_col=0 can be used to force pandas to not use file indexes as a unnamed column.

### Shape attribute

- Used to check how large the resulting DataFrame is.

Example:
`data.shape`

### head()

- return the first 5 rows in a data set.

Example:
`data.head()`

### df.to_csv()

- Converts a data frame into a csv file.
- It must take path/name as parameter.
- It can have index=False to not include the index in the file.

Example:
`df.to_csv('c:\fils\data.csv',index=False)`

---

### df.column_name

- Get all data of that column.
- Selecting a specific Series out of a DataFrame.

Example:
`df.name`

### df['column_name']

- Get all data of that column.
- Selecting a specific Series out of a DataFrame.
- This will work better when we have coulmn names of two words (e.g., first name)

Example:
`df['name']`

### df['column_name'][index:int]

- Get a specifc value from series based on gaven index.

Example:
`df['name'][0]`

### df.iLoc[index:int]

- index-based selection: Selecting data based on its numerical position in the data.
- To select the a row of data in a DataFrame.
- Both **loc** and **iloc** are row-first, column-second. This is the opposite of what we do in native Python, which is column-first, row-second.
- This means that it's marginally easier to retrieve rows, and marginally harder to get retrieve columns.
- On its own, the : operator, which also comes from native Python, means "everything". When combined with other selectors, however, it can be used to indicate a range of values.
- When we use iloc we treat the dataset like a big matrix (a list of lists), one that we have to index into by position.
- iloc uses the Python stdlib indexing scheme, where the first element of the range is included and the last one excluded. So 0:10 will select entries 0,...,9.
- [row, column]
  [start:end:step]

Example:
`df.iloc[0] # returns the first row in the dataset
df.iloc[:, 0] # returns the first column in the dataset
df.iloc[:3, 0] # returns the first 3 values in the first coulmn
df.iloc[[0,1,2], 0] # returns the first 3 values in the first coulmn
df.iloc[1:3, 0] # returns the first **2** values in the first coulmn
df.iloc[-5:] # returns the last 5 rows in the data set
df.iloc[::5]means “start at the first row (index 0), go till the end, and step by 5: 0, 5, 10, 15, 20, etc.
df.iloc[1::5] start fro 1 and step by 5: 1,6,11,...
`

### df.loc["column_name"]

- label-based selection. In this paradigm, it's the data index value, not its position, which matters.
- loc uses the information in the indices to do its work. Since your dataset usually has meaningful indices.
- it's usually easier to do things using loc instead.
- loc, meanwhile, indexes inclusively. So 0:10 will select entries 0,...,10.
- [row, column]

Example:
`df.loc[0,'name'] # returns the first value in the "name" coulmn
df.loc[:, ['name','age','sex']] # returns all data for these columns
df.loc[:, 'name':'sex'] # returns all data for these columns ,,column slice`

### df.set_inddex(column_name)

- This method can be used to manipulate the index

Example:
`df.set_index("sex")`

### Conditional selection

- df.name == 'value' return series of true or false
- df.loc[df.name == 'value'] returns only the row that check the condition
- df.loc[(df.sex=='male')& (df.age >20)] return only rows that fit to the conditions
- df.loc[(df.sex=='female') | (df['class']=='First')]

### df.column.isin([...])

- isin lets you select data whose value "is in" a list of values.

Example:
`df.loc[df.age.isin([20,30,40])]`

### df.column.notnull()

- These method let you highlight values which are (or are not) empty (NaN).

Example:
`df.loc[df.age.notnull()]`

### df.column.isnull()

- These method let you highlight values which are NaN or Null.

Example:
`df.loc[df.age.isnull()]`

### df.column.median()

- These method gets you the median of a series in the dataframe.

Example:
`df.age.median()`

### df.column.mean()

- These method gets you the average of a series in the dataframe.

Example:
`df.age.mean()`

### df.groupby(column_name)

- It allows for the grouping of rows within a DataFrame based on one or more column values.
- This operation enables the application of aggregation functions or transformations to these groups.
- Take your big table, split it into smaller groups based on some column(s), and then let me do calculations on each group separately.
- Find patterns per group instead of across the whole dataset.

Example:
`df.groupby('Category')['Value'].sum()
df.loc[df.embarked == 'C'].groupby('sex')fare.mean()
df.groupby('sex')['fare'].agg(['mean', 'std', 'min', 'max'])`

### Assigning data

- df.sex= 1 this will assign all values = 1

---

### df.column.describe()

- This method generates a high-level summary of the attributes of the given column.
- is used to generate descriptive statistics that summarize the central tendency, dispersion, and shape of a dataset's distribution.
- It's a very useful function for getting a quick overview of your data.
- Numerical Data such as:
  count: Number of non-null values.
  mean: Average value.
  std: Standard deviation.
  min: Minimum value.
  25%: 25th percentile (first quartile).
  50%: 50th percentile (median or second quartile).
  75%: 75th percentile (third quartile).
  max: Maximum value.

- Categorical Data (Object/String): When applied to categorical data:
  count: Number of non-null values.
  unique: Number of unique categories.
  top: The most frequent category.
  freq: The frequency of the most frequent category.

Example:
`df.age.describe()
df.describe(include='object')
df.describe(include='all')
`

### df.column.unique()

- To see a list of unique values.

Example:
`df.age.unique()`

### df.column.value_counts()

- To see a list of unique values and how often they occur in the dataset.

Example:
`df.age.value_counts()`

### df.column.map(lampda)

- Used for applying functions or transformations to data.
- Primarily designed for Series objects (a single column in a DataFrame).
- Applying a function to each individual element of a Series.
- Mapping values in a Series to new values based on a dictionary or another Series.
- Returns a new Series with the transformed or mapped values.

Example:
`review_points_mean = reviews.points.mean()
reviews.points.map(lambda p: p - review_points_mean)`

### df.column.apply(function, axis="")

- Used for applying functions or transformations to data.
- Used on both Series and DataFrame objects.
- Series: Similar to map() for element-wise transformations, but also allows for more complex functions and passing additional arguments.
- DataFrame: Applying a function along an axis (row-wise or column-wise) or to individual elements. It can also perform aggregations.
- Takes a callable (function).
- Can return a scalar, a Series, or a DataFrame, depending on the function applied and the axis specified.

Example:
`
def remean_points(row):
row.points = row.points - review_points_mean
return row

reviews.apply(remean_points, axis='columns')
`

### Built-ins mapping operations:

- These operators are faster than map() or apply() because they use speed ups built into pandas.
- All of the standard Python operators (>, <, ==, and so on) work in this manner.
- However, they are not as flexible as map() or apply(), which can do more advanced things.

Example:
`reviews.points - 5
reviews.country + " - " + reviews.region_1`

### df.idxmax(axis="0,1")

- Used to find the index (or label) of the maximum value along a specified axis in a Series or DataFrame.
- By default, axis=0 (or 'index') means it operates column-wise. It returns a Series where the index is the column label.
- If axis=1 (or 'columns'), it operates row-wise. It returns a Series where the index is the row label.
- skipna=True (default) means NA/null values are excluded when determining the maximum.

Example:
`df.idxmax(axis=0)`

---

### df.sort_values(by='column', ascending=False)

- Used to sort a dataframe or series by column and asc/dasc.

Example:
`df.sort_values(by='age', ascending=False)
df.loc[:,'age'].sort_values( ascending=False)
df.loc[df.age.notnull()].sort_values( by='age',ascending=False)
df.loc[df.age.notnull()].age.sort_values(ascending=False)
df.sort_values(by=['age','fare'], ascending=False)

### df.sort_index(ascending=False)

- Used to sort a dataframe or series by index.

Example:
`df.sort_index()
`

---

### df.dtypes / column.dtype

- The dtype get the culumn data type, while dtypes return all datafram data types

Example:
`df.dtypes
df.age.dtype
`

### column.astype('type_name')

- Convert a column data type into other one.

Example:
`age.astype('float64')`

### column.fillna(new_value)

- Is used to replace NaN values in a column with new values.
- will not modify your original DataFrame/Series unless you explicitly tell it to.
- It create and return a modified copy, leaving the original untouched.
- If you set inplace=True, the operation will be applied directly to the original DataFrame/Series, and nothing is returned (None is returned instead).

Example:
`df.country.fillna('Unknown') # replace each NaN with an "Unknown"
df.fillna(0, inplace=True)
`

### column.replace(old_value, new_value)

- Is used to replace an old value with a new one.
- The same as fillna with inplace thing.

Example:
`df.country.replace('Amiraca','USA')
df.replace(2, 20, inplace=True)`

### df.rename()

- Used to rename index names and/or column names.
- rename() lets you rename index or column values by specifying a index or column keyword parameter, respectively.
- It supports a variety of input formats, but usually a Python dictionary is the most convenient.
- There is two useless methods called set_index(), and rename_axis().

Example:
`reviews.rename(columns={'points': 'score'})
reviews.rename(index={0: 'firstEntry', 1: 'secondEntry'})`

### pd.concat([...])

- Given a list of elements, this function will smush those elements together along an axis.
- combine different DataFrames and/or Series in non-trivial ways.

Example:
`
canadian_youtube = pd.read_csv("../input/youtube-new/CAvideos.csv")
british_youtube = pd.read_csv("../input/youtube-new/GBvideos.csv")

pd.concat([canadian_youtube, british_youtube])
`

### pd.join([...])

- lets you combine different DataFrame objects which have an index in common.
- The lsuffix and rsuffix parameters are necessary here because the data has the same column names in both British and Canadian datasets.
  If this wasn't true (because, say, we'd renamed them beforehand) we wouldn't need them.

Example:
`
left = canadian_youtube.set_index(['title', 'trending_date'])
right = british_youtube.set_index(['title', 'trending_date'])

left.join(right, lsuffix='\_CAN', rsuffix='\_UK')
`
