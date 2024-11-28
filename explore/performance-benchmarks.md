---
description: Proof of the pudding for scalability of Obsrv
---

# Performance Benchmarks

> <mark style="color:orange;">**Note:**</mark>**&#x20;**_<mark style="color:blue;">**This is a work in progress page. Following results are from initial benchmarks. Detailed benchmarks will be added shortly once the benchmark exercise is completed**</mark>_

### Cluster Size

| Config Name       | Config Value                                |
| ----------------- | ------------------------------------------- |
| Number of Nodes   | 4                                           |
| Node Size         | 4 core, 16 Gb                               |
| PV size           | 1 TB                                        |
| Installation Mode | Obsrv with monitoring and real-time storage |

### Processing Benchmarks

Processing benchmark is independent on number of datasets created, hence the strategy is to test with volume with all configurations enabled. Disabling any configuration is going to improve throughput

#### Configuration 1

1. Dedup turned on
2. De-normalization configured on 2 master datasets
3. Transformations configured on 2 fields
4. Event size of 1 kb

#### Results

| Flink Configuration                     | Events per Min                                 | Events per hour                                | Events per Day                                 |
| --------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| 1 CPU, 1GB, 1 task slot, 1 parallelism  | \~ 13k  \| 13 Mb                               | \~ 750k \| 780Mb                               | \~ 18Million \| 18Gb                           |
| 2 CPU, 2GB, 2 task slot, 2 parallelism  | \~ 30k  \| 30 Mb                               | \~ 1.8Million \| 1.8Gb                         | \~ 40Million \| 40Gb                           |
| 4 CPU, 4Gb, 4 task slots, 4 parallelism | <mark style="color:purple;">In Progress</mark> | <mark style="color:purple;">In Progress</mark> | <mark style="color:purple;">In Progress</mark> |

> Note: Many other scenarios with varying flink configurations are under benchmarking and will be updated post completion

### Secor Backups Benchmark

To ensure there is no data loss across obsrv pipeline all data is backuped to object store using S3. Following are the benchmark results of Secor backups in real-time

#### Configuration 1

1. Total Secor processes - 7
2. Total CPU Allocated - 1.5 cpu
3. Event size of 1 kb

#### Results

<table><thead><tr><th width="192">Events per Min</th><th width="187">Events per hour</th><th width="177">Events per Day</th><th>Events per process</th></tr></thead><tbody><tr><td>~ 1.6 Million | 1.6Mb</td><td>~ 100 Million | 100Gb</td><td>~ 2.4 Billion | 2.4Tb</td><td>~ 300 Million | 300Gb</td></tr></tbody></table>

> Note: In DIKSHA we have observed each secor process with 1cpu was able to upload 200Million events (200 Gb) to Azure blob storage

### Druid Indexing Benchmark

Druid indexing benchmark is dependent on number of datasets created and number of aggregate tables. This benchmark is done with minimal configuration only and can actually linearly scale with the number of CPUs provided

#### Minimum Configuration

| Config Name         | Config Value  |
| ------------------- | ------------- |
| Process Name        | Druid Indexer |
| CPU                 | 0.5           |
| Direct Memory       | 2Gi           |
| Heap                | 9Gi           |
| GlobalIngestionHeap | 8Gi           |
| Workers Count       | 30            |
| Pod Memory          | 11Gi          |

#### Results

<table><thead><tr><th width="154">Num of Tables</th><th width="144">Events per Min</th><th>Events per hour</th><th>Events per Day</th></tr></thead><tbody><tr><td>1</td><td>~ 80k  | 80 Mb</td><td>~ 4.8 Million | 4.8 Gb</td><td>~ 110 Million | 110 Gb</td></tr><tr><td>2</td><td>~ 40k | 40 Mb</td><td>~ 2.4 Million | 2.4 Gb</td><td>~ 55 Million | 55 Gb</td></tr><tr><td>3</td><td><mark style="color:purple;">In Progress</mark></td><td><mark style="color:purple;">In Progress</mark></td><td><mark style="color:purple;">In Progress</mark></td></tr><tr><td>4</td><td><mark style="color:purple;">In Progress</mark></td><td><mark style="color:purple;">In Progress</mark></td><td><mark style="color:purple;">In Progress</mark></td></tr><tr><td>5</td><td>~ 35k  | 35 Mb</td><td>~ 2.1 Million | 2.1 Gb</td><td>~ 50 Million | 50 Gb</td></tr></tbody></table>

> Note: How does the indexing scale when more cpu resources are provided will be added once the benchmark is complete

### Query Benchmark

Similar to processing, query benchmark is dependent on the volume of data but not on the number of datasets (or tables) created. Query performance will increase linearly with the amount of CPU/Memory assigned to the Druid Historical process

#### Minimum Configuration

| Config Name                | Config Value     |
| -------------------------- | ---------------- |
| Process Name               | Druid Historical |
| CPU                        | 2                |
| Direct Memory              | 4608Mi           |
| Heap                       | 1Gi              |
| Pod Memory                 | 5700Mi           |
| Segment Size               | 4.77Gi           |
| No. of rows per segment    | 5000000          |
| processing.numThreads      | 2                |
| processing.numMergeBuffers | 6                |
| Concurrency                | 100              |

#### RAW Table Results

<table><thead><tr><th width="224">Query</th><th width="138">Query Interval</th><th width="120">Throughput</th><th>Response Times (in ms)</th></tr></thead><tbody><tr><td>Group by on Raw Data </td><td>1 Day</td><td>25 r/s</td><td><p>Avg | Min | Max | 90th</p><p>392 | 80   | 686  | 472</p></td></tr><tr><td>Group by on Raw Data </td><td>7 Days</td><td>4 r/s</td><td><p>Avg   | Min  | Max  | 90th</p><p>4933 | 1277 | 8382 | 5154</p></td></tr><tr><td>Group by on Raw Data</td><td>30 Days</td><td><mark style="color:purple;">In Progress</mark></td><td><mark style="color:purple;">In Progress</mark></td></tr></tbody></table>

#### Aggregate (Rollup) Table Results

<table><thead><tr><th width="224">Query</th><th width="138">Query Interval</th><th width="120">Throughput</th><th>Response Times (in ms)</th></tr></thead><tbody><tr><td>Group by on Aggregate Data </td><td>1 Day</td><td><mark style="color:purple;">In Progress</mark></td><td><mark style="color:purple;">In Progress</mark></td></tr><tr><td>Group by on Aggregate Data </td><td>7 Days</td><td><mark style="color:purple;">In Progress</mark></td><td><mark style="color:purple;">In Progress</mark></td></tr><tr><td>Group by on Aggregate Data </td><td>30 Days</td><td><mark style="color:purple;">In Progress</mark></td><td><mark style="color:purple;">In Progress</mark></td></tr></tbody></table>

> Note: Multiple query types with varying interval and historical configuration combinations are being benchmarked actively and results will be updated once the activity is completed.&#x20;
