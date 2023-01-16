
## Expressions
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)
**Expressions** are the core strenght of **Polars**. The expressions offer a versatile structure that solves easy queries, but is easily extended to complex analyses. Below we will cover the basic components that serve as building block for all your queries.

* select
* filter
* with_columns

### Select statement
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

To select a column we need to do two things. Define the DataFrame we want the data from. And second, select the data that we need. In the example below you see that we select col('*'). The asteriks stands for all columns.

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

You can also specify the specific columns that you want to return. There are two ways to do this. The first option is to create a list of column names, as seen below.


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

