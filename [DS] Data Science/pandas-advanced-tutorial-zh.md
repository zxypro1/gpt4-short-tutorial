## Pandas高级教程

### 1. 处理缺失数据

Pandas使用`np.nan`表示缺失数据。Pandas的所有描述性统计默认都不包括缺失数据。

```python
# 重构数据使其具有一个新的索引
df1 = df.reindex(index=dates[0:4], columns=list(df.columns) + ['E'])

# 修改值
df1.loc[dates[0]:dates[1], 'E'] = 1
```

- **丢弃缺失数据**

```python
# 丢弃包含缺失数据的行
df1.dropna(how='any')

# 只丢弃所有列都是NaN的行
df1.dropna(how='all')
```

- **填充缺失数据**

```python
# 将缺失的数据填充为指定的值
df1.fillna(value=5)

# 提供一个用于填充的字典，每列一个值
df1.fillna({'A': 0, 'B': 1, 'C': 2, 'D': 3, 'E': 4})
```

- **检查缺失数据**

```python
# 得到一个布尔掩码，显示哪些值是缺失的
pd.isna(df1)
```

### 2. 多重索引

Pandas提供了多种方法来处理多重索引的数据。

```python
# 创建一个具有多重索引的DataFrame
tuples = list(zip(*[['bar', 'bar', 'baz', 'baz', 'foo', 'foo', 'qux', 'qux'],
                    ['one', 'two', 'one', 'two', 'one', 'two', 'one', 'two']]))
index = pd.MultiIndex.from_tuples(tuples, names=['first', 'second'])
df = pd.DataFrame(np.random.randn(8, 2), index=index, columns=['A', 'B'])
```

- **堆叠和非堆叠**

```python
# 非堆叠
df2 = df[:4]
stacked = df2.stack()

# 堆叠
stacked.unstack()
```

- **索引操作**

```python
# 选择
df.loc['bar']

# 交换索引级别
df.swaplevel(0, 1)

# 排序索引
df.sort_index(level=1)
```

### 3. 分类

Pandas可以包含分类数据。

```python
df = pd.DataFrame({"id": [1, 2, 3, 4, 5, 6], "raw_grade": ['a', 'b', 'b', 'a', 'a', 'e']})

# 将raw grades转化为分类数据类型
df["grade"] = df["raw_grade"].astype("category")

# 重命名分类为更有意义的名称
df["grade"].cat.categories = ["very good", "good", "very bad"]

# 重新排序分类并同时添加缺失的分类
df["grade"] = df["grade"].cat.set_categories(["very bad", "bad", "

# 重新排序分类并同时添加缺失的分类
df["grade"] = df["grade"].cat.set_categories(["very bad", "bad", "medium", "good", "very good"])
```

- **排序是按照分类，而不是词汇顺序进行的**

```python
df.sort_values(by="grade")
```

- **按照分类列分组时，也包括了空的分类**

```python
df.groupby("grade").size()
```

### 4. 可视化

Pandas内置了一些画图方法，依赖于matplotlib。

```python
import matplotlib.pyplot as plt

# Series和DataFrame上的这些功能只是使用matplotlib库的plot()方法的简单包装实现
ts = pd.Series(np.random.randn(1000), index=pd.date_range('1/1/2000', periods=1000))
ts = ts.cumsum()

ts.plot()
plt.show()
```

### 5. 数据输入 / 输出

Pandas可以读取和写入各种格式的数据，如CSV，Excel，SQL，HDF5等。

```python
# 写入CSV
df.to_csv('foo.csv')

# 从CSV读取
pd.read_csv('foo.csv')

# 写入HDF5
df.to_hdf('foo.h5','df')

# 从HDF5读取
pd.read_hdf('foo.h5','df')

# 写入Excel
df.to_excel('foo.xlsx', sheet_name='Sheet1')

# 从Excel读取
pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA'])
```

这些只是Pandas高级特性的一部分，它还有更多的功能等待你去发掘和学习。我建议你可以阅读[Pandas的官方文档](https://pandas.pydata.org/docs/)来获取更多的信息。希望你在学习过程中能有所收获！