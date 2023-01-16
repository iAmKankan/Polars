## Read From files
![light](https://user-images.githubusercontent.com/12748752/212648973-a46457e4-8150-42e8-929a-e422a9ed5962.png)

In Polars we can also read files and create a ***DataFrame***. In the following examples we write the output of the ***DataFrame*** from the previous part to a specific file type (**csv**, **json** and **parquet**). After that we will read it and print the output for inspection.

### csv

#### Example #1:

* [Source](#A-DataFrame-is-created-from-a-dict-or-a-collection-of-dicts.)

```Python
>>> dataframe.write_csv('output.csv')
```
```Python
>>> df_csv = pl.read_csv('output.csv')
>>> print(df_csv)
```
```
shape: (3, 3)
┌─────────┬────────────────────────────┬───────┐
│ integer ┆ date                       ┆ float │
│ ---     ┆ ---                        ┆ ---   │
│ i64     ┆ str                        ┆ f64   │
╞═════════╪════════════════════════════╪═══════╡
│ 1       ┆ 2022-01-01T00:00:00.000000 ┆ 4.0   │
├╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 2       ┆ 2022-01-02T00:00:00.000000 ┆ 5.0   │
├╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 3       ┆ 2022-01-03T00:00:00.000000 ┆ 6.0   │
└─────────┴────────────────────────────┴───────┘
```

As we can see above, Polars made the datetimes a string. We can tell Polars to parse dates, when reading the csv, to ensure the date becomes a datetime. The example can be found below:


```Python
>>> df_csv_with_dates = pl.read_csv('output.csv', parse_dates=True)

>>> print(df_csv_with_dates)
```

### json

```Python
dataframe.write_json('output.json')

df_json = pl.read_json('output.json')

print(df_json)
```
```
shape: (3, 3)
┌─────────┬─────────────────────┬───────┐
│ integer ┆ date                ┆ float │
│ ---     ┆ ---                 ┆ ---   │
│ i64     ┆ datetime[μs]        ┆ f64   │
╞═════════╪═════════════════════╪═══════╡
│ 1       ┆ 2022-01-01 00:00:00 ┆ 4.0   │
├╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 2       ┆ 2022-01-02 00:00:00 ┆ 5.0   │
├╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 3       ┆ 2022-01-03 00:00:00 ┆ 6.0   │
└─────────┴─────────────────────┴───────┘
```

### parquet

```Python
dataframe.write_parquet('output.parquet')

df_parquet = pl.read_parquet('output.parquet')

print(df_parquet)
```
```
shape: (3, 3)
┌─────────┬─────────────────────┬───────┐
│ integer ┆ date                ┆ float │
│ ---     ┆ ---                 ┆ ---   │
│ i64     ┆ datetime[μs]        ┆ f64   │
╞═════════╪═════════════════════╪═══════╡
│ 1       ┆ 2022-01-01 00:00:00 ┆ 4.0   │
├╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 2       ┆ 2022-01-02 00:00:00 ┆ 5.0   │
├╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 3       ┆ 2022-01-03 00:00:00 ┆ 6.0   │
└─────────┴─────────────────────┴───────┘
```
