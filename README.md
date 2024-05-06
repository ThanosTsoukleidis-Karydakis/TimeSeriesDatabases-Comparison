# Comparison of CrateDB and QuestDB Time Series DBs
Term project for the course 'Analysis and Design of Information Systems', NTUA, 2023/24

## Objective:
This project was carried out as the chosen term project for the course of "Analysis and Design of Information Systems" at the School of Electrical and Computer Engineering of the National Technical University of Athens. The objective is a comparative study of QuestDB and CrateDB, two Time-Series DBs - databases oriented and adapted for managing time-series data -, and includes the installation and setup of the system, that will host the two databases, and of the databases themselves, the data generation and insertion into the two DBs and the query generation and execution. Afterwards, we attempt to compare the two databases' performance in different important procedures that take place during time-series data collection and analysis, such as data ingestion, execution of query batches (concurrent requests to the DB) and execution of atomic/single queries. With a view to compare the databases, suitable performance measurements were carried out, and namely data insertion and query execution time, thoughput, latency, cpu usage and node/cluster load (cluster load only for CrateDB, the only distributed DB amongst the two), whose results are attempted to be explained and justified based on the structural characteristics of the two databases. Ultimately, conclusions are drawn regarding the conditions under which the use of each of the two databases under consideration is most appropriate.

## Collaborators:
- [Dimitrios-David Gerokonstantis](https://github.com/DimitrisDavidGerokonstantis)  (el19209)
- [Athanasios Tsoukleidis-Karydakis](https://github.com/ThanosTsoukleidis-Karydakis)  (el19009)
- [Filippos Sevastakis](https://github.com/FilipposSevastakis) (el19183)

## Setup:

### Cluster setup:
The system setup - a cluster consisting of 3 VMs - can be found in the [System setup README](./System_setup/README.md).

### Databases' Setup:
The installation & setup guides for the two databases under consideration can be found in [CrateDB's setup guide](/CrateDB/README.md) and [QuestDB's setup guide](/QuestDB/README.md).

### Cluster overview:
<p align="center">
  <img src="https://github.com/FilipposSevastakis/InformationSystems_TermProject/assets/106911339/09703bd0-78d3-4896-b7e5-724c4a30cb77">
</p>


## Queries:
The queries that were executed by both CrateDB and QuestDB so as to compare the databases' performance can be found in the [Queries directory](./Queries) and consist of batch-queries of Time Series Benchmark Suite, as well as single-queries of our own making.

## Measurement results - Logs:
Measurement results, as they were taken in the course of this project, are presented in the [logs file](./logs.docx).

## Report:
In the [Report directory](./Report) one can find the report, as well as its Latex code (for anyone interested).

## Presentation:
In the [Presentation directory](./Presentation) one can find the complementary presentation of the project, along with its Latex code (for anyone interested).
