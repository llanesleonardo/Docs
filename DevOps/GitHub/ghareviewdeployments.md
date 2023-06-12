Back: [Github Actions](./gha.md)

# Reviewing deployments

You can approve or reject jobs awaiting review.

Jobs that reference an environment configured with required reviewers will wait for an approval before starting. While a job is awaiting approval, it has a status of "Waiting". If a job is not approved within 30 days, it will automatically fail.

## Approving or rejecting a job

### Process' checklist

1. Navigate to the workflow run that requires review. For more information about navigating to a workflow run, see "Viewing workflow run history."
2. If the run requires review, you will see a notification for the review request. On the notification, click Review deployments.
   Select the job environment(s) to approve or reject. Optionally, leave a comment.
3. Approve or reject:
   - To approve the job, click Approve and deploy. Once a job is approved (and any other environment protection rules have passed), the job will proceed. At this point, the job can access any secrets stored in the environment.
   - To reject the job, click Reject. If a job is rejected, the workflow will fail.

## Bypassing environment protection rules

If you have configured environment protection rules that control whether software can be deployed to an environment, you can bypass these rules and force all pending jobs referencing the environment to proceed.

### Process' checklist

1. Navigate to the workflow run.
2. To the right of Deployment protection rules, click Start all waiting jobs.
3. In the pop-up window, select the environments for which you want to bypass environment protection rules.
4. Under Leave a comment, enter a description for bypassing the environment protection rules.
5. Click I understand the consequences, start deploying.

## Disabling and Enabling workflows

### More information

- [Disabling and Enabling workflows](https://docs.github.com/en/actions/managing-workflow-runs/disabling-and-enabling-a-workflow)

## Skipping workflow runs

### More information

- [Skipping workflow runs](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs)

## Deleting a workflow run

### More information

- [Deleting a workflow run](https://docs.github.com/en/actions/managing-workflow-runs/deleting-a-workflow-run)

## Downloading workflow artifacts

### More information

- [Downloading workflow artifacts](https://docs.github.com/en/actions/managing-workflow-runs/downloading-workflow-artifacts)

## Removing workflow artifacts

### More information

- [Removing workflow artifacts](https://docs.github.com/en/actions/managing-workflow-runs/removing-workflow-artifacts)
