# How to Run CausalBench
You can use the [python notebook](../files/CausalBench-Quickstart.ipynb) attached, or follow along this page to get CausalBench into action.

## Install CausalBench,
Please follow the [installation guide](../install/) for installing CausalBench.

Install the latest version of CausalBench package on pip:
`pip install causalbench-asu`

## Create a context
```python
    context1: Context = Context.create(module_id=10,
                                        name='Context1',
                                        description='Test static context',
                                        task='discovery.static',
                                        datasets=[(dataset1, {'data': 'file1', 'ground_truth': 'file2'})],
                                        models=[model1, model2],
                                        metrics=[metric1, metric2])
```

## Download a pre-set context
Downloading a pre-set context (or any component) is straightforward, create a context object, and provide the `module_id` and `version` you'd like to download from the CausalBench context repository.
```python
context1: Context = Context(module_id=1, version=1)
```

## Upload a component
You can publish any component with the `publish()` function. Publish function takes in the `public` boolean argument which is `False` by default. In case you wish to publish directly as public, set the argument as `True`.

```python
context1.publish(public=True)
```

## Run a benchmark
With a set context, running a benchmark is done with `execute()` function.
```python
run: Run = context1.execute()
```
This will execute the benchmark.
You can also print the run using `print(run)` command.

## Upload results
Uploading results works the same as uploading any component, by using the `publish()` function.
```python
run.publish(public=True)
```

## Example CausalBench Execution:
This example will fetch a context, execute it, and upload the results.
```python
from causalbench.modules import Run
from causalbench.modules.context import Context

def main():

    # Select and fetch the Context
    context1: Context = Context(module_id=1, version=1)

    # Run selected Context
    run: Run = context1.execute()

    # Print Run execution results
    print(run)

    # Publish the Run
    run.publish()

if __name__ == '__main__':
    main()
```