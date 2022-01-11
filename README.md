# cheatsheet-pandas
A cheatsheet for pandas most used commands.

## Index and Select Data
* Brackets
* Advanced Method
  1. loc (label-based)
  2. iloc (integer position-based)

## Brackets
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

## **loc**
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


## **iloc**
### Row Access iloc
```python
df.iloc[[1]]
df.iloc[[1,2,3]]
```

### Row & Column iloc
```python
df.iloc[[1,2,3],[0,1]]
```

### Column Access iloc
```python
df.iloc[:,[0,1]]
```
