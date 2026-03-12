# Data Analysis Cheat Sheet: Pandas, NumPy, Matplotlib

## PANDAS

### DataFrame Creation
```python
df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4]})
df = pd.read_csv('file.csv')
df = pd.read_excel('file.xlsx')
df = pd.DataFrame(np.random.rand(5, 3), columns=['A', 'B', 'C'])
```

### Basic Inspection
```python
df.head() / df.tail()           # First/last rows
df.shape                        # (rows, columns)
df.info()                       # Data types & memory
df.describe()                   # Numeric statistics
df.dtypes                       # Column data types
df.columns                      # Column names
df.index                        # Row index
```

### Indexing & Selection
```python
df['col_name']                  # Single column (Series)
df[['col1', 'col2']]           # Multiple columns (DataFrame)
df.loc[row_label, 'col']       # Label-based indexing
df.iloc[row_num, col_num]      # Position-based indexing
df[df['col'] > 5]              # Boolean indexing
df.at[row, col] / df.iat[row, col]  # Single value access
```

### Data Cleaning
```python
df.drop('col', axis=1)          # Remove column
df.drop(0, axis=0)              # Remove row
df.dropna()                     # Remove NaN rows
df.drop_duplicates()            # Remove duplicates
df.fillna(value)                # Fill missing values
df.replace(old, new)            # Replace values
df.astype('int')                # Change data type
```

### Grouping & Aggregation
```python
df.groupby('col').sum()         # Group and sum
df.groupby('col').agg({'col2': 'mean', 'col3': 'count'})
df.groupby('col').apply(func)   # Apply function to groups
df.groupby(['col1', 'col2']).size()  # Multi-level grouping
df.pivot_table(values='val', index='idx', columns='col', aggfunc='sum')
```

### Merging & Combining
```python
pd.concat([df1, df2])           # Stack vertically
pd.concat([df1, df2], axis=1)  # Stack horizontally
pd.merge(df1, df2, on='key')   # SQL-style join
df1.merge(df2, left_on='col1', right_on='col2')  # Join on different columns
df.join(other_df, how='left')   # Index-based join
```

### Sorting & Ranking
```python
df.sort_values('col')           # Sort by column
df.sort_values(['col1', 'col2'], ascending=[True, False])
df.sort_index()                 # Sort by index
df.rank()                       # Rank values
df.nlargest(5, 'col')           # Top N values
```

### Data Transformation
```python
df.apply(func)                  # Apply function to columns
df.applymap(func)               # Apply to every element (deprecated: use map)
df.map(func)                    # Map values (Series)
df['new_col'] = df['col'].str.upper()  # String operations
df['new_col'] = pd.cut(df['col'], bins=5)  # Binning
```

### Statistics
```python
df.mean() / df.median() / df.std()
df.sum() / df.min() / df.max()
df.var() / df.quantile(0.25)
df.corr()                       # Correlation matrix
df.cov()                        # Covariance matrix
df.value_counts()               # Frequency count (Series)
```

### Time Series
```python
df['date'] = pd.to_datetime(df['date'])
df.set_index('date').resample('D').mean()  # Daily aggregation
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df.rolling(window=3).mean()     # Moving average
df.shift(1)                     # Lag/lead values
january = df[df["timestamp"].dt.month == 1]
year_2024 = df[df["timestamp"].dt.year == 2024]
one_day = df.loc["2024-01-05"]
range_df = df.loc["2024-01-03":"2024-01-07"]
january = df.loc["2024-01"]
year_2024 = df.loc["2024"]
```

---

## NUMPY

### Array Creation
```python
np.array([1, 2, 3])            # From list
np.zeros(5)                    # Array of zeros
np.ones((3, 4))                # Array of ones
np.arange(0, 10, 2)            # Range [0, 10) step 2
np.linspace(0, 1, 50)          # 50 evenly spaced values
np.random.rand(3, 4)           # Random [0, 1)
np.random.randint(0, 10, 5)    # Random integers
np.eye(3)                      # Identity matrix
```

### Array Manipulation
```python
arr.reshape(3, 4)              # Change shape
arr.flatten() / arr.ravel()    # Flatten to 1D
arr.T                          # Transpose
np.concatenate([arr1, arr2])   # Join arrays
np.vstack([arr1, arr2])        # Stack vertically
np.hstack([arr1, arr2])        # Stack horizontally
arr[arr > 5]                   # Boolean masking
```

### Math Operations
```python
arr + 5 / arr * 2              # Element-wise operations
np.sqrt(arr) / np.exp(arr)     # Element-wise math
np.dot(arr1, arr2)             # Matrix multiplication
np.sum() / np.mean() / np.std()
np.max() / np.min() / np.argmax()
np.unique(arr)                 # Unique values
np.where(condition, x, y)      # Conditional selection
```

### Useful Functions
```python
np.sort(arr)                   # Sort array
np.clip(arr, min_val, max_val) # Clip values
np.round(arr, 2)               # Round to 2 decimals
np.abs(arr)                    # Absolute value
np.cumsum(arr)                 # Cumulative sum
np.diff(arr)                   # Differences between elements
np.percentile(arr, 75)         # 75th percentile
```

---

## MATPLOTLIB

### Basic Plotting
```python
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 6))
plt.plot(x, y)                 # Line plot
plt.scatter(x, y)              # Scatter plot
plt.bar(x, y)                  # Bar chart
plt.hist(data, bins=20)        # Histogram
plt.boxplot(data)              # Box plot
plt.show()
```

### Multi-plot & Subplots
```python
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))
ax1.plot(x, y)
ax2.bar(x, y)
plt.tight_layout()
plt.show()
```

### Customization
```python
plt.xlabel('X Label')
plt.ylabel('Y Label')
plt.title('Plot Title')
plt.legend(['line1', 'line2'])
plt.grid(True, alpha=0.3)
plt.xlim(0, 10) / plt.ylim(0, 100)
ax.set_xticklabels(['A', 'B', 'C'], rotation=45)
plt.savefig('plot.png', dpi=300, bbox_inches='tight')
```

### Plot Types
```python
plt.plot(x, y, 'r-', linewidth=2)  # Line: 'r-', 'b--', 'g:', 'ko'
plt.scatter(x, y, s=50, alpha=0.6, c=colors)
plt.bar(x, y, width=0.4, color='skyblue', edgecolor='navy')
plt.hist(data, bins=30, color='green', edgecolor='black')
plt.pie(counts, labels=labels, autopct='%1.1f%%')
```

### Heatmaps & 2D
```python
import seaborn as sns

plt.imshow(data, cmap='viridis')
plt.colorbar()
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
sns.clustermap(data)
```

---

## COMMON PATTERNS

### Data Pipeline
```python
df = pd.read_csv('data.csv')
df = df.dropna()
df = df[df['col'] > threshold]
df['new_col'] = df['col'].apply(transform_func)
result = df.groupby('category').agg({'value': 'mean'})
```

### Filtering & Querying
```python
df.query('col1 > 5 and col2 < 10')
df[(df['A'] > 0) & (df['B'] < 100)]  # Use & | ~ for boolean logic
df.loc[df['col'].isin(['a', 'b', 'c'])]
```

### Performance Tips
```python
# Use vectorized operations instead of loops
df['result'] = df['A'] + df['B']  # Good
for i in df.index: df.loc[i, 'result'] = df.loc[i, 'A'] + df.loc[i, 'B']  # Bad

# Use .itertuples() or .iterrows() sparingly
for row in df.itertuples():
    print(row.col_name)

# Use categorical dtypes for memory efficiency
df['col'] = df['col'].astype('category')

# Use query() for complex conditions
df.query('A > B and C == "value"')
```

### Quick Stats
```python
df.describe()                   # 5-number summary
df.corr().abs().unstack().sort_values(ascending=False)  # Find correlations
(df.isnull().sum() / len(df) * 100).sort_values(ascending=False)  # Missing %
```

---

## DEBUGGING CHECKLIST

- **Shape mismatch**: Check `df.shape`, array dimensions
- **Type errors**: Verify `df.dtypes`, `arr.dtype`
- **NaN propagation**: Use `df.dropna()` or `df.fillna()`
- **Multiple index levels**: Use `.droplevel()` or `.reset_index()`
- **Groupby unexpected results**: Verify grouping columns, check for NaN
- **Memory issues**: Use `df.info()`, convert types, use `category`
- **Plot not showing**: Add `plt.show()` at the end
