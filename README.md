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



## References 
![dark](https://user-images.githubusercontent.com/12748752/212648966-d8f080dc-5022-41f0-a571-90f5d9aef139.png)
* [Jeff's Video](https://www.youtube.com/watch?v=J0wpRP-ExVg)
* [Jeff's Notebook](https://github.com/jeffheaton/present/blob/master/youtube/polars/polars.ipynb)
* [Polars Doc](https://pola-rs.github.io/polars-book/user-guide/index.html)
* [Polars Github](https://github.com/pola-rs/polars)

