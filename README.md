## Index 
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)


## Polars
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)
Polars is a **fast**, **multi-threaded**, **hybrid-out-of-core**, **_DataFrame_** library in _Rust_, Python & Node.js

It is a very fast _DataFrames_ library implemented in _Rust_ using _Apache Arrow Columnar Format_ as the memory model.

* Lazy / eager execution
* Multi-threaded
* SIMD
* Query optimization
* Powerful expression API
* Hybrid Streaming (larger than RAM datasets)
* Rust / Python / NodeJS / ...

The goal of Polars is to provide a lightning fast DataFrame library that utilizes all available cores on your machine. Unlike tools such as dask -- which tries to parallelize existing single-threaded libraries like **NumPy** and **Pandas** -- 

Polars is written from the ground up, designed for parallelization of queries on DataFrames.

Polars goes to great lengths to:

* Reduce redundant copies
* Traverse memory cache efficiently
* Minimize contention in parallelism

Polars is **lazy** and **semi-lazy**. It allows you to do most of your work eagerly, similar to Pandas, but it also provides a powerful expression syntax that will be optimized and executed on within the query engine.

In lazy Polars we are able to do query optimization on the entire query, further improving performance and memory pressure.

Polars keeps track of your query in a logical plan. This plan is optimized and reordered before running it. When a result is requested, Polars distributes the available work to different executors that use the algorithms available in the eager API to produce a result. Because the whole query context is known to the optimizer and executors of the logical plan, processes dependent on separate data sources can be parallelized on the fly.

### Difference with pandas
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

|Pandas|Polars|
|:-----|:-----|
|Indexing in _DF_| No Indexing in _DF_|


## Installetion and Import
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)
```Python
!pip install polars 
```
or
```Python
!pip install -U polars
```

### Import Polars as follows:
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

```Python
import polars as pl

# to enrich the examples in this quickstart with dates
from datetime import datetime, timedelta 
# to generate data for the examples
import numpy as np 
```

## Object creation
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

### From scratch

Creating a simple **Series** or **Dataframe** is easy and very familiar to other packages.

You can create a **Series** in Polars by providing a **list** or a **tuple**.



## Gyanas on Polars ***Series*** and ***DataFrame***
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

### 1. [***Series***](https://pola-rs.github.io/polars/py-polars/html/reference/series/index.html)

A *Series* represents a single column in a polars **DataFrame**.


```Python
class polars.Series(
name: str | ArrayLike | None = None, 
values: ArrayLike | None = None, 
dtype: PolarsDataType | None = None, 
strict: bool = True, nan_to_null: bool = False, 
dtype_if_empty: PolarsDataType | None = None)
```
#### Examples #1:
* Constructing a Series by specifying name and values positionally:
```Python
>>> s = pl.Series("a", [1, 2, 3])
>>> s
shape: (3,)
Series: 'a' [i64]
[
        1
        2
        3
]
```


It is possible to construct a Series with values as the first positional argument. This syntax considered an anti-pattern, but it can be useful in certain scenarios. You must specify any other arguments through keywords.

**Note:** that the *dtype* is automatically inferred as a polars *Int64*:

```Python
>>> s.dtype
Int64
```

Constructing a Series with a specific dtype:
```Python
>>> s2 = pl.Series("a", [1, 2, 3], dtype=pl.Float32)
>>> s2
shape: (3,)
Series: 'a' [f32]
[
    1.0
    2.0
    3.0
]
```

### 2. [*DataFrame*](https://pola-rs.github.io/polars/py-polars/html/reference/dataframe/index.html)

Two-dimensional data structure representing data as a table with **rows** and **columns**.



```Python
class polars.DataFrame(
    data: Mapping[str, Sequence[object] | Mapping[str, Sequence[object]] | Series] | Sequence[Any] |
    np.ndarray[Any, Any] | pa.Table | pd.DataFrame | Series | None = None,
    columns: ColumnsType | None = None, orient: Orientation | None = None, 
    infer_schema_length: int | None = 100
)
```

#### Notes:
Some methods internally convert the DataFrame into a LazyFrame before collecting the results back into a DataFrame. This can lead to unexpected behavior when using a subclassed DataFrame. For example,

```Python
>>> class MyDataFrame(pl.DataFrame):
...    pass
...
>>> isinstance(MyDataFrame().lazy().collect(), MyDataFrame)
False
```
#### Examples #1:

Constructing a DataFrame from a dictionary:

```Python
>>> data = {"a": [1, 2], "b": [3, 4]}
>>> df = pl.DataFrame(data)
df
>>> shape: (2, 2)
┌─────┬─────┐
│ a   ┆ b   │
│ --- ┆ --- │
│ i64 ┆ i64 │
╞═════╪═════╡
│ 1   ┆ 3   │
│ 2   ┆ 4   │
└─────┴─────┘
```


Set the columns parameter with a list of (name,dtype) pairs (compatible with all of the other valid data parameter types):

```Python
>>> data = {"col1": [1, 2], "col2": [3, 4]}
>>> df3 = pl.DataFrame(data, columns=[("col1", pl.Float32), ("col2", pl.Int64)])
>>> df3
shape: (2, 2)
┌──────┬──────┐
│ col1 ┆ col2 │
│ ---  ┆ ---  │
│ f32  ┆ i64  │
╞══════╪══════╡
│ 1.0  ┆ 3    │
│ 2.0  ┆ 4    │
└──────┴──────┘
```

The columns parameter could also be set with a **dict** containing the *schema* of the expected ***DataFrame***.

```Python
>>> data = {"col1": [0, 2], "col2": [3, 7]}
>>> df4 = pl.DataFrame(data, columns={"col1": pl.Float32, "col2": pl.Int64})
>>> df4
shape: (2, 2)
┌──────┬──────┐
│ col1 ┆ col2 │
│ ---  ┆ ---  │
│ f32  ┆ i64  │
╞══════╪══════╡
│ 0.0  ┆ 3    │
│ 2.0  ┆ 7    │
└──────┴──────┘
```

Constructing a DataFrame from a numpy ndarray, specifying column names:

```Python
>>> import numpy as np
>>> data = np.array([(1, 2), (3, 4)], dtype=np.int64)
>>> df5 = pl.DataFrame(data, columns=["a", "b"], orient="col")
>>> df5
shape: (2, 2)
┌─────┬─────┐
│ a   ┆ b   │
│ --- ┆ --- │
│ i64 ┆ i64 │
╞═════╪═════╡
│ 1   ┆ 3   │
│ 2   ┆ 4   │
└─────┴─────┘
```

Constructing a DataFrame from a list of lists, row orientation inferred:

```Python
>>> data = [[1, 2, 3], [4, 5, 6]]
>>> df6 = pl.DataFrame(data, columns=["a", "b", "c"])
>>> df6
shape: (2, 3)
┌─────┬─────┬─────┐
│ a   ┆ b   ┆ c   │
│ --- ┆ --- ┆ --- │
│ i64 ┆ i64 ┆ i64 │
╞═════╪═════╪═════╡
│ 1   ┆ 2   ┆ 3   │
│ 4   ┆ 5   ┆ 6   │
└─────┴─────┴─────┘
```








## References 
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)
* [Jeff's Video](https://www.youtube.com/watch?v=J0wpRP-ExVg)
* [Jeff's Notebook](https://github.com/jeffheaton/present/blob/master/youtube/polars/polars.ipynb)
* [Polars Doc](https://pola-rs.github.io/polars-book/user-guide/index.html)
* [Polars Github](https://github.com/pola-rs/polars)

