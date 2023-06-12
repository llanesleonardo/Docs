Back: [Github Actions](./gha.md)

# Github Actions Workflows

Get a high-level overview of GitHub Actions workflows, including triggers, syntax, and advanced features.

A workflow is a configurable automated process that will run one or more jobs. Workflows are defined by a YAML file checked in to your repository and will run when triggered by an event in your repository, or they can be triggered manually, or at a defined schedule.

Workflows are defined in the .github/workflows directory in a repository, and a repository can have multiple workflows, each of which can perform a different set of tasks. For example, you can have one workflow to build and test pull requests, another workflow to deploy your application every time a release is created, and still another workflow that adds a label every time someone opens a new issue.

## Workflow basics

---

A workflow must contain the following basic components:

### Process' checklist

1. One or more events that will trigger the workflow.
2. One or more jobs, each of which will execute on a runner machine and run a series of one or more steps.
   .3 Each step can either run a script that you define or run an action, which is a reusable extension that can simplify your workflow.

## Triggering a workflow

---

Workflow triggers are events that cause a workflow to run. These events can be:

- Events that occur in your workflow's repository
- Events that occur outside of GitHub and trigger a repository_dispatch event on GitHub
- Scheduled times
- Manual

For example, you can configure your workflow to run when a push is made to the default branch of your repository, when a release is created, or when an issue is opened.

## Workflow syntax

---

Workflow are defined using YAML. For the full reference of the YAML syntax for authoring workflows, see "Workflow syntax for GitHub Actions."

## Create an example workflow

---

GitHub Actions uses YAML syntax to define the workflow. Each workflow is stored as a separate YAML file in your code repository, in a directory named .github/workflows.

You can create an example workflow in your repository that automatically triggers a series of commands whenever code is pushed. In this workflow, GitHub Actions checks out the pushed code, installs the bats testing framework, and runs a basic command to output the bats version: bats -v.

### Process' checklist

1. In your repository, create the .github/workflows/ directory to store your workflow files.
2. In the .github/workflows/ directory, create a new file called learn-github-actions.yml and add the following code.

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

Your new GitHub Actions workflow file is now installed in your repository and will run automatically each time someone pushes a change to the repository. To see the details about a workflow's execution history, see "Viewing the activity for a workflow run."

## Understading the workflow

---

### More information

- [Understanding the workflow](https://docs.github.com/en/actions/using-workflows/about-workflows#understanding-the-workflow-file)

## Visualizing the workflow file

---

In this diagram, you can see the workflow file you just created and how the GitHub Actions components are organized in a hierarchy. Each step executes a single action or shell script. Steps 1 and 2 run actions, while steps 3 and 4 run shell scripts. To find more prebuilt actions for your workflows, see "Finding and customizing actions."

### More information

- [Workflow execution example](https://docs.github.com/assets/cb-33882/mw-1440/images/help/actions/overview-actions-event.webp)

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

## Using starter workflows

---

GitHub provides preconfigured starter workflows that you can customize to create your own continuous integration workflow. GitHub analyzes your code and shows you CI starter workflows that might be useful for your repository. For example, if your repository contains Node.js code, you'll see suggestions for Node.js projects. You can use starter workflows as a starting place to build your custom workflow or use them as-is.

You can browse the full list of starter workflows in the actions/starter-workflows repository.

### More information

- [Starter workflows](https://github.com/actions/starter-workflows)

## Advanced workflow features

---

This section briefly describes some of the advanced features of GitHub Actions that help you create more complex workflows.

## Storing secrets

---

If your workflows use sensitive data, such as passwords or certificates, you can save these in GitHub as secrets and then use them in your workflows as environment variables. This means that you will be able to create and share workflows without having to embed sensitive values directly in the workflow's YAML source.

This example job demonstrates how to reference an existing secret as an environment variable, and send it as a parameter to an example command.

```
jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - name: Retrieve secret
        env:
          super_secret: ${{ secrets.SUPERSECRET }}
        run: |
          example-command "$super_secret"
```

## Creating dependent jobs

---

By default, the jobs in your workflow all run in parallel at the same time. If you have a job that must only run after another job has completed, you can use the needs keyword to create this dependency. If one of the jobs fails, all dependent jobs are skipped; however, if you need the jobs to continue, you can define this using the if conditional statement.

In this example, the setup, build, and test jobs run in series, with build and test being dependent on the successful completion of the job that precedes them:

```
jobs:
  setup:
    runs-on: ubuntu-latest
    steps:
      - run: ./setup_server.sh
  build:
    needs: setup
    runs-on: ubuntu-latest
    steps:
      - run: ./build_server.sh
  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - run: ./test_server.sh
```

## Using a matrix

---

A matrix strategy lets you use variables in a single job definition to automatically create multiple job runs that are based on the combinations of the variables. For example, you can use a matrix strategy to test your code in multiple versions of a language or on multiple operating systems. The matrix is created using the strategy keyword, which receives the build options as an array. For example, this matrix will run the job multiple times, using different versions of Node.js:

```
jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node: [12, 14, 16]
    steps:
      - uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node }}
```

## Caching dependencies

---

If your jobs regularly reuse dependencies, you can consider caching these files to help improve performance. Once the cache is created, it is available to all workflows in the same repository.

This example demonstrates how to cache the ~/.npm directory:

```
jobs:
  example-job:
    steps:
      - name: Cache node modules
        uses: actions/cache@v3
        env:
          cache-name: cache-node-modules
        with:
          path: ~/.npm
          key: ${{ runner.os }}-build-${{ env.cache-name }}-${{ hashFiles('**/package-lock.json') }}
          restore-keys: |
            ${{ runner.os }}-build-${{ env.cache-name }}-
```

## Using databases and service containers

---

If your job requires a database or cache service, you can use the services keyword to create an ephemeral container to host the service; the resulting container is then available to all steps in that job and is removed when the job has completed. This example demonstrates how a job can use services to create a postgres container, and then use node to connect to the service.

```
jobs:
  container-job:
    runs-on: ubuntu-latest
    container: node:10.18-jessie
    services:
      postgres:
        image: postgres
    steps:
      - name: Check out repository code
        uses: actions/checkout@v3
      - name: Install dependencies
        run: npm ci
      - name: Connect to PostgreSQL
        run: node client.js
        env:
          POSTGRES_HOST: postgres
          POSTGRES_PORT: 5432
```

## Using labels to route workflows

---

If you want to be sure that a particular type of runner will process your job, you can use labels to control where jobs are executed. You can assign labels to a self-hosted runner in addition to their default label of self-hosted. Then, you can refer to these labels in your YAML workflow, ensuring that the job is routed in a predictable way. GitHub-hosted runners have predefined labels assigned.

This example shows how a workflow can use labels to specify the required runner:

```
jobs:
  example-job:
    runs-on: [self-hosted, linux, x64, gpu]
```

A workflow will only run on a runner that has all the labels in the runs-on array. The job will preferentially go to an idle self-hosted runner with the specified labels. If none are available and a GitHub-hosted runner with the specified labels exists, the job will go to a GitHub-hosted runner.

## Reusing workflows

---

You can call one workflow from within another workflow. This allows you to reuse workflows, avoiding duplication and making your workflows easier to maintain.

## Using environments

---

You can configure environments with protection rules and secrets to control the execution of jobs in a workflow. Each job in a workflow can reference a single environment. Any protection rules configured for the environment must pass before a job referencing the environment is sent to a runner.

## Triggering a workflow

---

How to automatically trigger GitHub Actions workflows

Workflow triggers are events that cause a workflow to run. These events can be:

- Events that occur in your workflow's repository
- Events that occur outside of GitHub and trigger a repository_dispatch event on GitHub
- Scheduled times
- Manual

For example, you can configure your workflow to run when a push is made to the default branch of your repository, when a release is created, or when an issue is opened.

Workflow triggers are defined with the on key. For more information, see "Workflow syntax for GitHub Actions."

The following steps occur to trigger a workflow run:

### Process' checklist

1. An event occurs on your repository. The event has an associated commit SHA and Git ref.
2. GitHub searches the .github/workflows directory in your repository for workflow files that are present in the associated commit SHA or Git ref of the event.
3. A workflow run is triggered for any workflows that have on: values that match the triggering event. Some events also require the workflow file to be present on the default branch of the repository in order to run.

Each workflow run will use the version of the workflow that is present in the associated commit SHA or Git ref of the event. When a workflow runs, GitHub sets the GITHUB_SHA (commit SHA) and GITHUB_REF (Git ref) environment variables in the runner environment.

## Triggering a workflow from a workflow

---

When you use the repository's GITHUB_TOKEN to perform tasks, events triggered by the GITHUB_TOKEN, with the exception of workflow_dispatch and repository_dispatch, will not create a new workflow run. This prevents you from accidentally creating recursive workflow runs. For example, if a workflow run pushes code using the repository's GITHUB_TOKEN, a new workflow will not run even when the repository contains a workflow configured to run when push events occur.

If you do want to trigger a workflow from within a workflow run, you can use a GitHub App installation access token or a personal access token instead of GITHUB_TOKEN to trigger events that require a token.

If you use a GitHub App, you'll need to create a GitHub App and store the app ID and private key as secrets. If you use a personal access token, you'll need to create a personal access token and store it as a secret.

To minimize your GitHub Actions usage costs, ensure that you don't create recursive or unintended workflow runs.

For example, the following workflow uses a personal access token (stored as a secret called MY_TOKEN) to add a label to an issue via GitHub CLI. Any workflows that run when a label is added will run once this step is performed.

```
on:
  issues:
    types:
      - opened

jobs:
  label_issue:
    runs-on: ubuntu-latest
    steps:
      - env:
          GITHUB_TOKEN: ${{ secrets.MY_TOKEN }}
          ISSUE_URL: ${{ github.event.issue.html_url }}
        run: |
          gh issue edit $ISSUE_URL --add-label "triage"
```

Conversely, the following workflow uses GITHUB_TOKEN to add a label to an issue. It will not trigger any workflows that run when a label is added.

```
on:
  issues:
    types:
      - opened

jobs:
  label_issue:
    runs-on: ubuntu-latest
    steps:
      - env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          ISSUE_URL: ${{ github.event.issue.html_url }}
        run: |
          gh issue edit $ISSUE_URL --add-label "triage"
```

## Using events to trigger workflows

---

Use the on key to specify what events trigger your workflow.

## Using a single event

---

For example, a workflow with the following on value will run when a push is made to any branch in the workflow's repository:

```
on: push
```

## Using multiple events

---

You can specify a single event or multiple events. For example, a workflow with the following on value will run when a push is made to any branch in the repository or when someone forks the repository:

```
on: [push, fork]
```

## Using activity types and filters with multiple events

---

You can use activity types and filters to further control when your workflow will run.

If you specify activity types or filters for an event and your workflow triggers on multiple events, you must configure each event separately. You must append a colon (:) to all events, including events without configuration.

For example, a workflow with the following on value will run when:

- A label is created
- A push is made to the main branch in the repository
- A push is made to a GitHub Pages-enabled branch

```
on:
  label:
    types:
      - created
  push:
    branches:
      - main
  page_build:
```

## Using event activity types

---

Some events have activity types that give you more control over when your workflow should run. Use on.<event_name>.types to define the type of event activity that will trigger a workflow run.

For example, the issue_comment event has the created, edited, and deleted activity types. If your workflow triggers on the label event, it will run whenever a label is created, edited, or deleted. If you specify the created activity type for the label event, your workflow will run when a label is created but not when a label is edited or deleted.

```
on:
  label:
    types:
      - created
```

If you specify multiple activity types, only one of those event activity types needs to occur to trigger your workflow. If multiple triggering event activity types for your workflow occur at the same time, multiple workflow runs will be triggered. For example, the following workflow triggers when an issue is opened or labeled. If an issue with two labels is opened, three workflow runs will start: one for the issue opened event and two for the two issue labeled events.

```
on:
  issues:
    types:
      - opened
      - labeled
```

## Using filters

---

Some events have filters that give you more control over when your workflow should run.

For example, the push event has a branches filter that causes your workflow to run only when a push to a branch that matches the branches filter occurs, instead of when any push occurs.

```
on:
  push:
    branches:
      - main
      - 'releases/**'
```

## Using filters to target specific branches for pull request events

---

When using the pull_request and pull_request_target events, you can configure a workflow to run only for pull requests that target specific branches.

Use the branches filter when you want to include branch name patterns or when you want to both include and exclude branch names patterns. Use the branches-ignore filter when you only want to exclude branch name patterns. You cannot use both the branches and branches-ignore filters for the same event in a workflow.

If you define both branches/branches-ignore and paths/paths-ignore, the workflow will only run when both filters are satisfied.

The branches and branches-ignore keywords accept glob patterns that use characters like \*, \*\*, +, ?, ! and others to match more than one branch name. If a name contains any of these characters and you want a literal match, you need to escape each of these special characters with \.

## Example: Including branches

---

The patterns defined in branches are evaluated against the Git ref's name. For example, the following workflow would run whenever there is a pull_request event for a pull request targeting:

A branch named main (refs/heads/main)
A branch named mona/octocat (refs/heads/mona/octocat)
A branch whose name starts with releases/, like releases/10 (refs/heads/releases/10)

```
on:
  pull_request:
    # Sequence of patterns matched against refs/heads
    branches:
      - main
      - 'mona/octocat'
      - 'releases/**'
```

## Example: Excluding branches

---

When a pattern matches the branches-ignore pattern, the workflow will not run. The patterns defined in branches are evaluated against the Git ref's name. For example, the following workflow would run whenever there is a pull_request event unless the pull request is targeting:

- A branch named mona/octocat (refs/heads/mona/octocat)
- A branch whose name matches releases/\*\*-alpha, like releases/beta/3-alpha (refs/heads/releases/beta/3-alpha)

```
on:
  pull_request:
    # Sequence of patterns matched against refs/heads
    branches-ignore:
      - 'mona/octocat'
      - 'releases/**-alpha'
```

## Example: Including and excluding branches

---

You cannot use branches and branches-ignore to filter the same event in a single workflow. If you want to both include and exclude branch patterns for a single event, use the branches filter along with the ! character to indicate which branches should be excluded.

If you define a branch with the ! character, you must also define at least one branch without the ! character. If you only want to exclude branches, use branches-ignore instead.

The order that you define patterns matters.

- A matching negative pattern (prefixed with !) after a positive match will exclude the Git ref.
- A matching positive pattern after a negative match will include the Git ref again.

The following workflow will run on pull_request events for pull requests that target releases/10 or releases/beta/mona, but not for pull requests that target releases/10-alpha or releases/beta/3-alpha because the negative pattern !releases/\*\*-alpha follows the positive pattern.

```
on:
  pull_request:
    branches:
      - 'releases/**'
      - '!releases/**-alpha'
```

## Using filters to target specific branches or tags for push events

---

When using the push event, you can configure a workflow to run on specific branches or tags.

Use the branches filter when you want to include branch name patterns or when you want to both include and exclude branch names patterns. Use the branches-ignore filter when you only want to exclude branch name patterns. You cannot use both the branches and branches-ignore filters for the same event in a workflow.

Use the tags filter when you want to include tag name patterns or when you want to both include and exclude tag names patterns. Use the tags-ignore filter when you only want to exclude tag name patterns. You cannot use both the tags and tags-ignore filters for the same event in a workflow.

If you define only tags/tags-ignore or only branches/branches-ignore, the workflow won't run for events affecting the undefined Git ref. If you define neither tags/tags-ignore or branches/branches-ignore, the workflow will run for events affecting either branches or tags. If you define both branches/branches-ignore and paths/paths-ignore, the workflow will only run when both filters are satisfied.

The branches, branches-ignore, tags, and tags-ignore keywords accept glob patterns that use characters like \*, \*\*, +, ?, ! and others to match more than one branch or tag name. If a name contains any of these characters and you want a literal match, you need to escape each of these special characters with \.

## Example: Including branches and tags

---

The patterns defined in branches and tags are evaluated against the Git ref's name. For example, the following workflow would run whenever there is a push event to:

- A branch named main (refs/heads/main)
- A branch named mona/octocat (refs/heads/mona/octocat)
- A branch whose name starts with releases/, like releases/10 (refs/heads/releases/10)
- A tag named v2 (refs/tags/v2)
- A tag whose name starts with v1., like v1.9.1 (refs/tags/v1.9.1)

```
on:
  push:
    # Sequence of patterns matched against refs/heads
    branches:
      - main
      - 'mona/octocat'
      - 'releases/**'
    # Sequence of patterns matched against refs/tags
    tags:
      - v2
      - v1.*
```

## Example: Including and excluding branches and tags

---

You can't use branches and branches-ignore to filter the same event in a single workflow. Similarly, you can't use tags and tags-ignore to filter the same event in a single workflow. If you want to both include and exclude branch or tag patterns for a single event, use the branches or tags filter along with the ! character to indicate which branches or tags should be excluded.

If you define a branch with the ! character, you must also define at least one branch without the ! character. If you only want to exclude branches, use branches-ignore instead. Similarly, if you define a tag with the ! character, you must also define at least one tag without the ! character. If you only want to exclude tags, use tags-ignore instead.

The order that you define patterns matters.

- A matching negative pattern (prefixed with !) after a positive match will exclude the Git ref.
- A matching positive pattern after a negative match will include the Git ref again.

The following workflow will run on pushes to releases/10 or releases/beta/mona, but not on releases/10-alpha or releases/beta/3-alpha because the negative pattern !releases/\*\*-alpha follows the positive pattern.

```
on:
  push:
    branches:
      - 'releases/**'
      - '!releases/**-alpha'
```

## Using filters to target specific paths for pull request or push events

---

When using the push and pull_request events, you can configure a workflow to run based on what file paths are changed. Path filters are not evaluated for pushes of tags.

Use the paths filter when you want to include file path patterns or when you want to both include and exclude file path patterns. Use the paths-ignore filter when you only want to exclude file path patterns. You cannot use both the paths and paths-ignore filters for the same event in a workflow.

If you define both branches/branches-ignore and paths/paths-ignore, the workflow will only run when both filters are satisfied.

The paths and paths-ignore keywords accept glob patterns that use the \* and \*\* wildcard characters to match more than one path name.

## Example: Including paths

---

If at least one path matches a pattern in the paths filter, the workflow runs. For example, the following workflow would run anytime you push a JavaScript file (.js).

```
on:
  push:
    paths:
      - '**.js'
```

## Example: Excluding paths

---

When all the path names match patterns in paths-ignore, the workflow will not run. If any path names do not match patterns in paths-ignore, even if some path names match the patterns, the workflow will run.

A workflow with the following path filter will only run on push events that include at least one file outside the docs directory at the root of the repository.

```
on:
  push:
    paths-ignore:
      - 'docs/**'
```

## Example: Including and excluding paths

---

You can not use paths and paths-ignore to filter the same event in a single workflow. If you want to both include and exclude path patterns for a single event, use the paths filter along with the ! character to indicate which paths should be excluded.

If you define a path with the ! character, you must also define at least one path without the ! character. If you only want to exclude paths, use paths-ignore instead.

The order that you define patterns matters:

A matching negative pattern (prefixed with !) after a positive match will exclude the path.
A matching positive pattern after a negative match will include the path again.
This example runs anytime the push event includes a file in the sub-project directory or its subdirectories, unless the file is in the sub-project/docs directory. For example, a push that changed sub-project/index.js or sub-project/src/index.js will trigger a workflow run, but a push changing only sub-project/docs/readme.md will not.

```
on:
  push:
    paths:
      - 'sub-project/**'
      - '!sub-project/docs/**'
```

## Git diff comparisons

---

The filter determines if a workflow should run by evaluating the changed files and running them against the paths-ignore or paths list. If there are no files changed, the workflow will not run.

GitHub generates the list of changed files using two-dot diffs for pushes and three-dot diffs for pull requests:

- ull requests: Three-dot diffs are a comparison between the most recent version of the topic branch and the commit where the topic branch was last synced with the base branch.
- Pushes to existing branches: A two-dot diff compares the head and base SHAs directly with each other.
- Pushes to new branches: A two-dot diff against the parent of the ancestor of the deepest commit pushed.

Diffs are limited to 300 files. If there are files changed that aren't matched in the first 300 files returned by the filter, the workflow will not run. You may need to create more specific filters so that the workflow will run automatically.

## Using filters to target specific branches for workflow run events

---

When using the workflow_run event, you can specify what branches the triggering workflow must run on in order to trigger your workflow.

The branches and branches-ignore filters accept glob patterns that use characters like \*, \*\*, +, ?, ! and others to match more than one branch name. If a name contains any of these characters and you want a literal match, you need to escape each of these special characters with \.

For example, a workflow with the following trigger will only run when the workflow named Build runs on a branch whose name starts with releases/:

```
on:
  workflow_run:
    workflows: ["Build"]
    types: [requested]
    branches:
      - 'releases/**'
```

A workflow with the following trigger will only run when the workflow named Build runs on a branch that is not named canary:

```
on:
  workflow_run:
    workflows: ["Build"]
    types: [requested]
    branches-ignore:
      - "canary"
```

You cannot use both the branches and branches-ignore filters for the same event in a workflow. If you want to both include and exclude branch patterns for a single event, use the branches filter along with the ! character to indicate which branches should be excluded.

The order that you define patterns matters.

A matching negative pattern (prefixed with !) after a positive match will exclude the branch.
A matching positive pattern after a negative match will include the branch again.
For example, a workflow with the following trigger will run when the workflow named Build runs on a branch that is named releases/10 or releases/beta/mona but will not releases/10-alpha, releases/beta/3-alpha, or main.

```
on:
  workflow_run:
    workflows: ["Build"]
    types: [requested]
    branches:
      - 'releases/**'
      - '!releases/**-alpha'
```

## Defining inputs for manually triggered workflows

---

When using the workflow_dispatch event, you can optionally specify inputs that are passed to the workflow. The triggered workflow receives the inputs in the inputs context.

```
on:
  workflow_dispatch:
    inputs:
      logLevel:
        description: 'Log level'
        required: true
        default: 'warning'
        type: choice
        options:
          - info
          - warning
          - debug
      print_tags:
        description: 'True to print to STDOUT'
        required: true
        type: boolean
      tags:
        description: 'Test scenario tags'
        required: true
        type: string
      environment:
        description: 'Environment to run tests against'
        type: environment
        required: true

jobs:
  print-tag:
    runs-on: ubuntu-latest
    if:  ${{ inputs.print_tags }}
    steps:
      - name: Print the input tag to STDOUT
        run: echo  The tags are ${{ inputs.tags }}
```

## Defining inputs, outputs, and secrets for reusable workflows

---

You can define inputs and secrets that a reusable workflow should receive from a calling workflow. You can also specify outputs that a reusable workflow will make available to a calling workflow.

## Using event information

---

Information about the event that triggered a workflow run is available in the github.event context. The properties in the github.event context depend on the type of event that triggered the workflow. For example, a workflow triggered when an issue is labeled would have information about the issue and label.

## Viewing all properties of an event

---

Reference the webhook event documentation for common properties and example payloads.

You can also print the entire github.event context to see what properties are available for the event that triggered your workflow:

```
jobs:
  print_context:
    runs-on: ubuntu-latest
    steps:
      - env:
          EVENT_CONTEXT: ${{ toJSON(github.event) }}
        run: |
          echo $EVENT_CONTEXT
```

## Accessing and using event properties

---

You can use the github.event context in your workflow. For example, the following workflow runs when a pull request that changes package\*.json, .github/CODEOWNERS, or .github/workflows/\*\* is opened. If the pull request author (github.event.pull_request.user.login) is not octobot or dependabot[bot], then the workflow uses the GitHub CLI to label and comment on the pull request (github.event.pull_request.number).

```
on:
  pull_request:
    types:
      - opened
    paths:
      - '.github/workflows/**'
      - '.github/CODEOWNERS'
      - 'package*.json'

jobs:
  triage:
    if: >-
      github.event.pull_request.user.login != 'octobot' &&
      github.event.pull_request.user.login != 'dependabot[bot]'
    runs-on: ubuntu-latest
    steps:
      - name: "Comment about changes we can't accept"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          PR: ${{ github.event.pull_request.html_url }}
        run: |
          gh pr edit $PR --add-label 'invalid'
          gh pr comment $PR --body 'It looks like you edited `package*.json`, `.github/CODEOWNERS`, or `.github/workflows/**`. We do not allow contributions to these files. Please review our [contributing guidelines](https://github.com/octo-org/octo-repo/blob/main/CONTRIBUTING.md) for what contributions are accepted.'
```

## Further controlling how your workflow will run

---

If you want more granular control than events, event activity types, or event filters provide, you can use conditionals and environments to control whether individual jobs or steps in your workflow will run.

## Using conditionals

---

You can use conditionals to further control whether jobs or steps in your workflow will run.

## Example using a value in the event payload

---

For example, if you want the workflow to run when a specific label is added to an issue, you can trigger on the issues labeled event activity type and use a conditional to check what label triggered the workflow. The following workflow will run when any label is added to an issue in the workflow's repository, but the run_if_label_matches job will only execute if the label is named bug.

```
on:
  issues:
    types:
      - labeled

jobs:
  run_if_label_matches:
    if: github.event.label.name == 'bug'
    runs-on: ubuntu-latest
    steps:
      - run: echo 'The label was bug'
```

## Example using event type

---

For example, if you want to run different jobs or steps depending on what event triggered the workflow, you can use a conditional to check whether a specific event type exists in the event context. The following workflow will run whenever an issue or pull request is closed. If the workflow ran because an issue was closed, the github.event context will contain a value for issue but not for pull_request. Therefore, the if_issue step will run but the if_pr step will not run. Conversely, if the workflow ran because a pull request was closed, the if_pr step will run but the if_issue step will not run.

```
on:
  issues:
    types:
      - closed
  pull_request:
    types:
      - closed

jobs:
  state_event_type:
    runs-on: ubuntu-latest
    steps:
    - name: if_issue
      if: github.event.issue
      run: |
        echo An issue was closed
    - name: if_pr
      if: github.event.pull_request
      run: |
        echo A pull request was closed
```

## Using environments to manually trigger workflow jobs

---

If you want to manually trigger a specific job in a workflow, you can use an environment that requires approval from a specific team or user. First, configure an environment with required reviewers.

Then, reference the environment name in a job in your workflow using the environment: key. Any job referencing the environment will not run until at least one reviewer approves the job.

For example, the following workflow will run whenever there is a push to main. The build job will always run. The publish job will only run after the build job successfully completes (due to needs: [build]) and after all of the rules (including required reviewers) for the environment called production pass (due to environment: production).

```
on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: build
        echo 'building'

  publish:
    needs: [build]
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: publish
        echo 'publishing'
```

### More information

- [Available events](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

## Events that trigger workflows

---

You can configure your workflows to run when specific activity on GitHub happens, at a scheduled time, or when an event outside of GitHub occurs.

### More information

- [Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)
- [Workflow Syntax](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [Workflow commands](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions)

## Reusing workflows

---

Learn how to avoid duplication when creating a workflow by reusing existing workflows.

Rather than copying and pasting from one workflow to another, you can make workflows reusable. You and anyone with access to the reusable workflow can then call the reusable workflow from another workflow.

Reusing workflows avoids duplication. This makes workflows easier to maintain and allows you to create new workflows more quickly by building on the work of others, just as you do with actions. Workflow reuse also promotes best practice by helping you to use workflows that are well designed, have already been tested, and have been proven to be effective. Your organization can build up a library of reusable workflows that can be centrally maintained.

The diagram below shows an in-progress workflow run that uses a reusable workflow.

- After each of three build jobs on the left of the diagram completes successfully, a dependent job called "Deploy" is run.
- The "Deploy" job calls a reusable workflow that contains three jobs: "Staging", "Review", and "Production."
- The "Production" deployment job only runs after the "Staging" job has completed successfully.
- When a job targets an environment, the workflow run displays a progress bar that shows the number of steps in the job. In the diagram below, the "Production" job contains 8 steps, with step 6 currently being processed.
- Using a reusable workflow to run deployment jobs allows you to run those jobs for each build without duplicating code in workflows.

### More information

- [Deployment.yml example](https://docs.github.com/assets/cb-34427/mw-1440/images/help/actions/reusable-workflows-ci-cd.webp)

A workflow that uses another workflow is referred to as a "caller" workflow. The reusable workflow is a "called" workflow. One caller workflow can use multiple called workflows. Each called workflow is referenced in a single line. The result is that the caller workflow file may contain just a few lines of YAML, but may perform a large number of tasks when it's run. When you reuse a workflow, the entire called workflow is used, just as if it was part of the caller workflow.

If you reuse a workflow from a different repository, any actions in the called workflow run as if they were part of the caller workflow. For example, if the called workflow uses actions/checkout, the action checks out the contents of the repository that hosts the caller workflow, not the called workflow.

When a reusable workflow is triggered by a caller workflow, the github context is always associated with the caller workflow. The called workflow is automatically granted access to github.token and secrets.GITHUB_TOKEN.

You can view the reused workflows referenced in your GitHub Actions workflows as dependencies in the dependency graph of the repository containing your workflows.

## Reusable workflows and starter workflows

---

Starter workflows allow everyone in your organization who has permission to create workflows to do so more quickly and easily. When people create a new workflow, they can choose a starter workflow and some or all of the work of writing the workflow will be done for them. Within a starter workflow, you can also reference reusable workflows to make it easy for people to benefit from reusing centrally managed workflow code. If you use a commit SHA when referencing the reusable workflow, you can ensure that everyone who reuses that workflow will always be using the same YAML code. However, if you reference a reusable workflow by a tag or branch, be sure that you can trust that version of the workflow.

A reusable workflow can be used by another workflow if any of the following is true:

- Both workflows are in the same repository.
- The called workflow is stored in a public repository, and your organization allows you to use public reusable workflows.
- The called workflow is stored in a private repository and the settings for that repository allow it to be accessed.

## Using GitHub-hosted runners

---

The assignment of GitHub-hosted runners is always evaluated using only the caller's context. Billing for GitHub-hosted runners is always associated with the caller. The caller workflow cannot use GitHub-hosted runners from the called repository.

## Using self-hosted runners

---

Called workflows that are owned by the same user or organization as the caller workflow can access self-hosted runners from the caller's context. This means that a called workflow can access self-hosted runners that are:

- In the caller repository
- In the caller repository's organization, provided that the runner has been made available to the caller repository

## Creating re usable workflows

---

### More information

- [Creating re usable workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows#creating-a-reusable-workflow)
- [Using outputs from a resusable workflow](https://docs.github.com/en/actions/using-workflows/reusing-workflows#using-outputs-from-a-reusable-workflow)

## Required workflows

---

You can specify which workflows will run as required status checks in all repositories or selected repositories in your organization.

You can configure a workflow that must run in repositories in an organization for all pull requests opened against any target branch. Required workflows allow you to implement organization-wide CI/CD policies that apply to current and future repositories. A required workflow is triggered by pull_request and pull_request_target default events and appears as a required status check, which blocks the ability to merge the pull request until the required workflow succeeds.

Required workflows are not the same as reusable workflows. Reusable workflows can be called by another workflow. Required workflows are enforced on repositories by an organization owner.

## Prerequisites

---

Before configuring a required workflow, note the following prerequisites:

- GitHub Actions must be enabled for a repository in the organization's settings in order for required workflows to run. Once enabled at an organization-level, required workflows will run even when GitHub Actions is disabled in the repository's settings.
- Required workflows are available for organizations and only in repositories where the organization's plan supports required status checks. If required status checks are not supported, the workflow will still run, but it will not be a required check and will not block merging.
- The repository's default branch must match the organization's default branch setting in order for required workflows to run as required status checks. If the default branch names do not match, the workflow will still run, but it will not be a required check.
- For required workflows to run, the pull request's source repository must be in the same organization as the target repository. GitHub will source the required workflow from a specified branch, tag, or commit SHA from the repository containing the workflow.
- Secrets used in a required workflow should be created at either the organization level or in the target repositories.
- Secrets in the source repository will not be fetched when a workflow runs in the target repository.
- When a workflow is run as a required workflow it will ignore all the filters in the on: section, for example: branches, branches-ignore, paths, types etc. The required workflow will run only for the pull_request and pull_request_target default events.
- Required workflows are not automatically triggered on already existing pull requests even though they automatically appear as expected checks. To trigger required workflows for an already existing pull request, push a new change to that pull request.

## Restrictions and behaviors for the source repository

---

Note the following restrictions and behaviors for the source repository and workflow:

- Required workflows can be stored in any repository folder and are not restricted to the .github/workflows folder like normal workflows. If a required workflow calls a reusable workflow, the reusable workflow must be stored in the .github/workflows folder. When calling a reusable workflow, a required workflow must use the full path and ref to the reusable workflow. For example, {owner}/{repo}/.github/workflows/{filename}@{ref}.
- If the required workflow is contained in a private repository, you must ensure that workflows within the repository are accessible by other repositories in your organization.
- Workflows stored in a public repository can be configured as required workflows for any repository in your organization. Workflows stored in a private repository can only be configured as required workflows for other private repositories in your organization.
- CodeQL is not supported in required workflows because CodeQL requires configuration at the repository level.
- To push to a branch where required workflows are enforced at the organizational level, create a pull request to make the necessary changes. You cannot push directly to branches with required workflow enforcements.
- If you want to allow direct pushes for a particular repository, you must remove the repository as a target from respective required workflows.
- Required workflows can be referenced using any branch, tag, or commit SHA from the repository containing the workflow file.

## Restrictions and behaviors for the target repository

---

Note the following restrictions and behaviors for the target repositories:

- When configuring a required workflow to run on all or selected repositories, the visibility of the repository containing the required workflow will affect which repositories in your organization the workflow runs on. Required workflows stored in public repositories will run on all repositories. Required workflows stored in private repositories will only run on other private repositories.
- Required workflows cannot be configured to run in the repository the workflow is created in. You should consider creating a separate repository to store your required workflows.
- When configuring a required workflow to run on all or selected repositories, required workflows will not run in repositories where actions is disabled in the organization settings.

## Viewing workflow runs for required workflows

---

After a required workflow has run at least once in a repository, you can view its workflow runs in that repository's "Actions" tab. To make changes to what workflows are configured as required in an organization, you must contact an organization owner. To make changes to a required workflow itself, anyone with write permissions for the repository that contains the required workflow can make changes to it.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Actions.
3. In the left sidebar, you can view workflow runs for required workflows under "Required workflows."

## Adding a required workflow to an organization

---

Organization owners can configure required workflows in their organization.

## Caching dependencies to speed up workflows

---

To make your workflows faster and more efficient, you can create and use caches for dependencies and other commonly reused files.

### More information

- [Caching dependencies to speed up workflows](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows)

## Storing workflow data as artifacts

---

Artifacts allow you to share data between jobs in a workflow and store data once that workflow has completed.

### More information

- [Storing workflow data as artifacts](https://docs.github.com/en/actions/using-workflows/storing-workflow-data-as-artifacts)

## Creating starter workflows for your organization

---

Learn how you can create starter workflows to help people in your team add new workflows more easily.

Starter workflows allow everyone in your organization who has permission to create workflows to do so more quickly and easily. When you create a new workflow, you can choose a starter workflow and some or all of the work of writing the workflow will be done for you. You can use starter workflows as a starting place to build your custom workflow or use them as-is. This not only saves time, it promotes consistency and best practice across your organization.

GitHub provides ready-to-use starter workflows for the following high level categories:

- Deployment (CD).
- Security.
- Continuous Integration (CI).
- Automation. Automation starter workflows offer solutions for automating workflows, such as triaging pull requests and applying a label based on the paths that are modified in the pull request, or greeting users who are first time contributors to the repository.

## Creating a starter workflow

---

Starter workflows can be created by users with write access to the organization's .github repository. These can then be used by organization members who have permission to create workflows.

Starter workflows created by users can only be used to create workflows in public repositories. Organizations using GitHub Enterprise Cloud can also use starter workflows to create workflows in private repositories.

This procedure demonstrates how to create a starter workflow and metadata file. The metadata file describes how the starter workflows will be presented to users when they are creating a new workflow.

### Process' checklist

1. If it doesn't already exist, create a new public repository named .github in your organization.
2. Create a directory named workflow-templates.
3. Create your new workflow file inside the workflow-templates directory.

If you need to refer to a repository's default branch, you can use the $default-branch placeholder. When a workflow is created the placeholder will be automatically replaced with the name of the repository's default branch.

For example, this file named octo-organization-ci.yml demonstrates a basic workflow.

```
name: Octo Organization CI

on:
  push:
    branches: [ $default-branch ]
  pull_request:
    branches: [ $default-branch ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Run a one-line script
        run: echo Hello from Octo Organization
```

4. Create a metadata file inside the workflow-templates directory. The metadata file must have the same name as the workflow file, but instead of the .yml extension, it must be appended with .properties.json. For example, this file named octo-organization-ci.properties.json contains the metadata for a workflow file named octo-organization-ci.yml:

```
{
    "name": "Octo Organization Workflow",
    "description": "Octo Organization CI starter workflow.",
    "iconName": "example-icon",
    "categories": [
        "Go"
    ],
    "filePatterns": [
        "package.json$",
        "^Dockerfile",
        ".*\\.md$"
    ]
}
```

5. -
   1. name - Required. The name of the workflow. This is displayed in the list of available workflows.
   2. description - Required. The description of the workflow. This is displayed in the list of available workflows.
   3. iconName - Optional. Specifies an icon for the workflow that is displayed in the list of workflows. iconName can one of the following types:
      1. An SVG file that is stored in the workflow-templates directory. To reference a file, the value must be the file name without the file extension. For example, an SVG file named example-icon.svg is referenced as example-icon.
      2. An icon from GitHub's set of Octicons. To reference an octicon, the value must be octicon <icon name>. For example, octicon smiley.
   4. categories - Optional. Defines the categories that the workflow is shown under. You can use category names from the following lists:
      1. General category names from the starter-workflows repository.
      2. Linguist languages from the list in the linguist repository.
      3. Supported tech stacks from the list in the starter-workflows repository.
   5. filePatterns - Optional. Allows the workflow to be used if the user's repository has a file in its root directory that matches a defined regular expression.

To add another starter workflow, add your files to the same workflow-templates directory.

## Using starter workflows

---

GitHub provides starter workflows for a variety of languages and tooling.

GitHub offers starter workflows for a variety of languages and tooling. When you set up workflows in your repository, GitHub analyzes the code in your repository and recommends workflows based on the language and framework in your repository. For example, if you use Node.js, GitHub will suggest a starter workflow file that installs your Node.js packages and runs your tests. You can search and filter to find relevant starter workflows.

## Using starter workflows

---

Anyone with write permission to a repository can set up GitHub Actions starter workflows for CI/CD or other automation.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Actions.
3. If you already have a workflow in your repository, click New workflow.
4. The "Choose a workflow" page shows a selection of recommended starter workflows. Find the starter workflow that you want to use, then click Configure. To help you find the starter workflow that you want, you can search for keywords or filter by category.
5. If the starter workflow contains comments detailing additional setup steps, follow these steps. Many of the starter workflow have corresponding guides.
6. Some starter workflows use secrets. For example, ${{ secrets.npm_token }}. If the starter workflow uses a secret, store the value described in the secret name as a secret in your repository.
7. Optionally, make additional changes. For example, you might want to change the value of on to change when the workflow runs.
8. Click Start commit.
9. Write a commit message and decide whether to commit directly to the default branch or to open a pull request.

## Sharing workflows, secrets, and runners with your organization

---

### More information

- [Sharing workflows, secrets, and runners with your organization](https://docs.github.com/en/actions/using-workflows/sharing-workflows-secrets-and-runners-with-your-organization)
