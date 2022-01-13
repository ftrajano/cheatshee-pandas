# cheatsheet-pandas
A cheatsheet for pandas most used commands.

### Index
1. <a href="#brackets">Brackets</a>
2. <a href="#loc">loc</a>
3. <a href="#iloc">iloc</a>
4. <a href="#boolean_numpy">Boolean Operators (Numpy)</a>
5. <a href="#datetime">Datetime</a>
6. <a href="#iterrows">iterrow</a>
7. <a href="#itertuples">itertuple</a>
8. <a href="#apply">apply</a>

## Index and Select Data
* Brackets
* Advanced Method
  1. loc (label-based)
  2. iloc (integer position-based)

<h2 id="brackets">Brackets</h2>

### Column Access

Series vs. Dataframes
When we have a dataframe df with 'a', 'b' columns, if we use 
```python
seriea = df['a']
```
The result of this atribution is a series. If we want a dataframe we should use 

```python 
dfa = df[['a']]
```

Using the doublem brackets we can select several columns 
```python
df_ab = df[['a', 'b']]
```

### Row access
We should use index slice
```python
df[1:4]
```

<h2 id="loc"><strong>loc</strong></h2>

### Row Access loc

```python
df.loc['label_of row'] 
df.loc[['label1', 'label2', 'label3']]
```

### Row & Column loc
```python
df.loc[['row_label'], ['column label']]
```

### Column access
```python
df.loc[:, ['column label']]
```


<h2 id="iloc"> <strong>iloc</strong></h2>

### Row Access iloc
```python
df.iloc[[1]]
df.iloc[[1,2,3]]
```

### Row & Column iloc
```python
df.iloc[[1,2,3],[0,1]]
```

<h3> Column Access iloc</h3>

```python
df.iloc[:,[0,1]]
```

<h2 id="boolean_numpy"><strong>Boolean Operators (numpy)</strong></h2>
Sometimes we want to use boolean propositions to elements of an array. In these cases we should use the Numpy Boolean Operators

* logical_and()
* logical_or()
* logical_not()

```python
array1 = [10, 100, 200]
np.logical_and(array1>10, array1<200) #[False, True, False] 

```

<h2 id="datetime">Datetime</h2>

for more information access: 
<a href="https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html">pandas.to_datetime</a>

For dataframes that have informations about dates we can use several forms to deal with them.

```python
pd.read_csv('../my_dataset.csv', parse_dates=['column1', 'column2'])
```
These atributes of read_csv try to parse the information as date objects.

another way is using 

```python
# the format string helps panda to identify the format of the data in your dataset and errors='coerce' transforms data that is not in our format to NaT
pd.to_datetime(df['column'], format='%d/%m/%Y %H:%M', errors='coerce')
```

<h3>Timedelta</h3>
for more information access:
<a href="https://pandas.pydata.org/docs/reference/api/pandas.Series.dt.html?highlight=pandas%20series%20dt#pandas.Series.dt"> pandas.Series.dt</a>
when we need to do math with dates we have to pay attention to the timedelta operator.
If we simply subrtrack two dates, the result is a kind of data that has "days" in the data.
to get a number we should use 

```python
(data1-data2).dt.days 
```

<h2 id="iterrows">iterrows</h2>

for more information access:
<a href="https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.iterrows.html"> pandas.DataFrame.iterrows()</a>

if we need to use a for loop in the rows of a data frame one of the best ways is to use pandas.DataFrame.iterrows()
I think that it returns an iterable tuple of index and row

```python
for i, row in df.iterrows()
  print(i)
  print(row)
```


<h2 id="itertuples">itertuples</h2>

for more information access:
<a href="https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.itertuples.html"> pandas.DataFrame.iterrows()</a>

Another way of iterate over a dataframe is using itertuples. Using this method we get as an output a named tuple ( from collections)
it works as a tuple but to access their items we should use dot notation with the name of the atributes (df's colum names(?))

```python
for named_tuple in df.itertuples()
  print(named_tuple.Index)
  print(named_tuple.Other_column)
```

<h2 id="apply">Using apply for loop on dataframes</h2>

we can use lambda functions in pandas.DataFrame.apply()
```python
applied = df.apply(
    lambda row: calculate(row['a'], row['b'], axis=1) # this will iterate over rows, remember 0 for columns and 1 for rows
df['new_column'] = applied # the apply method returns a series(?)
```

Examples:
<table>
  <tr>
    <th></th>
    <th>RS</th>
    <th>RA</th>
    <th>W</th>
    <th>Playoffs</th>
  </tr>
  <tr>
    <td>2012</td>
    <td>697</td>
    <td>577</td>
    <td>90</td>
    <td>0</td>
  </tr>
  <tr>
    <td>2011</td>
    <td>707</td>
    <td>614</td>
    <td>91</td>
    <td>1</td>
  </tr>
<tr>
  <td>2009  </td>
    <td>803  </td>
    <td>754  </td>
    <td>84        </td>
    <td> 0</td>
  </tr>
<tr>
  <td>2010</td>
    <td>802</td>
    <td>649</td>
    <td>96</td>
    <td>1</td>
  </tr>
<tr>
  <td>2008</td>
    <td>  774  </td>
    <td>671</td>
    <td>  97</td>
    <td>1</td>
  </tr>
</table>

```python
# Gather sum of all columns
stat_totals = rays_df.apply(sum, axis=0)
print(stat_totals)

"""
RS          3783
RA          3265
W            458
Playoffs       3
dtype: int64"""

# Gather total runs scored in all games per year
total_runs_scored = rays_df[['RS', 'RA']].apply(sum, axis=1)
print(total_runs_scored)

"""
2012    1274
2011    1321
2010    1451
2009    1557
2008    1445
dtype: int64"""

# Convert numeric playoffs to text by applying text_playoffs()
textual_playoffs = rays_df.apply(lambda row: text_playoffs(row['Playoffs']), axis=1)
print(textual_playoffs)

"""<script.py> output:
    2012     No
    2011    Yes
    2010    Yes
    2009     No
    2008    Yes
    dtype: object"""

```


