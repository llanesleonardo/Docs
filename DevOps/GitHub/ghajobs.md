# Github Actions Jobs

## Using jobs in a workflow

Use workflows to run multiple jobs.

A workflow run is made up of one or more jobs, which run in parallel by default. To run jobs sequentially, you can define dependencies on other jobs using the jobs.<job_id>.needs keyword.

Each job runs in a runner environment specified by runs-on.

You can run an unlimited number of jobs as long as you are within the workflow usage limits.

If you need to find the unique identifier of a job running in a workflow run, you can use the GitHub API.

## Setting an ID for a job

Use jobs.<job*id> to give your job a unique identifier. The key job_id is a string and its value is a map of the job's configuration data. You must replace <job_id> with a string that is unique to the jobs object. The <job_id> must start with a letter or * and contain only alphanumeric characters, -, or \_.

### Example: Creating jobs

In this example, two jobs have been created, and their job_id values are my_first_job and my_second_job.

```
jobs:
  my_first_job:
    name: My first job
  my_second_job:
    name: My second job
```

## Setting a name for a job

Use jobs.<job_id>.name to set a name for the job, which is displayed in the GitHub UI.

## Defining prerequisite jobs

Use jobs.<job_id>.needs to identify any jobs that must complete successfully before this job will run. It can be a string or array of strings. If a job fails or is skipped, all jobs that need it are skipped unless the jobs use a conditional expression that causes the job to continue. If a run contains a series of jobs that need each other, a failure or skip applies to all jobs in the dependency chain from the point of failure or skip onwards.

### Example: Requiring successful dependent jobs

```
jobs:
  job1:
  job2:
    needs: job1
  job3:
    needs: [job1, job2]
```

In this example, job1 must complete successfully before job2 begins, and job3 waits for both job1 and job2 to complete.

The jobs in this example run sequentially:

1. job1
2. job2
3. job3

### Example: Not requiring successful dependent jobs

```
    jobs:
    job1:
    job2:
    needs: job1
    job3:
    if: ${{ always() }}
    needs: [job1, job2]
```

In this example, job3 uses the always() conditional expression so that it always runs after job1 and job2 have completed, regardless of whether they were successful.

## Choose the runner for a job

Define the type of machine that will process a job in your workflow.

[Choose the runner for a job](https://docs.github.com/en/actions/using-jobs/choosing-the-runner-for-a-job)

## Using conditions to control job execution

Prevent a job from running unless your conditions are met.

You can use the jobs.<job_id>.if conditional to prevent a job from running unless a condition is met. You can use any supported context and expression to create a conditional.

When you use expressions in an if conditional, you may omit the expression syntax (${{ }}) because GitHub automatically evaluates the if conditional as an expression.

### Example: Only run job for specific repository

This example uses if to control when the production-deploy job can run. It will only run if the repository is named octo-repo-prod and is within the octo-org organization. Otherwise, the job will be marked as skipped.

On a skipped job, you should see "This check was skipped."

## Using Matrices for your jobs

Create a matrix to define variations for each job.

A matrix strategy lets you use variables in a single job definition to automatically create multiple job runs that are based on the combinations of the variables. For example, you can use a matrix strategy to test your code in multiple versions of a language or on multiple operating systems.

[Using matrices for your jobs](https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs)

## Using concurrency

Run a single job at a time.

You can use jobs.<job_id>.concurrency to ensure that only a single job or workflow using the same concurrency group will run at a time. A concurrency group can be any string or expression. Allowed expression contexts: github, inputs, vars, needs, strategy, and matrix.

You can also specify concurrency at the workflow level.

When a concurrent job or workflow is queued, if another job or workflow using the same concurrency group in the repository is in progress, the queued job or workflow will be pending. Any previously pending job or workflow in the concurrency group will be canceled. To also cancel any currently running job or workflow in the same concurrency group, specify cancel-in-progress: true.

### Examples: Using concurrency and the default behavior

```
concurrency: staging_environment
concurrency: ci-${{ github.ref }}
```

### Example: Using concurrency to cancel any in-progress job or run

```
concurrency:
group: ${{ github.ref }}
cancel-in-progress: true
```

### Example: Using a fallback value

If you build the group name with a property that is only defined for specific events, you can use a fallback value. For example, github.head_ref is only defined on pull_request events. If your workflow responds to other events in addition to pull_request events, you will need to provide a fallback to avoid a syntax error. The following concurrency group cancels in-progress jobs or runs on pull_request events only; if github.head_ref is undefined, the concurrency group will fallback to the run ID, which is guaranteed to be both unique and defined for the run.

```
concurrency:
  group: ${{ github.head_ref || github.run_id }}
  cancel-in-progress: true
```

### Example: Only cancel in-progress jobs or runs for the current workflow

If you have multiple workflows in the same repository, concurrency group names must be unique across workflows to avoid canceling in-progress jobs or runs from other workflows. Otherwise, any previously in-progress or pending job will be canceled, regardless of the workflow.

To only cancel in-progress runs of the same workflow, you can use the github.workflow property to build the concurrency group:

```
concurrency:
group: ${{ github.workflow }}-${{ github.ref }}
cancel-in-progress: true
```

### Monitoring your current jobs in your organization or enterprise

To identify any constraints with concurrency or queuing, you can check how many jobs are currently being processed on the GitHub-hosted runners in your organization or enterprise.

## Running jobs in a container

Use a container to run the steps in a job.

Use jobs.<job_id>.container to create a container to run any steps in a job that don't already specify a container. If you have steps that use both script and container actions, the container actions will run as sibling containers on the same network with the same volume mounts.

If you do not set a container, all steps will run directly on the host specified by runs-on unless a step refers to an action configured to run in a container.

The default shell for run steps inside a container is sh instead of bash. This can be overridden with jobs.<job_id>.defaults.run or jobs.<job_id>.steps[*].shell.

### Example: Running a job within a container

```
name: CI
on:
  push:
    branches: [ main ]
jobs:
  container-test-job:
    runs-on: ubuntu-latest
    container:
      image: node:14.16
      env:
        NODE_ENV: development
      ports:
        - 80
      volumes:
        - my_docker_volume:/volume_mount
      options: --cpus 1
    steps:
      - name: Check for dockerenv file
        run: (ls /.dockerenv && echo Found dockerenv) || (echo No dockerenv)
```

When you only specify a container image, you can omit the image keyword.

```
jobs:
  container-test-job:
    runs-on: ubuntu-latest
    container: node:14.16
```

## Defining the container image

Use jobs.<job_id>.container.image to define the Docker image to use as the container to run the action. The value can be the Docker Hub image name or a registry name.

## Defining credentials for a container registry

If the image's container registry requires authentication to pull the image, you can use jobs.<job_id>.container.credentials to set a map of the username and password. The credentials are the same values that you would provide to the docker login command.

### Example: Defining credentials for a container registry

```
container:
image: ghcr.io/owner/image
credentials:
username: ${{ github.actor }}
password: ${{ secrets.github_token }}
```

## Using environment variables with a container

Use jobs.<job_id>.container.env to set a map of environment variables in the container.

## Exposing network ports on a container

Use jobs.<job_id>.container.ports to set an array of ports to expose on the container.

## Mounting volumes in a container

Use jobs.<job_id>.container.volumes to set an array of volumes for the container to use. You can use volumes to share data between services or other steps in a job. You can specify named Docker volumes, anonymous Docker volumes, or bind mounts on the host.

To specify a volume, you specify the source and destination path:

<source>:<destinationPath>.

The <source> is a volume name or an absolute path on the host machine, and <destinationPath> is an absolute path in the container.

### Example: Mounting volumes in a container

```
volumes:
  - my_docker_volume:/volume_mount
  - /data/my_data
  - /source/directory:/destination/directory
```

## Setting container resource options

Use jobs.<job_id>.container.options to configure additional Docker container resource options.

## Setting default values for jobs

Define the default settings that will apply to all jobs in the workflow, or all steps in a job.

Use defaults to create a map of default settings that will apply to all jobs in the workflow. You can also set default settings that are only available to a job.

When more than one default setting is defined with the same name, GitHub uses the most specific default setting. For example, a default setting defined in a job will override a default setting that has the same name defined in a workflow.

## Setting default shell and working directory

You can use defaults.run to provide default shell and working-directory options for all run steps in a workflow. You can also set default settings for run that are only available to a job. For more information, see jobs.<job_id>.defaults.run. You cannot use contexts or expressions in this keyword.

When more than one default setting is defined with the same name, GitHub uses the most specific default setting. For example, a default setting defined in a job will override a default setting that has the same name defined in a workflow.

## Setting default shell and working directory for a job

Use jobs.<job_id>.defaults.run to provide default shell and working-directory to all run steps in the job. Context and expression are not allowed in this section.

You can provide default shell and working-directory options for all run steps in a job. You can also set default settings for run for the entire workflow. For more information, see jobs.defaults.run. You cannot use contexts or expressions in this keyword.

When more than one default setting is defined with the same name, GitHub uses the most specific default setting. For example, a default setting defined in a job will override a default setting that has the same name defined in a workflow.

### Example: Setting default run step options for a job

```
jobs:
  job1:
    runs-on: ubuntu-latest
    defaults:
      run:
        shell: bash
        working-directory: scripts
```

### Assigning permissions to jobs

[Assigning permissions to jobs](https://docs.github.com/en/actions/using-jobs/assigning-permissions-to-jobs)

## Defining outputs for jobs

Create a map of outputs for your jobs.

You can use jobs.<job_id>.outputs to create a map of outputs for a job. Job outputs are available to all downstream jobs that depend on this job.
