# How to Install CausalBench
Install the latest version of CausalBench package on pip:
`pip install causalbench-asu`

## Prerequisites
CausalBench package requires several packages and registration to the CausalBench in order to run.
### Package Prerequisites:
CausalBench requires several packages in order to execute, these packages are downloaded alongisde CausalBench:
- "gputil",
- "requests",
- "pyyaml",
- "bunch_py3",
- "pandas",
- "jsonschema",
- "pipreqs",
- "psutil",
- "py-cpuinfo",
- "pip-system-certs",
- "pyadl",
- "gcastle",
- "torch~=2.3.0"

### Configuration

CausalBench requires an user account registered in [https://causalbench.org](https://causalbench.org) for authenticating with the system, downloading and uploading benchmark components.

During execution, CausalBench creates a .causalbench folder in the user directory, which will host any downloaded components and user configuration. In order to authenticate with the system, you must create a `config.yaml` file with your username and password/access token in this format (without brackets):

```yaml
email: [your email address]
password: [your access token/password]
```