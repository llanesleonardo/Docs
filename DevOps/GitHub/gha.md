Back: [Table contents](./1-tablecontent.md)

# Github Actions

## Understanding GitHub Actions

---

Learn the basics of GitHub Actions, including core concepts and essential terminology.

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. You can create workflows that build and test every pull request to your repository, or deploy merged pull requests to production.

GitHub Actions goes beyond just DevOps and lets you run workflows when other events happen in your repository. For example, you can run a workflow to automatically add the appropriate labels whenever someone creates a new issue in your repository.

GitHub provides Linux, Windows, and macOS virtual machines to run your workflows, or you can host your own self-hosted runners in your own data center or cloud infrastructure.

## The components of GitHub Actions

---

You can configure a GitHub Actions workflow to be triggered when an event occurs in your repository, such as a pull request being opened or an issue being created. Your workflow contains one or more jobs which can run in sequential order or in parallel. Each job will run inside its own virtual machine runner, or inside a container, and has one or more steps that either run a script that you define or run an action, which is a reusable extension that can simplify your workflow.

### More information

- [Components](https://docs.github.com/assets/cb-25535/mw-1440/images/help/actions/overview-actions-simple.webp)

## Workflows

---

A workflow is a configurable automated process that will run one or more jobs. Workflows are defined by a YAML file checked in to your repository and will run when triggered by an event in your repository, or they can be triggered manually, or at a defined schedule.

Workflows are defined in the .github/workflows directory in a repository, and a repository can have multiple workflows, each of which can perform a different set of tasks. For example, you can have one workflow to build and test pull requests, another workflow to deploy your application every time a release is created, and still another workflow that adds a label every time someone opens a new issue.

You can reference a workflow within another workflow.

## Events

---

An event is a specific activity in a repository that triggers a workflow run. For example, activity can originate from GitHub when someone creates a pull request, opens an issue, or pushes a commit to a repository. You can also trigger a workflow to run on a schedule, by posting to a REST API, or manually.

### More information

- [Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

## Jobs

---

A job is a set of steps in a workflow that is executed on the same runner. Each step is either a shell script that will be executed, or an action that will be run. Steps are executed in order and are dependent on each other. Since each step is executed on the same runner, you can share data from one step to another. For example, you can have a step that builds your application followed by a step that tests the application that was built.

You can configure a job's dependencies with other jobs; by default, jobs have no dependencies and run in parallel with each other. When a job takes a dependency on another job, it will wait for the dependent job to complete before it can run. For example, you may have multiple build jobs for different architectures that have no dependencies, and a packaging job that is dependent on those jobs. The build jobs will run in parallel, and when they have all completed successfully, the packaging job will run.

### More information

- [Using Jobs](https://docs.github.com/en/actions/using-jobs)

## Actions

---

An action is a custom application for the GitHub Actions platform that performs a complex but frequently repeated task. Use an action to help reduce the amount of repetitive code that you write in your workflow files. An action can pull your git repository from GitHub, set up the correct toolchain for your build environment, or set up the authentication to your cloud provider.

You can write your own actions, or you can find actions to use in your workflows in the GitHub Marketplace.

## Runners

---

A runner is a server that runs your workflows when they're triggered. Each runner can run a single job at a time. GitHub provides Ubuntu Linux, Microsoft Windows, and macOS runners to run your workflows; each workflow run executes in a fresh, newly-provisioned virtual machine. GitHub also offers larger runners, which are available in larger configurations.

## Creating and example workflow

---

GitHub Actions uses YAML syntax to define the workflow. Each workflow is stored as a separate YAML file in your code repository, in a directory named .github/workflows.

You can create an example workflow in your repository that automatically triggers a series of commands whenever code is pushed. In this workflow, GitHub Actions checks out the pushed code, installs the bats testing framework, and runs a basic command to output the bats version: bats -v.

### Process' checklist

1. In your repository, create the .github/workflows/ directory to store your workflow files.
2. In the .github/workflows/ directory, create a new file called learn-github-actions.yml and add the following code.

YAML

```
name: learn-github-actions
run-name: $ github.actor  is learning GitHub Actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
```

3. Commit these changes and push them to your GitHub repository.

Your new GitHub Actions workflow file is now installed in your repository and will run automatically each time someone pushes a change to the repository.

## Understading a workflow file

---

### More information

- [Understading a workflow file](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#understanding-the-workflow-file)

## Visualizing the workflow file

---

In this diagram, you can see the workflow file you just created and how the GitHub Actions components are organized in a hierarchy. Each step executes a single action or shell script. Steps 1 and 2 run actions, while steps 3 and 4 run shell scripts.

### More information

- [Github action Job](https://docs.github.com/assets/cb-33882/mw-1440/images/help/actions/overview-actions-event.webp)

## Viewing the activity for a workflow run

---

When your workflow is triggered, a workflow run is created that executes the workflow. After a workflow run has started, you can see a visualization graph of the run's progress and view each step's activity on GitHub.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Actions.
3. In the left sidebar, click the workflow you want to see.
4. From the list of workflow runs, click the name of the run to see the workflow run summary.
5. In the left sidebar or in the visualization graph, click the job you want to see.
6. To view the results of a step, click the step.

## Finding and customizing actions

---

Actions are the building blocks that power your workflow. A workflow can contain actions created by the community, or you can create your own actions directly within your application's repository. This guide will show you how to discover, use, and customize actions.

The actions you use in your workflow can be defined in:

The same repository as your workflow file
Any public repository
A published Docker container image on Docker Hub
GitHub Marketplace is a central location for you to find actions created by the GitHub community.

### More information

- [Github marketplace](https://github.com/marketplace?type=actions)

## Browsing Marketplace actions in the workflow editor

---

You can search and browse actions directly in your repository's workflow editor. From the sidebar, you can search for a specific action, view featured actions, and browse featured categories. You can also view the number of stars an action has received from the GitHub community.

### Process' checklist

1. In your repository, browse to the workflow file you want to edit.
2. In the upper right corner of the file view, to open the workflow editor, click (edit icon).
3. To the right of the editor, use the GitHub Marketplace sidebar to browse actions. Actions with the badge indicate GitHub has verified the creator of the action as a partner organization.

## Adding an action to your workflow

---

You can add an action to your workflow by referencing the action in your workflow file.

You can view the actions referenced in your GitHub Actions workflows as dependencies in the dependency graph of the repository containing your workflows.

## Adding an action from GitHub Marketplace

---

An action's listing page includes the action's version and the workflow syntax required to use the action. To keep your workflow stable even when updates are made to an action, you can reference the version of the action to use by specifying the Git or Docker tag number in your workflow file.

### Process' checklist

1. Navigate to the action you want to use in your workflow.
2. Click to view the full marketplace listing for the action.
3. Under "Installation", click copy the workflow syntax.
4. Paste the syntax as a new step in your workflow.
5. If the action requires you to provide inputs, set them in your workflow.

You can also enable Dependabot version updates for the actions that you add to your workflow.

## Adding an action from the same repository

---

If an action is defined in the same repository where your workflow file uses the action, you can reference the action with either the ‌{owner}/{repo}@{ref} or ./path/to/dir syntax in your workflow file.

Example repository file structure:

```
|-- hello-world (repository)
|   |__ .github
|       └── workflows
|           └── my-first-workflow.yml
|       └── actions
|           |__ hello-world-action
|               └── action.yml
```

Example workflow file:

```
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # This step checks out a copy of your repository.
      - uses: actions/checkout@v3
      # This step references the directory that contains the action.
      - uses: ./.github/actions/hello-world-action
```

The action.yml file is used to provide metadata for the action.

## Adding an action from a different repository

---

If an action is defined in a different repository than your workflow file, you can reference the action with the {owner}/{repo}@{ref} syntax in your workflow file.

The action must be stored in a public repository.

```
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: actions/setup-node@v3
```

## Referencing a container on Docker Hub

---

If an action is defined in a published Docker container image on Docker Hub, you must reference the action with the docker://{image}:{tag} syntax in your workflow file. To protect your code and data, we strongly recommend you verify the integrity of the Docker container image from Docker Hub before using it in your workflow.

```
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: docker://alpine:3.8
```

### More information

- [Docker Action example](https://github.com/actions/starter-workflows/blob/main/ci/docker-image.yml)

## Using release management for your custom actions

---

The creators of a community action have the option to use tags, branches, or SHA values to manage releases of the action. Similar to any dependency, you should indicate the version of the action you'd like to use based on your comfort with automatically accepting updates to the action.

You will designate the version of the action in your workflow file. Check the action's documentation for information on their approach to release management, and to see which tag, branch, or SHA value to use.

## Using tags

---

Tags are useful for letting you decide when to switch between major and minor versions, but these are more ephemeral and can be moved or deleted by the maintainer. This example demonstrates how to target an action that's been tagged as v1.0.1:

```
steps:
  - uses: actions/javascript-action@v1.0.1

```

## Using SHAs

---

If you need more reliable versioning, you should use the SHA value associated with the version of the action. SHAs are immutable and therefore more reliable than tags or branches. However, this approach means you will not automatically receive updates for an action, including important bug fixes and security updates. You must use a commit's full SHA value, and not an abbreviated value. When selecting a SHA, you should verify it is from the action's repository and not a repository fork. This example targets an action's SHA:

```
steps:
  - uses: actions/javascript-action@a824008085750b8e136effc585c3cd6082bd575f
```

## Using branches

---

Specifying a target branch for the action means it will always run the version currently on that branch. This approach can create problems if an update to the branch includes breaking changes. This example targets a branch named @main:

```
steps:
  - uses: actions/javascript-action@main
```

## Using inputs and outputs with an action

---

An action often accepts or requires inputs and generates outputs that you can use. For example, an action might require you to specify a path to a file, the name of a label, or other data it will use as part of the action processing.

To see the inputs and outputs of an action, check the action.yml or action.yaml in the root directory of the repository.

In this example action.yml, the inputs keyword defines a required input called file-path, and includes a default value that will be used if none is specified. The outputs keyword defines an output called results-file, which tells you where to locate the results.

```
name: "Example"
description: "Receives file and generates output"
inputs:
  file-path: # id of input
    description: "Path to test script"
    required: true
    default: "test-file.js"
outputs:
  results-file: # id of output
    description: "Path to results file"
```

## Essential features of GitHub Actions

---

GitHub Actions are designed to help you build robust and dynamic automations. This guide will show you how to craft GitHub Actions workflows that include environment variables, customized scripts, and more.

GitHub Actions allow you to customize your workflows to meet the unique needs of your application and team. In this guide, we'll discuss some of the essential customization techniques such as using variables, running scripts, and sharing data and artifacts between jobs.

## Using variables in your workflows

---

GitHub Actions include default environment variables for each workflow run. If you need to use custom environment variables, you can set these in your YAML workflow file. This example demonstrates how to create custom variables named POSTGRES_HOST and POSTGRES_PORT. These variables are then available to the node client.js script.

```
jobs:
  example-job:
      steps:
        - name: Connect to PostgreSQL
          run: node client.js
          env:
            POSTGRES_HOST: postgres
            POSTGRES_PORT: 5432
```

## Adding scripts to your workflow

---

You can use actions to run scripts and shell commands, which are then executed on the assigned runner. This example demonstrates how an action can use the run keyword to execute npm install -g bats on the runner.

```
jobs:
  example-job:
    steps:
      - run: npm install -g bats
```

For example, to run a script as an action, you can store the script in your repository and supply the path and shell type.

```
jobs:
  example-job:
    steps:
      - name: Run build script
        run: ./.github/scripts/build.sh
        shell: bash
```

## Sharing data between jobs

---

If your job generates files that you want to share with another job in the same workflow, or if you want to save the files for later reference, you can store them in GitHub as artifacts. Artifacts are the files created when you build and test your code. For example, artifacts might include binary or package files, test results, screenshots, or log files. Artifacts are associated with the workflow run where they were created and can be used by another job. All actions and workflows called within a run have write access to that run's artifacts.

For example, you can create a file and then upload it as an artifact.

```
jobs:
  example-job:
    name: Save output
    steps:
      - shell: bash
        run: |
          expr 1 + 1 > output.log
      - name: Upload output file
        uses: actions/upload-artifact@v3
        with:
          name: output-log-file
          path: output.log
```

To download an artifact from a separate workflow run, you can use the actions/download-artifact action. For example, you can download the artifact named output-log-file.

```
jobs:
  example-job:
    steps:
      - name: Download a single artifact
        uses: actions/download-artifact@v3
        with:
          name: output-log-file
```

To download an artifact from the same workflow run, your download job should specify needs: upload-job-name so it doesn't start until the upload job finishes.

## Expresions

---

You can evaluate expressions in workflows and actions.

You can use expressions to programmatically set environment variables in workflow files and access contexts. An expression can be any combination of literal values, references to a context, or functions. You can combine literals, context references, and functions using operators.

Expressions are commonly used with the conditional if keyword in a workflow file to determine whether a step should run. When an if conditional is true, the step will run.

You need to use specific syntax to tell GitHub to evaluate an expression rather than treat it as a string.

```
'$ <expression> '

```

When you use expressions in an if conditional, you may omit the expression syntax ('$ ') because GitHub automatically evaluates the if conditional as an expression.

## Example expression in an if conditional

---

```
steps:
  - uses: actions/hello-world-javascript-action@e76147da8e5c81eaf017dede5645551d4b94427b
    if: '$ <expression> '
```

```
Example setting an environment variable
env:
  MY_ENV_VAR: '$ <expression> '
```

## Literals

---

As part of an expression, you can use boolean, null, number, or string data types.

### More information

- [Literals](https://docs.github.com/en/actions/learn-github-actions/expressions#literals)

```
env:
  myNull: '$ null '
  myBoolean: '$ false '
  myIntegerNumber: '$ 711 '
  myFloatNumber: '$ -9.2 '
  myHexNumber: '$ 0xff '
  myExponentialNumber: '$ -2.99e-2 '
  myString: Mona the Octocat
  myStringInBraces: '$ 'It''s open source!' '
```

## Operators

---

### More information

- [Operators](https://docs.github.com/en/actions/learn-github-actions/expressions#operators)

## Functions

---

### More information

- [Functions](https://docs.github.com/en/actions/learn-github-actions/expressions#functions)

## Contexts

---

You can access context information in workflows and actions.
Contexts are a way to access information about workflow runs, variables, runner environments, jobs, and steps. Each context is an object that contains properties, which can be strings or other objects.

Contexts, objects, and properties will vary significantly under different workflow run conditions.

You can access contexts using the expression syntax.

```
'$ <context> '

```

### More information

- [List of context variables](https://docs.github.com/en/actions/learn-github-actions/contexts)

As part of an expression, you can access context information using one of two syntaxes.

- Index syntax: github['sha']
- Property dereference syntax: github.sha
  In order to use property dereference syntax, the property name must start with a letter or _ and contain only alphanumeric characters, -, or _.

If you attempt to dereference a non-existent property, it will evaluate to an empty string.

## Determining when to use contexts

---

GitHub Actions includes a collection of variables called contexts and a similar collection of variables called default variables. These variables are intended for use at different points in the workflow:

- Default environment variables: These environment variables exist only on the runner that is executing your job.
- Contexts: You can use most contexts at any point in your workflow, including when default variables would be unavailable. For example, you can use contexts with expressions to perform initial processing before the job is routed to a runner for execution; this allows you to use a context with the conditional if keyword to determine whether a step should run. Once the job is running, you can also retrieve context variables from the runner that is executing the job, such as runner.os.

The following example demonstrates how these different types of variables can be used together in a job:

```
name: CI
on: push
jobs:
  prod-check:
    if: '$ github.ref == 'refs/heads/main' '
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying to production server on branch $GITHUB_REF"
```

In this example, the if statement checks the github.ref context to determine the current branch name; if the name is refs/heads/main, then the subsequent steps are executed. The if check is processed by GitHub Actions, and the job is only sent to the runner if the result is true. Once the job is sent to the runner, the step is executed and refers to the $GITHUB_REF variable from the runner.

## Context availability

---

Different contexts are available throughout a workflow run. For example, the secrets context may only be used at certain places within a job.

In addition, some functions may only be used in certain places. For example, the hashFiles function is not available everywhere.

The following table indicates where each context and special function can be used within a workflow. Unless listed below, a function can be used anywhere.

### More information

- [Content available Workflow key](https://docs.github.com/en/actions/learn-github-actions/contexts#context-availability)

## Example: printing context information to the log

---

You can print the contents of contexts to the log for debugging. The toJSON function is required to pretty-print JSON objects to the log.

YAML

```
name: Context testing
on: push

jobs:
  dump_contexts_to_log:
    runs-on: ubuntu-latest
    steps:
      - name: Dump GitHub context
        id: github_context_step
        run: echo '$ toJSON(github) '
      - name: Dump job context
        run: echo '$ toJSON(job) '
      - name: Dump steps context
        run: echo '$ toJSON(steps) '
      - name: Dump runner context
        run: echo '$ toJSON(runner) '
      - name: Dump strategy context
        run: echo '$ toJSON(strategy) '
      - name: Dump matrix context
        run: echo '$ toJSON(matrix) '
```

## github context

---

The github context contains information about the workflow run and the event that triggered the run. You can also read most of the github context data in environment variables.

### More information

- [Github context- property](https://docs.github.com/en/actions/learn-github-actions/contexts#github-context)

## Example contents of the github context

---

The following example context is from a workflow run triggered by the push event. The event object in this example has been truncated because it is identical to the contents of the push webhook payload.

```
{
  "token": "***",
  "job": "dump_contexts_to_log",
  "ref": "refs/heads/my_branch",
  "sha": "c27d339ee6075c1f744c5d4b200f7901aad2c369",
  "repository": "octocat/hello-world",
  "repository_owner": "octocat",
  "repositoryUrl": "git://github.com/octocat/hello-world.git",
  "run_id": "1536140711",
  "run_number": "314",
  "retention_days": "90",
  "run_attempt": "1",
  "actor": "octocat",
  "workflow": "Context testing",
  "head_ref": "",
  "base_ref": "",
  "event_name": "push",
  "event": {
    ...
  },
  "server_url": "https://github.com",
  "api_url": "https://api.github.com",
  "graphql_url": "https://api.github.com/graphql",
  "ref_name": "my_branch",
  "ref_protected": false,
  "ref_type": "branch",
  "secret_source": "Actions",
  "workspace": "/home/runner/work/hello-world/hello-world",
  "action": "github_step",
  "event_path": "/home/runner/work/_temp/_github_workflow/event.json",
  "action_repository": "",
  "action_ref": "",
  "path": "/home/runner/work/_temp/_runner_file_commands/add_path_b037e7b5-1c88-48e2-bf78-eaaab5e02602",
  "env": "/home/runner/work/_temp/_runner_file_commands/set_env_b037e7b5-1c88-48e2-bf78-eaaab5e02602"
}
```

## Example usage of the github context

---

This example workflow uses the github.event_name context to run a job only if the workflow run was triggered by the pull_request event.

```
name: Run CI
on: [push, pull_request]

jobs:
  normal_ci:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run normal CI
        run: ./run-tests

  pull_request_ci:
    runs-on: ubuntu-latest
    if: '$ github.event_name == 'pull_request' '
    steps:
      - uses: actions/checkout@v3
      - name: Run PR CI
        run: ./run-additional-pr-ci
```

## env context

---

The env context contains variables that have been set in a workflow, job, or step. For more information about setting variables in your workflow, see "Workflow syntax for GitHub Actions."

The env context syntax allows you to use the value of a variable in your workflow file. You can use the env context in the value of any key in a step except for the id and uses keys. For more information on the step syntax, see "Workflow syntax for GitHub Actions."

If you want to use the value of a variable inside a runner, use the runner operating system's normal method for reading environment variables.

### More information

- [Env context](https://docs.github.com/en/actions/learn-github-actions/contexts#env-context)

## Example contents of the env context

---

The contents of the env context is a mapping of variable names to their values. The context's contents can change depending on where it is used in the workflow run.

```
{
"first_name": "Mona",
"super_duper_var": "totally_awesome"
}
```

## Example usage of the env context

---

This example workflow shows how the env context can be configured at the workflow, job, and step levels, as well as using the context in steps.

When more than one environment variable is defined with the same name, GitHub uses the most specific variable. For example, an environment variable defined in a step will override job and workflow environment variables with the same name, while the step executes. An environment variable defined for a job will override a workflow variable with the same name, while the job executes.

```
name: Hi Mascot
on: push
env:
  mascot: Mona
  super_duper_var: totally_awesome

jobs:
  windows_job:
    runs-on: windows-latest
    steps:
      - run: echo 'Hi $ env.mascot '  # Hi Mona
      - run: echo 'Hi $ env.mascot '  # Hi Octocat
        env:
          mascot: Octocat
  linux_job:
    runs-on: ubuntu-latest
    env:
      mascot: Tux
    steps:
      - run: echo 'Hi $ env.mascot '  # Hi Tux

```

## Example contents of the github context

---

The following example context is from a workflow run triggered by the push event. The event object in this example has been truncated because it is identical to the contents of the push webhook payload.

```
{
  "token": "***",
  "job": "dump_contexts_to_log",
  "ref": "refs/heads/my_branch",
  "sha": "c27d339ee6075c1f744c5d4b200f7901aad2c369",
  "repository": "octocat/hello-world",
  "repository_owner": "octocat",
  "repositoryUrl": "git://github.com/octocat/hello-world.git",
  "run_id": "1536140711",
  "run_number": "314",
  "retention_days": "90",
  "run_attempt": "1",
  "actor": "octocat",
  "workflow": "Context testing",
  "head_ref": "",
  "base_ref": "",
  "event_name": "push",
  "event": {
    ...
  },
  "server_url": "https://github.com",
  "api_url": "https://api.github.com",
  "graphql_url": "https://api.github.com/graphql",
  "ref_name": "my_branch",
  "ref_protected": false,
  "ref_type": "branch",
  "secret_source": "Actions",
  "workspace": "/home/runner/work/hello-world/hello-world",
  "action": "github_step",
  "event_path": "/home/runner/work/_temp/_github_workflow/event.json",
  "action_repository": "",
  "action_ref": "",
  "path": "/home/runner/work/_temp/_runner_file_commands/add_path_b037e7b5-1c88-48e2-bf78-eaaab5e02602",
  "env": "/home/runner/work/_temp/_runner_file_commands/set_env_b037e7b5-1c88-48e2-bf78-eaaab5e02602"
}

```

## Example usage of the github context

---

This example workflow uses the github.event_name context to run a job only if the workflow run was triggered by the pull_request event.

```
name: Run CI
on: [push, pull_request]

jobs:
  normal_ci:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run normal CI
        run: ./run-tests

  pull_request_ci:
    runs-on: ubuntu-latest
    if: '$ github.event_name == 'pull_request' '
    steps:
      - uses: actions/checkout@v3
      - name: Run PR CI
        run: ./run-additional-pr-ci
```

## env context

---

The env context contains variables that have been set in a workflow, job, or step.

The env context syntax allows you to use the value of a variable in your workflow file. You can use the env context in the value of any key in a step except for the id and uses keys.

If you want to use the value of a variable inside a runner, use the runner operating system's normal method for reading environment variables.

## Example contents of the env context

---

The contents of the env context is a mapping of variable names to their values. The context's contents can change depending on where it is used in the workflow run.

```
{
"first_name": "Mona",
"super_duper_var": "totally_awesome"
}
```

## Example usage of the env context

---

This example workflow shows how the env context can be configured at the workflow, job, and step levels, as well as using the context in steps.

When more than one environment variable is defined with the same name, GitHub uses the most specific variable. For example, an environment variable defined in a step will override job and workflow environment variables with the same name, while the step executes. An environment variable defined for a job will override a workflow variable with the same name, while the job executes.

```
name: Hi Mascot
on: push
env:
  mascot: Mona
  super_duper_var: totally_awesome

jobs:
  windows_job:
    runs-on: windows-latest
    steps:
      - run: echo 'Hi $ env.mascot '  # Hi Mona
      - run: echo 'Hi $ env.mascot '  # Hi Octocat
        env:
          mascot: Octocat
  linux_job:
    runs-on: ubuntu-latest
    env:
      mascot: Tux
    steps:
      - run: echo 'Hi $ env.mascot '  # Hi Tux
```

## vars context

---

Note: Configuration variables for GitHub Actions are in beta and subject to change.

The vars context contains custom configuration variables set at the organization, repository, and environment levels.

## Example contents of the vars context

---

The contents of the vars context is a mapping of configuration variable names to their values.

```
{
"mascot": "Mona"
}
```

## Example usage of the vars context

---

This example workflow shows how configuration variables set at the repository, environment, or organization levels are automatically available using the vars context.

If a configuration variable has not been set, the return value of a context referencing the variable will be an empty string.

The following example shows using configuration variables with the vars context across a workflow. Each of the following configuration variables have been defined at the repository, organization, or environment levels.

```
on:
  workflow_dispatch:
env:
  # Setting an environment variable with the value of a configuration variable
  env_var: '$ vars.ENV_CONTEXT_VAR '

jobs:
  display-variables:
    name: '$ vars.JOB_NAME '
    # You can use configuration variables with the `vars` context for dynamic jobs
    if: '$ vars.USE_VARIABLES == 'true' '
    runs-on: '$ vars.RUNNER '
    environment: '$ vars.ENVIRONMENT_STAGE '
    steps:
    - name: Use variables
      run: |
        echo "repository variable : $REPOSITORY_VAR"
        echo "organization variable : $ORGANIZATION_VAR"
        echo "overridden variable : $OVERRIDE_VAR"
        echo "variable from shell environment : $env_var"
      env:
        REPOSITORY_VAR: '$ vars.REPOSITORY_VAR '
        ORGANIZATION_VAR: '$ vars.ORGANIZATION_VAR '
        OVERRIDE_VAR: '$ vars.OVERRIDE_VAR '

    - name:'$ vars.HELLO_WORLD_STEP '
      if: '$ vars.HELLO_WORLD_ENABLED == 'true' '
      uses: actions/hello-world-javascript-action@main
      with:
        who-to-greet: '$ vars.GREET_NAME '

```

## Job context

### More information

- [Job Context](https://docs.github.com/en/actions/learn-github-actions/contexts#job-context)

## Example contents of the job context

---

This example job context uses a PostgreSQL service container with mapped ports. If there are no containers or service containers used in a job, the job context only contains the status property.

```
{
  "status": "success",
  "container": {
    "network": "github_network_53269bd575974817b43f4733536b200c"
  },
  "services": {
    "postgres": {
      "id": "60972d9aa486605e66b0dad4abb638dc3d9116f566579e418166eedb8abb9105",
      "ports": {
        "5432": "49153"
      },
      "network": "github_network_53269bd575974817b43f4733536b200c"
    }
  }
}
```

## Example usage of the job context

---

This example workflow configures a PostgreSQL service container, and automatically maps port 5432 in the service container to a randomly chosen available port on the host. The job context is used to access the number of the port that was assigned on the host.

```
name: PostgreSQL Service Example
on: push
jobs:
  postgres-job:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres
        env:
          POSTGRES_PASSWORD: postgres
        options: --health-cmd pg_isready --health-interval 10s --health-timeout 5s --health-retries 5
        ports:
          # Maps TCP port 5432 in the service container to a randomly chosen available port on the host.
          - 5432

    steps:
      - uses: actions/checkout@v3
      - run: pg_isready -h localhost -p '$ job.services.postgres.ports[5432] '
      - run: ./run-tests
```

## jobs context

---

### More information

- [Jobs context](https://docs.github.com/en/actions/learn-github-actions/contexts#jobs-context)

## Example contents of the jobs context

---

This example jobs context contains the result and outputs of a job from a reusable workflow run.

```
{
  "example_job": {
    "result": "success",
    "outputs": {
      "output1": "hello",
      "output2": "world"
    }
  }
}
```

## Example usage of the jobs context

---

This example reusable workflow uses the jobs context to set outputs for the reusable workflow. Note how the outputs flow up from the steps, to the job, then to the workflow_call trigger.

```
name: Reusable workflow

on:
  workflow_call:
    # Map the workflow outputs to job outputs
    outputs:
      firstword:
        description: "The first output string"
        value: '$ jobs.example_job.outputs.output1 '
      secondword:
        description: "The second output string"
        value: '$ jobs.example_job.outputs.output2 '

jobs:
  example_job:
    name: Generate output
    runs-on: ubuntu-latest
    # Map the job outputs to step outputs
    outputs:
      output1: '$ steps.step1.outputs.firstword '
      output2: '$ steps.step2.outputs.secondword '
    steps:
      - id: step1
        run: echo "firstword=hello" >> $GITHUB_OUTPUT
      - id: step2
        run: echo "secondword=world" >> $GITHUB_OUTPUT
```

## steps context

---

### More information

- [Steps context](https://docs.github.com/en/actions/learn-github-actions/contexts#steps-context)

## Example contents of the steps context

---

This example steps context shows two previous steps that had an id specified. The first step had the id named checkout, the second generate_number. The generate_number step had an output named random_number.

```
{
  "checkout": {
    "outputs": {},
    "outcome": "success",
    "conclusion": "success"
  },
  "generate_number": {
    "outputs": {
      "random_number": "1"
    },
    "outcome": "success",
    "conclusion": "success"
  }
}
```

## Example usage of the steps context

---

This example workflow generates a random number as an output in one step, and a later step uses the steps context to read the value of that output.

```
name: Generate random failure
on: push
jobs:
  randomly-failing-job:
    runs-on: ubuntu-latest
    steps:
      - id: checkout
        uses: actions/checkout@v3
      - name: Generate 0 or 1
        id: generate_number
        run:  echo "random_number=$(($RANDOM % 2))" >> $GITHUB_OUTPUT
      - name: Pass or fail
        run: |
          if [[ '$ steps.generate_number.outputs.random_number ' == 0 ]]; then exit 0; else exit 1; fi
```

## runner context

---

### More information

- [runner context](https://docs.github.com/en/actions/learn-github-actions/contexts#runner-context)

## Example contents of the runner context

---

The following example context is from a Linux GitHub-hosted runner.

```
{
"os": "Linux",
"arch": "X64",
"name": "GitHub Actions 2",
"tool_cache": "/opt/hostedtoolcache",
"temp": "/home/runner/work/\_temp"
}
```

## Example usage of the runner context

---

This example workflow uses the runner context to set the path to the temporary directory to write logs, and if the workflow fails, it uploads those logs as artifact.

```
name: Build
on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build with logs
        run: |
          mkdir '$ runner.temp '/build_logs
          ./build.sh --log-path '$ runner.temp '/build_logs
      - name: Upload logs on fail
        if: '$ failure() '
        uses: actions/upload-artifact@v3
        with:
          name: Build failure logs
          path: '$ runner.temp '/build_logs
```

## secrets context

---

The secrets context contains the names and values of secrets that are available to a workflow run. The secrets context is not available for composite actions due to security reasons. If you want to pass a secret to a composite action, you need to do it explicitly as an input.

GITHUB_TOKEN is a secret that is automatically created for every workflow run, and is always included in the secrets context.

### More information

- [secrets context](https://docs.github.com/en/actions/learn-github-actions/contexts#secrets-context)

## Example contents of the secrets context

---

The following example contents of the secrets context shows the automatic GITHUB_TOKEN, as well as two other secrets available to the workflow run.

```
{
"github_token": "**_",
"NPM_TOKEN": "_**",
"SUPERSECRET": "\*\*\*"
}
```

## Example usage of the secrets context

---

This example workflow uses the labeler action, which requires the GITHUB_TOKEN as the value for the repo-token input parameter:

```
name: Pull request labeler
on: [ pull_request_target ]

jobs:
  triage:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    steps:
      - uses: actions/labeler@v4
        with:
          repo-token: '$ secrets.GITHUB_TOKEN '
```

## strategy context

---

### More information

- [strategy context](https://docs.github.com/en/actions/learn-github-actions/contexts#strategy-context)

## Example contents of the strategy context

---

The following example contents of the strategy context is from a matrix with four jobs, and is taken from the final job. Note the difference between the zero-based job-index number, and job-total which is not zero-based.

```
{
"fail-fast": true,
"job-index": 3,
"job-total": 4,
"max-parallel": 4
}
```

## Example usage of the strategy context

---

This example workflow uses the strategy.job-index property to set a unique name for a log file for each job in a matrix.

```
name: Test matrix
on: push

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        test-group: [1, 2]
        node: [14, 16]
    steps:
      - uses: actions/checkout@v3
      - run: npm test > test-job-$' strategy.job-index '.txt
      - name: Upload logs
        uses: actions/upload-artifact@v3
        with:
          name: Build log for job '$ strategy.job-index '
          path: test-job-'$ strategy.job-index '.txt
```

## matrix context

---

### More information

- [matrix context](https://docs.github.com/en/actions/learn-github-actions/contexts#matrix-context)

## Example contents of the matrix context

---

The following example contents of the matrix context is from a job in a matrix that has the os and node matrix properties defined in the workflow. The job is executing the matrix combination of an ubuntu-latest OS and Node.js version 16.

```
{
"os": "ubuntu-latest",
"node": 16
}
```

## Example usage of the matrix context

---

This example workflow creates a matrix with os and node keys. It uses the matrix.os property to set the runner type for each job, and uses the matrix.node property to set the Node.js version for each job.

```
name: Test matrix
on: push

jobs:
  build:
    runs-on: '$ matrix.os '
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest]
        node: [14, 16]
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '$ matrix.node '
      - name: Install dependencies
        run: npm ci
      - name: Run tests
        run: npm test
```

## needs context

---

### More information

- [needs context](https://docs.github.com/en/actions/learn-github-actions/contexts#needs-context)

## Example contents of the needs context

---

The following example contents of the needs context shows information for two jobs that the current job depends on.

```
{
"build": {
"result": "success",
"outputs": {
"build_id": "ABC123"
}
},
"deploy": {
"result": "failure",
"outputs": {}
}
}
```

## Example usage of the needs context

---

This example workflow has three jobs: a build job that does a build, a deploy job that requires the build job, and a debug job that requires both the build and deploy jobs and runs only if there is a failure in the workflow. The deploy job also uses the needs context to access an output from the build job.

```
name: Build and deploy
on: push

jobs:
  build:
    runs-on: ubuntu-latest
    outputs:
      build_id: '$ steps.build_step.outputs.build_id '
    steps:
      - uses: actions/checkout@v3
      - name: Build
        id: build_step
        run: |
          ./build
          echo "build_id=$BUILD_ID" >> $GITHUB_OUTPUT
  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: ./deploy --build '$ needs.build.outputs.build_id '
  debug:
    needs: [build, deploy]
    runs-on: ubuntu-latest
    if: '$ failure() '
    steps:
      - uses: actions/checkout@v3
      - run: ./debug
```

## inputs context

---

### More information

- [inputs context](https://docs.github.com/en/actions/learn-github-actions/contexts#inputs-context)

## Example contents of the inputs context

---

The following example contents of the inputs context is from a workflow that has defined the build_id, deploy_target, and perform_deploy inputs.

```
{
"build_id": 123456768,
"deploy_target": "deployment_sys_1a",
"perform_deploy": true
}
```

## Example usage of the inputs context in a reusable workflow

---

This example reusable workflow uses the inputs context to get the values of the build_id, deploy_target, and perform_deploy inputs that were passed to the reusable workflow from the caller workflow.

```
name: Reusable deploy workflow
on:
  workflow_call:
    inputs:
      build_id:
        required: true
        type: number
      deploy_target:
        required: true
        type: string
      perform_deploy:
        required: true
        type: boolean

jobs:
  deploy:
    runs-on: ubuntu-latest
    if:' $ inputs.perform_deploy '
    steps:
      - name: Deploy build to target
        run: deploy --build '$ inputs.build_id ' --target '$ inputs.deploy_target '
```

## Example usage of the inputs context in a manually triggered workflow

---

This example workflow triggered by a workflow_dispatch event uses the inputs context to get the values of the build_id, deploy_target, and perform_deploy inputs that were passed to the workflow.

```
on:
  workflow_dispatch:
    inputs:
      build_id:
        required: true
        type: string
      deploy_target:
        required: true
        type: string
      perform_deploy:
        required: true
        type: boolean

jobs:
  deploy:
    runs-on: ubuntu-latest
    if: '$ inputs.perform_deploy '
    steps:
      - name: Deploy build to target
        run: deploy --build '$ inputs.build_id ' --target $ inputs.deploy_target '
```

## Examples

---

### More information

- [Using scripts to test your code on a runner](https://docs.github.com/en/actions/examples/using-scripts-to-test-your-code-on-a-runner)
- [Using the GitHub CLI on a runner](https://docs.github.com/en/actions/examples/using-the-github-cli-on-a-runner)
- [Using concurrency, expressions, and a test matrix](https://docs.github.com/en/actions/examples/using-concurrency-expressions-and-a-test-matrix)
