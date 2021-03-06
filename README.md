# Snowflake Dataset

This repository contains documentation for the dataset that accompanies our NSDI 2020 paper, "Building an Elastic Query Engine on Disaggregated Storage". It also includes scripts to aid with processing of the data and to reproduce the analysis results in the paper.

## Main Dataset

The main dataset contains several statistics (timing, I/O, resource usage, etc..) pertaining to ~70 million queries from all customers that ran on [Snowflake](https://www.snowflake.com/) over a 14 day period from Feb 21st 2018 to March 7th 2018. This dataset is available in both CSV and Parquet formats and can be obtained from the [Downloads](download.md) page.

### Schema

Each row corresponds to one unique query with the columns representing various characteristics pertaining to that query. The **queryId** column contains a unique 64-bit identifier for each query. For a detailed description of all of the columns, please refer to the [Schema](schema.md) page. 

## Auxiliary Time-series Explosion

We also provide some auxiliary data to make it easier to perform time-series analysis (e.g. things like how do resource utilizations vary over time). This data is also available in both CSV and Parquet formats and can be obtained from the [Downloads](download.md) page. Note that this data can be computed from the main dataset, we are just providing a pre-computed version for convenience. 

### Schema

Each row consists of a **timestamp**, **queryId** pair indicating that query with identifier **queryId** was running/active at timestamp **timestamp**. For every query that is running/active at **timestamp** there will be one such row. So to compute a time-series of how many queries were active at given timestamp, one could simply do the equivalent of `SELECT COUNT(*) AS queryCount GROUP BY timestamp`. To bring in other query statistics one can join this data with the main dataset on the **queryId** column.  For more details, please refer to the [Schema](schema.md) page. 

## Scripts

The [scripts/](scripts/) directory has some helper scripts to aid with dataset manipulation. This includes AWK headers and some sample pandas scripts. In addition the [paper-results/](paper-results/) directory contains a set of IPython notebooks (written mostly using pandas) that can re-produce all of the results in our NSDI 2020 paper.

## Limitations

## Privacy Concerns

All identifiers in the dataset that could potentially reveal a customer's identity have been replaced by pseudo-random numbers to preserve anonymity. Public access to the information in this dataset does not lead to any privacy or other ethical concerns.

## Contact

Midhul Vuppalapati ([midhul@cs.cornell.edu](mailto:midhul@cs.cornell.edu))

## Usage

Information in this dataset is open to the public for use in research and education purposes. Kindly cite the following publication if you are using our dataset:

```
@inproceedings {snowflake-nsdi20,
author = {Midhul Vuppalapati and Justin Miron and Rachit Agarwal and Dan Truong and Ashish Motivala and Thierry Cruanes},
title = {Building An Elastic Query Engine on Disaggregated Storage },
booktitle = {17th {USENIX} Symposium on Networked Systems Design and Implementation ({NSDI} 20)},
year = {2020},
isbn = {978-1-939133-13-7},
address = {Santa Clara, CA},
pages = {449--462},
url = {https://www.usenix.org/conference/nsdi20/presentation/vuppalapati},
publisher = {{USENIX} Association},
month = feb,
}
```

