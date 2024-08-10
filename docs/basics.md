# CausalBench 101

## Dataset
- **Description**: Data and configuration files that describe the data in the data files.

### How to define a dataset
A dataset is defined with a yaml configuration, and the data files.
Any dataset configuration must inlcude a type, name, task(?), files defined. Files need to be configured with `type`, `data` type, file path in `path`, and any columns with their details.  
Optional fields are: `headers`, `version_num`, that defines the versions, `url`, `source` and `description` that define the dataset.

```yaml
type: dataset
name: abalone
source: UCI
url: https://archive.ics.uci.edu/dataset/1/abalone
description: Predict the age of abalone from physical measurements
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
A model is defined with a yaml configuration, alongside a python script that the model is executed on. A model must have a type, name, task and its path defined.

Optional fields are: `version_num`, that defines the versions, `url`, `source` and `description` that define the model.

```yaml
type: model
name: VAR-LiNGAM
source: GitHub
url: https://github.com/huawei-noah/trustworthyAI/tree/master/gcastle
description: Discovery of non-gaussian linear causal models
task: discovery.temporal
path: varlingam.py
version_num: 1
```

## Metric
- **Description**: Python implementations of metric calculations.
- **Function**: Take in the outputs provided by the model and output a numerical value, based on its configuration.

### How to define a metric
```yaml
type: metric
name: accuracy_static
source: NA
url: NA
description: Accuracy metric for static causal graph.
task: discovery.static
path: accuracy_static.py
```

## Context
- **Description**: A configuration that encapsulates a selected set of multiple datasets, models, metrics and hyperparameters.
- **Function**: Defined by users, contexts represent experiments carried out on a selection of components. Contexts are defined on user level, and all of the dataset-model tuple combinations are created and executed on the system level.

### How to define a context
A context is created with a yaml notation. Any context should have a type, name, task(?), and at least one dataset, model and metric defined.

```yaml
name: Context Abhinav 1
task: discovery.static
description: July experiment set
datasets:
- id: 14
  version: 1
- id: 15
  version: 1
models:
- id: 22
  version: 1
- id: 17
  version: 1
metrics:
- id: 12
  version: 1
- id: 12
  version: 2
```

## Task
- **Description**: Logical definition of Causal/Machine Learning tasks.
- **Function**: Handles configurations between dataset/model/metric components through python functions.

### How to define a task
A task takes in two files: a `.yaml` file that defines the type, name, path and the class name of a task, and a `.py` file that defines the task and its execution.

The yaml file should only include the `type`, `name`, `path`, and the `class` fields.
```yaml
type: task
name: discovery.static
path: discovery.static.py
class_name: DiscoveryStatic
```

The python file should include any input and output functions for any dataset -> model, model -> metric, dataset -> metric relations, and the helper functions to facilitate the task. discovery.static.py and discovery.temporal.py files under the `/task` folder provides examples on construction of these functions.

## Benchmark
- **Description**: Benchmark defines run results of a number of executed contexts. 
On top of the executed context structure, benchmark includes run-configuration specific information like the system configuration, GPU-CPU resource profiling. 