# CausalBench 101

## Dataset
- **Description**: Data and configuration files that describe the data in the data files.

### How to define a dataset
A dataset is defined with a yaml configuration, and the data files.
Any dataset configuration must inlcude a type, name, task(?), files defined. Files need to be configured with `type`, `data` type, file path in `path`, and any columns with their details.  
Optional fields are: `headers`.

```yaml
type: dataset
name: abalone

files:
    file1:
        type: csv
        data: dataframe
        path: abalone.mixed.numeric.csv
        headers: true
        columns:
            sex:
                header: Sex
                type: nominal
                data: integer
                labels:
                    - 0
                    - 1
                    - 2
            ...
    file2:
        type: csv
        data: graph
        path: causal_info_adjmat.csv
        headers: true
        columns:
            sex:
                header: Sex
                type: nominal
                data: integer
            ...
```

## Model
- **Description**: Algorithms written in Python that take in a dataset and execute a particular model.
- **Function**: Produce outputs based on the tasks and models.

### How to define a model
A model is defined with a yaml configuration, alongside a python script that the model is executed on. A model must have a type, name, task(?), path, and its inputs and outputs defined.
Optional fields are: `version_num`, that defines the versions, `arguments` that define any arguments and hyperparameters a model can take.

```yaml
type: model
name: tcdf
task: discovery
path: tcdf.py
version_num: 1
arguments:
    kernel_size:
        type: int
        default_value: 4
        description: Size of sliding kernel

inputs:
    data:
        id: data
        data: dataframe
    space:
        id: space
        data: graph
outputs:
    prediction:
        id: pred
        data: graph
```

## Metric
- **Description**: Python implementations of metric calculations.
- **Function**: Take in the outputs provided by the model and output a numerical value, based on its configuration.

### How to define a metric
...

## Context
- **Description**: A configuration that encapsulates a selected set of multiple datasets, models, metrics and hyperparameters.
- **Function**: ...

### How to define a context
A context is created with a yaml notation. Any context should have a type, name, task(?), and at least one dataset, model and metric defined.  

```yaml
type: context
name: TCDF Discovery
task: discovery.static
dataset:
    id: 0
    version_num: 1
model:
    id: 1
    version_num: 1
    parameters:
        data: file1
metrics:
    -   id: 0
        version_num: 1
        parameters:
            ground_truth: file2
    -   id: 1
        version_num: 1
        parameters:
            ground_truth: file2
model_hyperparameters:
    kernel_size: 8
    learning_rate: 0.05
```

## Benchmark
- **Description**: Benchmark defines run results of a number of executed contexts. 
...
