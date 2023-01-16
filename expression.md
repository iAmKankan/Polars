
## Expressions
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)
**Expressions** are the core strenght of **Polars**. The expressions offer a versatile structure that solves easy queries, but is easily extended to complex analyses. Below we will cover the basic components that serve as building block for all your queries.

* select
* filter
* with_columns
* Groupby
* Combining operations

## Combining dataframes
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)

* Join
* Concat

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
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)

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
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)

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


## Groupby
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)

We will create a new DataFrame for the **Groupby** functionality. This new DataFrame will include several 'groups' that we want to groupby.

```Python
df2 = pl.DataFrame({
                    "x": np.arange(0, 8), 
                    "y": ['A', 'A', 'A', 'B', 'B', 'C', 'X', 'X'],
})

print(df2)
```
```
shape: (8, 2)
┌─────┬─────┐
│ x   ┆ y   │
│ --- ┆ --- │
│ i64 ┆ str │
╞═════╪═════╡
│ 0   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌┤
│ 1   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌┤
│ 2   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌┤
│ 3   ┆ B   │
├╌╌╌╌╌┼╌╌╌╌╌┤
│ 4   ┆ B   │
├╌╌╌╌╌┼╌╌╌╌╌┤
│ 5   ┆ C   │
├╌╌╌╌╌┼╌╌╌╌╌┤
│ 6   ┆ X   │
├╌╌╌╌╌┼╌╌╌╌╌┤
│ 7   ┆ X   │
└─────┴─────┘
```
```Python
# without maintain_order you will get a random order back.
df2.groupby("y", maintain_order=True).count()
```
```
shape: (4, 2)
┌─────┬───────┐
│ y   ┆ count │
│ --- ┆ ---   │
│ str ┆ u32   │
╞═════╪═══════╡
│ A   ┆ 3     │
├╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ B   ┆ 2     │
├╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ C   ┆ 1     │
├╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ X   ┆ 2     │
└─────┴───────┘
```
```Python
df2.groupby("y", maintain_order=True).agg([
    pl.col("*").count().alias("count"),
    pl.col("*").sum().alias("sum")
])
```
```
shape: (4, 3)
┌─────┬───────┬─────┐
│ y   ┆ count ┆ sum │
│ --- ┆ ---   ┆ --- │
│ str ┆ u32   ┆ i64 │
╞═════╪═══════╪═════╡
│ A   ┆ 3     ┆ 3   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ B   ┆ 2     ┆ 7   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ C   ┆ 1     ┆ 5   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ X   ┆ 2     ┆ 13  │
└─────┴───────┴─────┘

```

#### More on groupby with expressions in the Polars Book: [link](https://pola-rs.github.io/polars-book/user-guide/dsl/groupby.html)

## Combining operations
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)

Below are some examples on how to combine operations to create the DataFrame you require.

```Python
# create a new colum that multiplies column `a` and `b` from our DataFrame
# select all the columns, but exclude column `c` and `d` from the final DataFrame

df_x = df.with_column(
    (pl.col("a") * pl.col("b")).alias("a * b")
).select([
    pl.all().exclude(['c', 'd'])
])

print(df_x)
```
```
shape: (8, 3)
┌─────┬──────────┬──────────┐
│ a   ┆ b        ┆ a * b    │
│ --- ┆ ---      ┆ ---      │
│ i64 ┆ f64      ┆ f64      │
╞═════╪══════════╪══════════╡
│ 0   ┆ 0.220182 ┆ 0.0      │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 1   ┆ 0.750839 ┆ 0.750839 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 2   ┆ 0.634639 ┆ 1.269277 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 3   ┆ 0.67404  ┆ 2.022121 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 4   ┆ 0.102818 ┆ 0.41127  │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 5   ┆ 0.896408 ┆ 4.482038 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 6   ┆ 0.062943 ┆ 0.377657 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 7   ┆ 0.108093 ┆ 0.756653 │
└─────┴──────────┴──────────┘
```
```Python
# only excluding column `d` in this example

df_y = df.with_columns([
    (pl.col("a") * pl.col("b")).alias("a * b")
]).select([
    pl.all().exclude('d')
])

print(df_y)
```
```
shape: (8, 4)
┌─────┬──────────┬─────────────────────┬──────────┐
│ a   ┆ b        ┆ c                   ┆ a * b    │
│ --- ┆ ---      ┆ ---                 ┆ ---      │
│ i64 ┆ f64      ┆ datetime[μs]        ┆ f64      │
╞═════╪══════════╪═════════════════════╪══════════╡
│ 0   ┆ 0.220182 ┆ 2022-12-01 00:00:00 ┆ 0.0      │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 1   ┆ 0.750839 ┆ 2022-12-02 00:00:00 ┆ 0.750839 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 2   ┆ 0.634639 ┆ 2022-12-03 00:00:00 ┆ 1.269277 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 3   ┆ 0.67404  ┆ 2022-12-04 00:00:00 ┆ 2.022121 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 4   ┆ 0.102818 ┆ 2022-12-05 00:00:00 ┆ 0.41127  │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 5   ┆ 0.896408 ┆ 2022-12-06 00:00:00 ┆ 4.482038 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 6   ┆ 0.062943 ┆ 2022-12-07 00:00:00 ┆ 0.377657 │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ 7   ┆ 0.108093 ┆ 2022-12-08 00:00:00 ┆ 0.756653 │
└─────┴──────────┴─────────────────────┴──────────┘
```
#### More oncontexts in expressions in the Polars Book: [link](https://pola-rs.github.io/polars-book/user-guide/dsl/contexts.html)

## Combining dataframes
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)

### Join
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

Let's have a closer look on how to join two DataFrames to a single DataFrame.

```Python
df = pl.DataFrame({"a": np.arange(0, 8), 
                   "b": np.random.rand(8), 
                   "c": [datetime(2022, 12, 1) + timedelta(days=idx) for idx in range(8)],
                   "d": [1, 2.0, np.NaN, np.NaN, 0, -5, -42, None]
                  })

df2 = pl.DataFrame({
                    "x": np.arange(0, 8), 
                    "y": ['A', 'A', 'A', 'B', 'B', 'C', 'X', 'X'],
})
```

Our two DataFrames both have an 'id'-like column: a and x. We can use those columns to join the DataFrames in this example.

```Python
df.join(df2, left_on="a", right_on="x")
```
```
shape: (8, 5)
┌─────┬──────────┬─────────────────────┬───────┬─────┐
│ a   ┆ b        ┆ c                   ┆ d     ┆ y   │
│ --- ┆ ---      ┆ ---                 ┆ ---   ┆ --- │
│ i64 ┆ f64      ┆ datetime[μs]        ┆ f64   ┆ str │
╞═════╪══════════╪═════════════════════╪═══════╪═════╡
│ 0   ┆ 0.220182 ┆ 2022-12-01 00:00:00 ┆ 1.0   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ 1   ┆ 0.750839 ┆ 2022-12-02 00:00:00 ┆ 2.0   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ 2   ┆ 0.634639 ┆ 2022-12-03 00:00:00 ┆ NaN   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ 3   ┆ 0.67404  ┆ 2022-12-04 00:00:00 ┆ NaN   ┆ B   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ 4   ┆ 0.102818 ┆ 2022-12-05 00:00:00 ┆ 0.0   ┆ B   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ 5   ┆ 0.896408 ┆ 2022-12-06 00:00:00 ┆ -5.0  ┆ C   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ 6   ┆ 0.062943 ┆ 2022-12-07 00:00:00 ┆ -42.0 ┆ X   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┤
│ 7   ┆ 0.108093 ┆ 2022-12-08 00:00:00 ┆ null  ┆ X   │
└─────┴──────────┴─────────────────────┴───────┴─────┘
```

#### Link to joins in the Polars Book: [link](https://pola-rs.github.io/polars-book/user-guide/howcani/combining_data/joining.html)
#### More information about joins in the Reference guide [link](https://pola-rs.github.io/polars/py-polars/html/reference/dataframe/api/polars.DataFrame.join.html#polars.DataFrame.join)

### Concat
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)
We can also concatenate two DataFrames. Vertical concatenation will make the DataFrame longer. Horizontal concatenation will make the DataFrame wider. Below you can see the result of an horizontal concatenation of our two DataFrames.

```Python
pl.concat([df,df2], how="horizontal")
```
```
shape: (8, 6)
┌─────┬──────────┬─────────────────────┬───────┬─────┬─────┐
│ a   ┆ b        ┆ c                   ┆ d     ┆ x   ┆ y   │
│ --- ┆ ---      ┆ ---                 ┆ ---   ┆ --- ┆ --- │
│ i64 ┆ f64      ┆ datetime[μs]        ┆ f64   ┆ i64 ┆ str │
╞═════╪══════════╪═════════════════════╪═══════╪═════╪═════╡
│ 0   ┆ 0.220182 ┆ 2022-12-01 00:00:00 ┆ 1.0   ┆ 0   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┼╌╌╌╌╌┤
│ 1   ┆ 0.750839 ┆ 2022-12-02 00:00:00 ┆ 2.0   ┆ 1   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┼╌╌╌╌╌┤
│ 2   ┆ 0.634639 ┆ 2022-12-03 00:00:00 ┆ NaN   ┆ 2   ┆ A   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┼╌╌╌╌╌┤
│ 3   ┆ 0.67404  ┆ 2022-12-04 00:00:00 ┆ NaN   ┆ 3   ┆ B   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┼╌╌╌╌╌┤
│ 4   ┆ 0.102818 ┆ 2022-12-05 00:00:00 ┆ 0.0   ┆ 4   ┆ B   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┼╌╌╌╌╌┤
│ 5   ┆ 0.896408 ┆ 2022-12-06 00:00:00 ┆ -5.0  ┆ 5   ┆ C   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┼╌╌╌╌╌┤
│ 6   ┆ 0.062943 ┆ 2022-12-07 00:00:00 ┆ -42.0 ┆ 6   ┆ X   │
├╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌┼╌╌╌╌╌┤
│ 7   ┆ 0.108093 ┆ 2022-12-08 00:00:00 ┆ null  ┆ 7   ┆ X   │
└─────┴──────────┴─────────────────────┴───────┴─────┴─────┘
```
#### Link to concatenation in the Polars Book: [link](https://pola-rs.github.io/polars-book/user-guide/howcani/combining_data/concatenating.html)
#### More information about concatenation in the Reference guide [link](https://pola-rs.github.io/polars/py-polars/html/reference/api/polars.concat.html#polars.concat)



               


