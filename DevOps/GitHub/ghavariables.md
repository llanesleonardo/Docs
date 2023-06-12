Back: [Github Actions](./gha.md)

# Github Action Variables

GitHub sets default variables for each GitHub Actions workflow run. You can also set custom variables for use in a single workflow or multiple workflows.

Variables provide a way to store and reuse non-sensitive configuration information. You can store any configuration data such as compiler flags, usernames, or server names as variables. Variables are interpolated on the runner machine that runs your workflow. Commands that run in actions or workflow steps can create, read, and modify variables.

You can set your own custom variables or use the default environment variables that GitHub sets automatically.

You can set a custom variable in two ways.

- To define an environment variable for use in a single workflow, you can use the env key in the workflow file.
- To define a configuration variable across multiple workflows, you can define it at the organization, repository, or environment level.

## Defining environment variables for a single workflow

To set a custom environment variable for a single workflow, you can define it using the env key in the workflow file. The scope of a custom variable set by this method is limited to the element in which it is defined. You can define variables that are scoped for:

- The entire workflow, by using env at the top level of the workflow file.
- The contents of a job within a workflow, by using jobs.<job_id>.env.
- A specific step within a job, by using jobs.<job_id>.steps[*].env.

```
name: Greeting on variable day

on:
  workflow_dispatch

env:
  DAY_OF_WEEK: Monday

jobs:
  greeting_job:
    runs-on: ubuntu-latest
    env:
      Greeting: Hello
    steps:
      - name: "Say Hello Mona it's Monday"
        run: echo "$Greeting $First_Name. Today is $DAY_OF_WEEK!"
        env:
          First_Name: Mona
```

You can access env variable values using runner environment variables or using contexts. The example above shows three custom variables being used as environment variables in an echo command: $DAY_OF_WEEK, $Greeting, and $First_Name. The values for these variables are set, and scoped, at the workflow, job, and step level respectively.

Because runner environment variable interpolation is done after a workflow job is sent to a runner machine, you must use the appropriate syntax for the shell that's used on the runner. In this example, the workflow specifies ubuntu-latest. By default, Linux runners use the bash shell, so you must use the syntax $NAME. If the workflow specified a Windows runner, you would use the syntax for PowerShell, $env:NAME.

## Naming conventions for environment variables

When you set an environment variable, you cannot use any of the default environment variable names.

If you attempt to override the value of one of these default variables, the assignment is ignored.

Any new variables you set that point to a location on the filesystem should have a \_PATH suffix. The GITHUB_ENV and GITHUB_WORKSPACE default variables are exceptions to this convention.

You can list the entire set of environment variables that are available to a workflow step by using run: env in a step and then examining the output for the step.

## Defining configuration variables for multiple workflows

You can create configuration variables for use across multiple workflows, and can define them at either the organization, repository, or environment level.

For example, you can use configuration variables to set default values for parameters passed to build tools at an organization level, but then allow repository owners to override these parameters on a case-by-case basis.

When you define configuration variables, they are automatically available in the vars context.

## Configuration variable precedence

If a variable with the same name exists at multiple levels, the variable at the lowest level takes precedence. For example, if an organization-level variable has the same name as a repository-level variable, then the repository-level variable takes precedence. Similarly, if an organization, repository, and environment all have a variable with the same name, the environment-level variable takes precedence.

For reusable workflows, the variables from the caller workflow's repository are used. Variables from the repository that contains the called workflow are not made available to the caller workflow.

## Naming conventions for configuration variables

The following rules apply to configuration variable names:

- Names can only contain alphanumeric characters ([a-z], [A-Z], [0-9]) or underscores (\_). Spaces are not allowed.
- Names must not start with the GITHUB\_ prefix.
- Names must not start with a number.
- Names are not case-sensitive.
- Names must be unique at the level they are created at.

## Creating configuration variables for a repository

To create secrets or variables for a personal account repository, you must be the repository owner. To create secrets or variables for an organization repository, you must have admin access.

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select ... the dropdown menu, then click Settings.
3. In the "Security" section of the sidebar, select Secrets and variables, then click Actions.
4. Click the Variables tab.
5. Click New repository variable.
6. In the Name field, enter a name for your variable.
7. In the Value field, enter the value for your variable.
8. Click Add variable.

## Creating configuration variables for an enviroment

### More information

- [Creating configuration variables for an enviroment](https://docs.github.com/en/actions/learn-github-actions/variables#creating-configuration-variables-for-an-environment)

## Creating configuration variables for an organization

### More information

- [Creating configuration variables for an organization](https://docs.github.com/en/actions/learn-github-actions/variables#creating-configuration-variables-for-an-organization)

## Limits for configuration variables

Individual variables are limited to 48 KB in size.

You can store up to 1,000 organization variables, 500 variables per repository, and 100 variables per environment. The total combined size limit for organization and repository variables is 256 KB per workflow run.

A workflow created in a repository can access the following number of variables:

- Up to 500 repository variables, if the total size of repository variables is less than 256 KB. If the total size of repository variables exceeds 256 KB, only the repository variables that fall below the limit will be available (as sorted alphabetically by variable name).
- Up to 1,000 organization variables, if the total combined size of repository and organization variables is less than 256 KB. If the total combined size of organization and repository variables exceeds 256 KB, only the organization variables that fall below that limit will be available (after accounting for repository variables and as sorted alphabetically by variable name).
- Up to 100 environment-level variables.

## Using contexts to access variable values

Contexts are a way to access information about workflow runs, variables, runner environments, jobs, and steps. For more information, see "Contexts". There are many other contexts that you can use for a variety of purposes in your workflows. For details of where you can use specific contexts within a workflow, see "Contexts."

You can access environment variable values using the env context and configuration variable values using the vars context.

## Using the env context to access environment variable values

In addition to runner environment variables, GitHub Actions allows you to set and read env key values using contexts. Environment variables and contexts are intended for use at different points in the workflow.

Runner environment variables are always interpolated on the runner machine. However, parts of a workflow are processed by GitHub Actions and are not sent to the runner. You cannot use environment variables in these parts of a workflow file. Instead, you can use contexts. For example, an if conditional, which determines whether a job or step is sent to the runner, is always processed by GitHub Actions. You can use a context in an if conditional statement to access the value of an variable.

```
env:
  DAY_OF_WEEK: Monday

jobs:
  greeting_job:
    runs-on: ubuntu-latest
    env:
      Greeting: Hello
    steps:
      - name: "Say Hello Mona it's Monday"
        if: ${{ env.DAY_OF_WEEK == 'Monday' }}
        run: echo "$Greeting $First_Name. Today is $DAY_OF_WEEK!"
        env:
          First_Name: Monas
```

In this modification of the earlier example, we've introduced an if conditional. The workflow step is now only run if DAY_OF_WEEK is set to "Monday". We access this value from the if conditional statement by using the env context.

Contexts are usually denoted using the dollar sign and curly braces, as ${{ context.property }}. In an if conditional, the ${{ and }} are optional, but if you use them they must enclose the entire comparison statement, as shown above.

You will commonly use either the env or github context to access variable values in parts of the workflow that are processed before jobs are sent to runners.

## Using the vars context to access configuration variable values

Configuration variables can be accessed across the workflow using vars context. For more information, see "Contexts".

If a configuration variable has not been set, the return value of a context referencing the variable will be an empty string.

The following example shows using configuration variables with the vars context across a workflow. Each of the following configuration variables have been defined at the repository, organization, or environment levels.

```
on:
  workflow_dispatch:
env:
  # Setting an environment variable with the value of a configuration variable
  env_var: ${{ vars.ENV_CONTEXT_VAR }}

jobs:
  display-variables:
    name: ${{ vars.JOB_NAME }}
    # You can use configuration variables with the `vars` context for dynamic jobs
    if: ${{ vars.USE_VARIABLES == 'true' }}
    runs-on: ${{ vars.RUNNER }}
    environment: ${{ vars.ENVIRONMENT_STAGE }}
    steps:
    - name: Use variables
      run: |
        echo "repository variable : $REPOSITORY_VAR"
        echo "organization variable : $ORGANIZATION_VAR"
        echo "overridden variable : $OVERRIDE_VAR"
        echo "variable from shell environment : $env_var"
      env:
        REPOSITORY_VAR: ${{ vars.REPOSITORY_VAR }}
        ORGANIZATION_VAR: ${{ vars.ORGANIZATION_VAR }}
        OVERRIDE_VAR: ${{ vars.OVERRIDE_VAR }}

    - name: ${{ vars.HELLO_WORLD_STEP }}
      if: ${{ vars.HELLO_WORLD_ENABLED == 'true' }}
      uses: actions/hello-world-javascript-action@main
      with:
        who-to-greet: ${{ vars.GREET_NAME }}
```

## Default enviromental variables

### More information

- [Default enviromental variables](https://docs.github.com/en/actions/learn-github-actions/variables#default-environment-variables)

## Detecting the operating system

You can write a single workflow file that can be used for different operating systems by using the RUNNER_OS default environment variable and the corresponding context property ${{ runner.os }}. For example, the following workflow could be run successfully if you changed the operating system from macos-latest to windows-latest without having to alter the syntax of the environment variables, which differs depending on the shell being used by the runner.

In this example, the two if statements check the os property of the runner context to determine the operating system of the runner. if conditionals are processed by GitHub Actions, and only steps where the check resolves as true are sent to the runner. Here one of the checks will always be true and the other false, so only one of these steps is sent to the runner. Once the job is sent to the runner, the step is executed and the environment variable in the echo command is interpolated using the appropriate syntax ($env:NAME for PowerShell on Windows, and $NAME for bash and sh on Linux and MacOS). In this example, the statement runs-on: macos-latest means that the second step will be run.

## Passing values between steps and jobs in a workflow

If you generate a value in one step of a job, you can use the value in subsequent steps of the same job by assigning the value to an existing or new environment variable and then writing this to the GITHUB_ENV environment file. The environment file can be used directly by an action, or from a shell command in the workflow file by using the run keyword.

If you want to pass a value from a step in one job in a workflow to a step in another job in the workflow, you can define the value as a job output. You can then reference this job output from a step in another job.

## Workflow billing & Limits

### More information

- [Workflow billing & Limits](https://docs.github.com/en/actions/learn-github-actions/usage-limits-billing-and-administration)
