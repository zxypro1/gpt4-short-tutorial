

## Pandas基础教程

### 1. 导入 Pandas

在你开始使用 Pandas 之前，你需要先导入它。习惯上，我们将 pandas 导入为 "pd"。

```python
import pandas as pd
```

### 2. 数据结构

Pandas 主要有两种数据结构：Series（一维）和 DataFrame（二维）。

- **Series** 是一种类似于一维数组的对象，它由一组数据（各种 NumPy 数据类型）以及一组与之相关的数据标签（即索引）组成。

```python
s = pd.Series([1, 3, 5, np.nan, 6, 8])
```

- **DataFrame** 是一种二维标签化数据结构，可以容纳许多不同类型的输入，如字典、二维 ndarray、Series 或另一个 DataFrame。

```python
df = pd.DataFrame({'A': 1.,
                   'B': pd.Timestamp('20130102'),
                   'C': pd.Series(1, index=list(range(4)), dtype='float32'),
                   'D': np.array([3] * 4, dtype='int32'),
                   'E': pd.Categorical(["test", "train", "test", "train"]),
                   'F': 'foo'})
```

### 3. 读取和写入数据

Pandas 可以读取和写入许多不同的数据格式，包括但不限于 CSV、Excel 和 SQL 数据库。

- **读取数据**

```python
# 读取 CSV 文件
df = pd.read_csv('filename.csv')

# 读取 Excel 文件
df = pd.read_excel('filename.xlsx')

# 从 SQL 数据库中读取
import sqlite3
con = sqlite3.connect('database.db')
df = pd.read_sql_query("SELECT * FROM tablename", con)
```

- **写入数据**

```python
# 将数据写入 CSV 文件
df.to_csv('filename.csv')

# 将数据写入 Excel 文件
df.to_excel('filename.xlsx')
```

### 4. 数据选择与过滤

你可以使用许多不同的方式来选择或过滤你的数据。

- **选择**

```python
# 选择一列，返回一个 Series
df['A']

# 选择多行，返回一个 DataFrame
df[0:3]

# 按标签选择
df.loc[dates[0]]

# 按位置选择
df.iloc[3]
```

- **过滤**

```python
# 使用单个列的值来选择数据
df[df['A'] > 0]

# 使用 where 操作来过滤
df[df > 0]
```

### 5. 数据清洗

数据清洗是一个重要的步骤，Pandas 提供了许多工具来帮助你。

```python
# 丢弃缺失的数据
df.dropna(how='any')

# 填充缺失的数据
df.fillna(value=5)

# 获取数据的布尔掩码，表示哪些值是缺失的
pd.isna(df)
```

### 6. 数据操作

你可以对 DataFrame 进行许多不同的操作，例如统计、应用函数等。

- **统计**

```python
# 执行描述性统计
df.describe()

# 计算均值
df.mean()

# 计算两个列（或行）的相关系数
df['A'].corr(df['B'])
```

- **应用函数**

```python
# 将函数应用到数据上
df.apply(np.cumsum)

# 应用 lambda 函数
df.apply(lambda x: x.max() - x.min())
```

### 7. 合并与分组

Pandas 提供了大量的方法来合并 DataFrame 和对数据进行分组操作。

- **合并**

```python
# 使用 concat 合并 DataFrame
df = pd.concat([df1, df2])

# 使用 merge 合并 DataFrame
df = pd.merge(df1, df2, on='key')
```

- **分组**

```python
# 按某列的值分组
df.groupby('A')

# 分组并应用函数
df.groupby('A').sum()
```

### 8. 重塑与透视

你可以使用各种方法来重塑或透视你的数据。

```python
# 设置新的索引
df.set_index('A')

# 重塑数据
df.pivot_table(index='A', columns='B', values='C')
```

Pandas 的功能远不止这些，它还提供了大量的方法和函数来处理时间序列、分类数据、可视化等等。你可以访问 [Pandas 的官方文档](https://pandas.pydata.org/docs/) 来获取更多信息。我建议你在学习过程中多做笔记，多实践，这样你就可以更好地理解和记住这些概念和方法了。
