# cheatsheet-pandas
A cheatsheet for pandas most used commands.

### Index
1. <a href="#brackets">Brackets</a>
2. <a href="#loc">loc</a>
3. <a href="#iloc">iloc</a>
4. <a href="#boolean_numpy">Boolean Operators (Numpy)</a>

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
Sometime we want to use boolean propositions to elements of an array. In these cases we should use the Numpy Boolean Operators

* logical_and()
* logical_or()
* logical_not()


