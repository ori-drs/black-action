# black-action

This repository contains a configuration for a github action to apply a [black](https://github.com/psf/black) check on a repository. The action fails if the linter would modify files, to encourage consistent usage of formatting.

# Usage

To use this, you need to set up an action in the repository you want to check. An action is configured by a file in the repository at `.github/workflows/file.yaml`. You can also use the actions tab in github to get started. Below is an example workflow, which will run black on all python files in the repository if a pull request comes in.

```yaml

# This name appears in the actions list 
name: Linting

# Controls when the action will run. Triggers the workflow only when there is a pull request
on: [pull_request]

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "black-check"
  black-check:
    # The type of runner that the job will run on - this is github's linux server
    runs-on: ubuntu-latest
    # A job can have multiple steps
    steps:
    # We use one of github's actions to checkout the code into the docker instance that is created by the black-action repository
    - uses: actions/checkout@v1
    # Then, we run the black formatter
    - name: Run Black
      # From the repository in ori-drs, which contains a dockerfile
      uses: ori-drs/black-action@master
      # The dockerfile is run and receives arguments into the entrypoint.sh file. Here we pass the arguments we need to the formatter
      with:
        args: --check .
```