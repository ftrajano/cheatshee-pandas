# cheatshee-pandas
A cheatsheet for pandas most used commands.

## Series vs. Dataframes
When we have a dataframe df with 'a', 'b' columns, if we use 
```python
seriea = df['a']
```
The result of this atribution is a series. If we want a dataframe we should use 

```python 
dfa = df[['a']]
```

