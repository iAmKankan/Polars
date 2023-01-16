
## Expressions
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)
**Expressions** are the core strenght of **Polars**. The expressions offer a versatile structure that solves easy queries, but is easily extended to complex analyses. Below we will cover the basic components that serve as building block for all your queries.

* select
* filter
* with_columns

## Select statement
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)

To select a column we need to do two things. 
* Define the **DataFrame** we want the data from. 
* And select the data that we need. 


In the example below you see that we select **col('*')**. _The asteriks stands for all columns_.

```Python
df.select(
    pl.col('*')
)
```
```
shape: (8, 4)
┌─────┬──────────┬─────────────────────┬───────┐
│ a   ┆ b        ┆ c                   ┆ d     │
│ --- ┆ ---      ┆ ---                 ┆ ---   │
│ i64 ┆ f64      ┆ datetime[μs]        ┆ f64   │
╞═════╪══════════╪═════════════════════╪═══════╡
│ 0   ┆ 0.164545 ┆ 2022-12-01 00:00:00 ┆ 1.0   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 1   ┆ 0.747291 ┆ 2022-12-02 00:00:00 ┆ 2.0   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 2   ┆ 0.889227 ┆ 2022-12-03 00:00:00 ┆ NaN   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 3   ┆ 0.736651 ┆ 2022-12-04 00:00:00 ┆ NaN   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 4   ┆ 0.099687 ┆ 2022-12-05 00:00:00 ┆ 0.0   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 5   ┆ 0.965809 ┆ 2022-12-06 00:00:00 ┆ -5.0  │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 6   ┆ 0.93697  ┆ 2022-12-07 00:00:00 ┆ -42.0 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 7   ┆ 0.848925 ┆ 2022-12-08 00:00:00 ┆ null  │
└─────┴──────────┴─────────────────────┴───────┘
```

You can also specify the specific columns that you want to return. There are two ways to do this. 

1. The first option is to create a **list of column names**, as seen below.


```Python
df.select(
    pl.col(['a', 'b'])
)
```
```shape: (8, 2)
┌─────┬──────────┐
│ a   ┆ b        │
│ --- ┆ ---      │
│ i64 ┆ f64      │
╞═════╪══════════╡
│ 0   ┆ 0.164545 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 1   ┆ 0.747291 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 2   ┆ 0.889227 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 3   ┆ 0.736651 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 4   ┆ 0.099687 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 5   ┆ 0.965809 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 6   ┆ 0.93697  │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 7   ┆ 0.848925 │
└─────┴──────────┘
```
2. The second option is to specify each column within a list in the select statement. This option is shown below.

```Python
# in this example we limit the number of rows returned to 3, as the comparison is clear.
# this also shows how easy we can extend our expression to what we need. 
df.select([
    pl.col('a'),
    pl.col('b')
]).limit(3)
```
```
shape: (3, 2)
┌─────┬──────────┐
│ a   ┆ b        │
│ --- ┆ ---      │
│ i64 ┆ f64      │
╞═════╪══════════╡
│ 0   ┆ 0.164545 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 1   ┆ 0.747291 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 2   ┆ 0.889227 │
└─────┴──────────┘
```

### Exclude statement
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

If you want to exclude an entire column from your view, you can simply use exclude in your select statement.

```Python
df.select([
    pl.exclude('a')
])
```
```
shape: (8, 3)
┌──────────┬─────────────────────┬───────┐
│ b        ┆ c                   ┆ d     │
│ ---      ┆ ---                 ┆ ---   │
│ f64      ┆ datetime[μs]        ┆ f64   │
╞══════════╪═════════════════════╪═══════╡
│ 0.220182 ┆ 2022-12-01 00:00:00 ┆ 1.0   │
├╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 0.750839 ┆ 2022-12-02 00:00:00 ┆ 2.0   │
├╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 0.634639 ┆ 2022-12-03 00:00:00 ┆ NaN   │
├╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 0.67404  ┆ 2022-12-04 00:00:00 ┆ NaN   │
├╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 0.102818 ┆ 2022-12-05 00:00:00 ┆ 0.0   │
├╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 0.896408 ┆ 2022-12-06 00:00:00 ┆ -5.0  │
├╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 0.062943 ┆ 2022-12-07 00:00:00 ┆ -42.0 │
├╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 0.108093 ┆ 2022-12-08 00:00:00 ┆ null  │
└──────────┴─────────────────────┴───────┘
```
#### More on Polars expression book [link](https://pola-rs.github.io/polars-book/user-guide/dsl/expressions.html)

## Filter
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

The filter option allows us to create a subset of the DataFrame. We use the same DataFrame as earlier and we filter between two specified dates.

```Python
df.filter(
    pl.col("c").is_between(datetime(2022, 12, 2), datetime(2022, 12, 8)),
)
```
```
shape: (5, 4)
┌─────┬──────────┬─────────────────────┬───────┐
│ a   ┆ b        ┆ c                   ┆ d     │
│ --- ┆ ---      ┆ ---                 ┆ ---   │
│ i64 ┆ f64      ┆ datetime[μs]        ┆ f64   │
╞═════╪══════════╪═════════════════════╪═══════╡
│ 2   ┆ 0.634639 ┆ 2022-12-03 00:00:00 ┆ NaN   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 3   ┆ 0.67404  ┆ 2022-12-04 00:00:00 ┆ NaN   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 4   ┆ 0.102818 ┆ 2022-12-05 00:00:00 ┆ 0.0   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 5   ┆ 0.896408 ┆ 2022-12-06 00:00:00 ┆ -5.0  │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 6   ┆ 0.062943 ┆ 2022-12-07 00:00:00 ┆ -42.0 │
└─────┴──────────┴─────────────────────┴───────┘
```

With **filter** you can also create more complex filters that include **multiple columns**.

```Python
df.filter(
    (pl.col('a') <= 3) & (pl.col('d').is_not_nan())
)
```
```
shape: (2, 4)
┌─────┬──────────┬─────────────────────┬─────┐
│ a   ┆ b        ┆ c                   ┆ d   │
│ --- ┆ ---      ┆ ---                 ┆ --- │
│ i64 ┆ f64      ┆ datetime[μs]        ┆ f64 │
╞═════╪══════════╪═════════════════════╪═════╡
│ 0   ┆ 0.220182 ┆ 2022-12-01 00:00:00 ┆ 1.0 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ 1   ┆ 0.750839 ┆ 2022-12-02 00:00:00 ┆ 2.0 │
└─────┴──────────┴─────────────────────┴─────┘
```

#### More about finter and condition [link](https://pola-rs.github.io/polars-book/user-guide/dsl/expressions.html#filter-and-conditionals)

## With_columns
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

**with_colums** allows you to create new columns for you analyses. We create to new columns **e** and **b+42**. First we sum all values from column **b** and store the results in column **e**. After that we add **42** to the values of **b**. Creating a new column **b+42** to store these results.

```Python
df.with_columns([
    pl.col('b').sum().alias('e'),
    (pl.col('b') + 42).alias('b+42')
])
```
```
shape: (8, 6)
┌─────┬──────────┬─────────────────────┬───────┬──────────┬───────────┐
│ a   ┆ b        ┆ c                   ┆ d     ┆ e        ┆ b+42      │
│ --- ┆ ---      ┆ ---                 ┆ ---   ┆ ---      ┆ ---       │
│ i64 ┆ f64      ┆ datetime[μs]        ┆ f64   ┆ f64      ┆ f64       │
╞═════╪══════════╪═════════════════════╪═══════╪══════════╪═══════════╡
│ 0   ┆ 0.606396 ┆ 2022-12-01 00:00:00 ┆ 1.0   ┆ 4.126554 ┆ 42.606396 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌┤
│ 1   ┆ 0.404966 ┆ 2022-12-02 00:00:00 ┆ 2.0   ┆ 4.126554 ┆ 42.404966 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌┤
│ 2   ┆ 0.619193 ┆ 2022-12-03 00:00:00 ┆ NaN   ┆ 4.126554 ┆ 42.619193 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌┤
│ 3   ┆ 0.41586  ┆ 2022-12-04 00:00:00 ┆ NaN   ┆ 4.126554 ┆ 42.41586  │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌┤
│ 4   ┆ 0.35721  ┆ 2022-12-05 00:00:00 ┆ 0.0   ┆ 4.126554 ┆ 42.35721  │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌┤
│ 5   ┆ 0.726861 ┆ 2022-12-06 00:00:00 ┆ -5.0  ┆ 4.126554 ┆ 42.726861 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌┤
│ 6   ┆ 0.201782 ┆ 2022-12-07 00:00:00 ┆ -42.0 ┆ 4.126554 ┆ 42.201782 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌┤
│ 7   ┆ 0.794286 ┆ 2022-12-08 00:00:00 ┆ null  ┆ 4.126554 ┆ 42.794286 │
└─────┴──────────┴─────────────────────┴───────┴──────────┴───────────┘
```







