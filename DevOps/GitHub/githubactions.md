# Github Actions

## Understanding GitHub Actions

Learn the basics of GitHub Actions, including core concepts and essential terminology.

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. You can create workflows that build and test every pull request to your repository, or deploy merged pull requests to production.

GitHub Actions goes beyond just DevOps and lets you run workflows when other events happen in your repository. For example, you can run a workflow to automatically add the appropriate labels whenever someone creates a new issue in your repository.

GitHub provides Linux, Windows, and macOS virtual machines to run your workflows, or you can host your own self-hosted runners in your own data center or cloud infrastructure.

## The components of GitHub Actions

You can configure a GitHub Actions workflow to be triggered when an event occurs in your repository, such as a pull request being opened or an issue being created. Your workflow contains one or more jobs which can run in sequential order or in parallel. Each job will run inside its own virtual machine runner, or inside a container, and has one or more steps that either run a script that you define or run an action, which is a reusable extension that can simplify your workflow.

[Components](https://docs.github.com/assets/cb-25535/mw-1440/images/help/actions/overview-actions-simple.webp)

## Workflows

A workflow is a configurable automated process that will run one or more jobs. Workflows are defined by a YAML file checked in to your repository and will run when triggered by an event in your repository, or they can be triggered manually, or at a defined schedule.

Workflows are defined in the .github/workflows directory in a repository, and a repository can have multiple workflows, each of which can perform a different set of tasks. For example, you can have one workflow to build and test pull requests, another workflow to deploy your application every time a release is created, and still another workflow that adds a label every time someone opens a new issue.

You can reference a workflow within another workflow.

## Events

An event is a specific activity in a repository that triggers a workflow run. For example, activity can originate from GitHub when someone creates a pull request, opens an issue, or pushes a commit to a repository. You can also trigger a workflow to run on a schedule, by posting to a REST API, or manually.

[Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

## Jobs

A job is a set of steps in a workflow that is executed on the same runner. Each step is either a shell script that will be executed, or an action that will be run. Steps are executed in order and are dependent on each other. Since each step is executed on the same runner, you can share data from one step to another. For example, you can have a step that builds your application followed by a step that tests the application that was built.

You can configure a job's dependencies with other jobs; by default, jobs have no dependencies and run in parallel with each other. When a job takes a dependency on another job, it will wait for the dependent job to complete before it can run. For example, you may have multiple build jobs for different architectures that have no dependencies, and a packaging job that is dependent on those jobs. The build jobs will run in parallel, and when they have all completed successfully, the packaging job will run.

[Using Jobs](https://docs.github.com/en/actions/using-jobs)

## Actions

An action is a custom application for the GitHub Actions platform that performs a complex but frequently repeated task. Use an action to help reduce the amount of repetitive code that you write in your workflow files. An action can pull your git repository from GitHub, set up the correct toolchain for your build environment, or set up the authentication to your cloud provider.

You can write your own actions, or you can find actions to use in your workflows in the GitHub Marketplace.

## Runners

A runner is a server that runs your workflows when they're triggered. Each runner can run a single job at a time. GitHub provides Ubuntu Linux, Microsoft Windows, and macOS runners to run your workflows; each workflow run executes in a fresh, newly-provisioned virtual machine. GitHub also offers larger runners, which are available in larger configurations.

## Creating and example workflow

GitHub Actions uses YAML syntax to define the workflow. Each workflow is stored as a separate YAML file in your code repository, in a directory named .github/workflows.

You can create an example workflow in your repository that automatically triggers a series of commands whenever code is pushed. In this workflow, GitHub Actions checks out the pushed code, installs the bats testing framework, and runs a basic command to output the bats version: bats -v.

1. In your repository, create the .github/workflows/ directory to store your workflow files.
2. In the .github/workflows/ directory, create a new file called learn-github-actions.yml and add the following code.

YAML

```
name: learn-github-actions
run-name: ${{ github.actor }} is learning GitHub Actions
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

[Understading a workflow file](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#understanding-the-workflow-file)

## Visualizing the workflow file

In this diagram, you can see the workflow file you just created and how the GitHub Actions components are organized in a hierarchy. Each step executes a single action or shell script. Steps 1 and 2 run actions, while steps 3 and 4 run shell scripts.

[Github action Job](https://docs.github.com/assets/cb-33882/mw-1440/images/help/actions/overview-actions-event.webp)

## Viewing the activity for a workflow run

When your workflow is triggered, a workflow run is created that executes the workflow. After a workflow run has started, you can see a visualization graph of the run's progress and view each step's activity on GitHub.

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Actions.
3. In the left sidebar, click the workflow you want to see.
4. From the list of workflow runs, click the name of the run to see the workflow run summary.
5. In the left sidebar or in the visualization graph, click the job you want to see.
6. To view the results of a step, click the step.

## Finding and customizing actions

Actions are the building blocks that power your workflow. A workflow can contain actions created by the community, or you can create your own actions directly within your application's repository. This guide will show you how to discover, use, and customize actions.

The actions you use in your workflow can be defined in:

The same repository as your workflow file
Any public repository
A published Docker container image on Docker Hub
GitHub Marketplace is a central location for you to find actions created by the GitHub community.

[Github marketplace](https://github.com/marketplace?type=actions)

## Browsing Marketplace actions in the workflow editor

You can search and browse actions directly in your repository's workflow editor. From the sidebar, you can search for a specific action, view featured actions, and browse featured categories. You can also view the number of stars an action has received from the GitHub community.

1. In your repository, browse to the workflow file you want to edit.
2. In the upper right corner of the file view, to open the workflow editor, click (edit icon).
3. To the right of the editor, use the GitHub Marketplace sidebar to browse actions. Actions with the badge indicate GitHub has verified the creator of the action as a partner organization.

## Adding an action to your workflow

You can add an action to your workflow by referencing the action in your workflow file.

You can view the actions referenced in your GitHub Actions workflows as dependencies in the dependency graph of the repository containing your workflows.

## Adding an action from GitHub Marketplace

An action's listing page includes the action's version and the workflow syntax required to use the action. To keep your workflow stable even when updates are made to an action, you can reference the version of the action to use by specifying the Git or Docker tag number in your workflow file.

1. Navigate to the action you want to use in your workflow.
2. Click to view the full marketplace listing for the action.
3. Under "Installation", click copy the workflow syntax.
4. Paste the syntax as a new step in your workflow.
5. If the action requires you to provide inputs, set them in your workflow.

You can also enable Dependabot version updates for the actions that you add to your workflow.

## Adding an action from the same repository

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

If an action is defined in a published Docker container image on Docker Hub, you must reference the action with the docker://{image}:{tag} syntax in your workflow file. To protect your code and data, we strongly recommend you verify the integrity of the Docker container image from Docker Hub before using it in your workflow.

```
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: docker://alpine:3.8
```

[Docker Action example](https://github.com/actions/starter-workflows/blob/main/ci/docker-image.yml)

## Using release management for your custom actions

The creators of a community action have the option to use tags, branches, or SHA values to manage releases of the action. Similar to any dependency, you should indicate the version of the action you'd like to use based on your comfort with automatically accepting updates to the action.

You will designate the version of the action in your workflow file. Check the action's documentation for information on their approach to release management, and to see which tag, branch, or SHA value to use.

## Using tags

Tags are useful for letting you decide when to switch between major and minor versions, but these are more ephemeral and can be moved or deleted by the maintainer. This example demonstrates how to target an action that's been tagged as v1.0.1:

```
steps:
  - uses: actions/javascript-action@v1.0.1

```

## Using SHAs

If you need more reliable versioning, you should use the SHA value associated with the version of the action. SHAs are immutable and therefore more reliable than tags or branches. However, this approach means you will not automatically receive updates for an action, including important bug fixes and security updates. You must use a commit's full SHA value, and not an abbreviated value. When selecting a SHA, you should verify it is from the action's repository and not a repository fork. This example targets an action's SHA:

```
steps:
  - uses: actions/javascript-action@a824008085750b8e136effc585c3cd6082bd575f
```

## Using branches

Specifying a target branch for the action means it will always run the version currently on that branch. This approach can create problems if an update to the branch includes breaking changes. This example targets a branch named @main:

```
steps:
  - uses: actions/javascript-action@main
```

## Using inputs and outputs with an action

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
