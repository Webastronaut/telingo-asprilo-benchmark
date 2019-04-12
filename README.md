# telingo-asprilo-benchmark

## Introduction

This repository encompasses the data I collected for my student project as well as the tools to replicate that data.

## Replicating the data

In order to get started make sure you have installed clingo 5.3 and telingo 1.0.1 on a cluster of your choice (I ran the benchmarks on a cluster with Linux, Intel Xeon E5-2650v4 processors with 2.20GHz and 64 GB memory), e.g. by executing:

```shell
conda install -c potassco clingo
conda install -c potassco telingo
```

Upload the folder `benchmark-tool` to the cluster. It contains all necessary test files and configurations to run the benchmarks. You do not need to change anything.
The test instances are located in the folder `benchmark-tool/benchmarks/asprilo`. Configuration files can be found in `benchmark-tool/runscripts/`.

### Running benchmarks

To run all benchmarks one by one change to the previously uploaded folder `benchmark-tool` and execute the following command per instance:

```shell
./bgen runscripts/runscript-asprilo-[VERSION].xml
```
This creates a shell script that will automatically run telingo with each of the respective test instances once the benchmark is started.

To start the benchmark run:

```shell
./output-asprilo-[VERSION]/asprilo-bmarks/zuse/start.sh
``` 

This has to be done for all given runscripts in order to reproduce all results.

For more information about the used benchmark tool check out the corresponding [repository](https://github.com/potassco/benchmark-tool).

## Collecting the data

Once a benchmark has finished download the folder

```shell
benchmark-tool/output-asprilo-[VERSION]/asprilo-bmarks/zuse/results/ALL/asprilo-pmork-Base/
```

from the cluster. It contains the command line output of each test. The provided Python script `create-csv.py` (Python v2.7) extracts these informations and generates a csv file:

```shell
python create-csv.py ./asprilo-pmork-Base/
```