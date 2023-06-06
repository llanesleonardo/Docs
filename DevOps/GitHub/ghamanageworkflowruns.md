# Manage workflow runs

## Manually running a workflow

When a workflow is configured to run on the workflow_dispatch event, you can run the workflow using the Actions tab on GitHub, GitHub CLI, or the REST API.

[Manually running a workflow](https://docs.github.com/en/actions/managing-workflow-runs/manually-running-a-workflow)

## Re-running workflows and jobs

You can re-run a workflow run, all failed jobs in a workflow run, or specific jobs in a workflow run up to 30 days after its initial run.

Re-running a workflow or jobs in a workflow uses the same GITHUB_SHA (commit SHA) and GITHUB_REF (Git ref) of the original event that triggered the workflow run. The workflow will use the privileges of the actor who initially triggered the workflow, not the privileges of the actor who initiated the re-run. You can re-run a workflow or jobs in a workflow for up to 30 days after the initial run. You cannot re-run jobs in a workflow once its logs have passed their retention limits.

## Re-running all the jobs in a workflow

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Actions.
3. In the left sidebar, click the workflow you want to see.
4. From the list of workflow runs, click the name of the run to see the workflow run summary.
5. In the upper-right corner of the workflow, re-run jobs.
   1. If any jobs failed, select the Re-run jobs dropdown menu and click Re-run all jobs.
   2. If no jobs failed, click Re-run all jobs.
6. Optionally, to enable runner diagnostic logging and step debug logging for the re-run, select Enable debug logging.
7. Click Re-run jobs.

## Re-running failed jobs in a workflow

If any jobs in a workflow run failed, you can re-run just the jobs that failed. When you re-run failed jobs in a workflow, a new workflow run will start for all failed jobs and their dependents. Any outputs for any successful jobs in the previous workflow run will be used for the re-run. Any artifacts that were created in the initial run will be available in the re-run. Any environment protection rules that passed in the previous run will automatically pass in the re-run.

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Actions.
3. In the left sidebar, click the workflow you want to see.
4. From the list of workflow runs, click the name of the run to see the workflow run summary.
5. In the upper-right corner of the workflow, select the Re-run jobs dropdown menu, and click Re-run failed jobs.
6. Optionally, to enable runner diagnostic logging and step debug logging for the re-run, select Enable debug logging.
7. Click Re-run jobs.

## Re-running a specific job in a workflow

When you re-run a specific job in a workflow, a new workflow run will start for the job and any dependents. Any outputs for any other jobs in the previous workflow run will be used for the re-run. Any artifacts that were created in the initial run will be available in the re-run. Any environment protection rules that passed in the previous run will automatically pass in the re-run.

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Actions.
3. In the left sidebar, click the workflow you want to see.
4. From the list of workflow runs, click the name of the run to see the workflow run summary.
5. Next to the job that you want to re-run, click (update icon).
6. Optionally, to enable runner diagnostic logging and step debug logging for the re-run, select Enable debug logging.
7. Click Re-run jobs.

## Re-running workflows and jobs with reusable workflows

Reusable workflows from public repositories can be referenced using a SHA, a release tag, or a branch name.

When you re-run a workflow that uses a reusable workflow and the reference is not a SHA, there are some behaviors to be aware of:

- Re-running all jobs in a workflow will use the reusable workflow from the specified reference.
- Re-running failed jobs or a specific job in a workflow will use the reusable workflow from the same commit SHA of the first attempt.

## Reviewing previous workflow runs

You can view the results from your previous attempts at running a workflow. You can also view previous workflow runs using the API. For more information, see "Actions."

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Actions.
3. In the left sidebar, click the workflow you want to see.
4. From the list of workflow runs, click the name of the run to see the workflow run summary.
5. To the right of the run name, select the Latest dropdown menu and click a previous run attempt.

## Canceling a workflow

[Canceling a workflow](https://docs.github.com/en/actions/managing-workflow-runs/canceling-a-workflow)

## Aproving workflow runs from public forks

[Aproving workflow runs from public forks](https://docs.github.com/en/actions/managing-workflow-runs/approving-workflow-runs-from-public-forks)

## Aproving workflow runs from private forks

[Aproving workflow runs from private forks](https://docs.github.com/en/actions/managing-workflow-runs/approving-workflow-runs-from-private-forks)
