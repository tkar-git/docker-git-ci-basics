# CI basics

Continuous Integration (CI) is a software development practice where code changes are automatically built, tested, and deployed to ensure that the software is always in a releasable state. CI helps catch bugs early, improve code quality, and streamline the development process.

# CI tools
There are many CI tools available, each with its own features and capabilities. Some popular CI tools include:
- Jenkins
- Travis CI
- CircleCI
- GitLab CI
- GitHub Actions
- Azure DevOps


## CI pipeline
A CI pipeline is a series of automated steps that are executed whenever code changes are made. The pipeline typically includes the following stages:
1. **Build**: The code is compiled and built into an executable or deployable artifact. This step ensures that the code can be successfully built without any errors.
2. **Test**: Automated tests are run to verify that the code behaves as expected. This step helps catch bugs and ensures that new changes do not break existing functionality.
3. **Deploy**: The built artifact is deployed to a staging or production environment. This step ensures that the code is ready for release and can be tested in a real-world environment.


## CI configuration
The CI configuration file defines the steps and stages of the CI pipeline. The configuration file is typically written in YAML or JSON format and includes the following sections:
```yaml
name: <name of your workflow>

on: <event or list of events>

jobs:
  job_1:
    name: <name of the first job>
    runs-on: <type of machine to run the job on>
    steps:
      - name: <step 1>
        run: |
          <commands>
      - name: <step 2>
        run: |
          <commands>
  job_2:
    name: <name of the second job>
    runs-on: <type of machine to run the job on>
    steps:
      - name: <step 1>
        run: |
          <commands>
      - name: <step 2>
        run: |
          <commands>
```

Below is an example of a CI configuration file for a simple job that echoes "Hello, World!" and runs a test:
```yaml
name: example_ci

on: push

jobs:
  job_1:
    runs-on: ubuntu-latest
    steps:
      - name: test CI
        run: |
          echo "Hello there!"
          echo "I hope you are having a great day!"
          echo "This is a test CI job."
```

### Keywords
`name`: GitHub displays the names of your workflows on your repository’s actions page. If you omit name, GitHub sets it to the YAML file name.
`on`: (Required) This keyword specifies the events that trigger the CI pipeline. Common events include `push`, `pull_request`, and `schedule`. You can also specify multiple events using a list.
`jobs`: This keyword defines the jobs that will be executed in the CI pipeline. Each job can have its own set of steps and can run in parallel or sequentially.
 - `runs-on`: (Required) This keyword specifies the type of machine that the job will run on. Common options include `ubuntu-latest`, `windows-latest`, and `macos-latest`. For more on available runners, see [here](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions#jobsjob_idruns-on).
 - `steps`: Specify sequence of tasks. A step is an individual task that can run commands (known as actions). Each step in a job executes on the same runner, allowing the actions in that job to share data with each other. If you do not provide a name, the step name will default to the text specified in the run command.

## Exercise 1
1. Add the example ci configuration file to your repository. You can do this by creating a new file (e.g. main.yml) in the `.github/workflows` directory of your repository and pasting the example configuration into it. Make sure to commit and push the changes to your repository.
2. Now go to GitHub and navigate to the "Actions" tab of your repository. You should see the workflow listed there.

## Exercise 2
1. Add another job to the CI configuration file to build the cmake project we pushed to git yesterday. 
2. You can tests the build job to work on different Operating systems (e.g. ubuntu-latest, windows-latest, macos-latest) by changing the `runs-on` parameter in the configuration file.
3. You can also add a step to run the tests after the build step. This will ensure that the code is tested after it is built.


**Hint:** For GitHub Actions to have access to your code from your repository, you need to add the following under `steps`:
```yaml
- name: Checkout code
  uses: actions/checkout@v4
``` 
Here `@v4` uses version 4 of the official `actions/checkout` GitHub Actions which is the most stable and recent major realease.

You can use the following action to set up CMake:
```yaml
- name: Set up CMake
  uses: lukka/get-cmake@latest
```
For more details check [get-cmake](https://github.com/lukka/get-cmake)

