# Incorporate changes

You can merge pull requests by retaining all the commits in a feature branch, squashing all commits into a single commit, or by rebasing individual commits from the head branch onto the base branch.

## Merge your commits

When you click the default Merge pull request option on a pull request on GitHub.com, all commits from the feature branch are added to the base branch in a merge commit. The pull request is merged using the --no-ff option.

To merge pull requests, you must have write permissions in the repository.

[Merge your commits](https://docs.github.com/assets/cb-5402/mw-1440/images/help/pull_requests/standard-merge-commit-diagram.webp)

## Squash and merge your commits

When you select the Squash and merge option on a pull request on GitHub.com, the pull request's commits are squashed into a single commit. Instead of seeing all of a contributor's individual commits from a topic branch, the commits are combined into one commit and merged into the default branch. Pull requests with squashed commits are merged using the fast-forward option.

To squash and merge pull requests, you must have write permissions in the repository, and the repository must allow squash merging.

[Squash and merge your commits](https://docs.github.com/assets/cb-5742/mw-1440/images/help/pull_requests/commit-squashing-diagram.webp)

You can use squash and merge to create a more streamlined Git history in your repository. Work-in-progress commits are helpful when working on a feature branch, but they aren’t necessarily important to retain in the Git history. If you squash these commits into one commit while merging to the default branch, you can retain the original changes with a clear Git history.

When you squash and merge, GitHub generates a default commit message, which you can edit. Depending on how the repository is configured and the number of commits in the pull request, not including merge commits, this message may include the pull request title, pull request description, or information about the commits.

[Merge message for a squash merge](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges#merge-message-for-a-squash-merge)

People with maintainer or admin access to a repository can configure their repository's default merge message for all squashed commits to use the pull request title, the pull request title and commit details, or the pull request title and description.

### Squashing and merging a long-running branch

If you plan to continue work on the head branch of a pull request after the pull request is merged, we recommend you don't squash and merge the pull request.

When you create a pull request, GitHub identifies the most recent commit that is on both the head branch and the base branch: the common ancestor commit. When you squash and merge the pull request, GitHub creates a commit on the base branch that contains all of the changes you made on the head branch since the common ancestor commit.

Because this commit is only on the base branch and not the head branch, the common ancestor of the two branches remains unchanged. If you continue to work on the head branch, then create a new pull request between the two branches, the pull request will include all of the commits since the common ancestor, including commits that you squashed and merged in the previous pull request. If there are no conflicts, you can safely merge these commits. However, this workflow makes merge conflicts more likely. If you continue to squash and merge pull requests for a long-running head branch, you will have to resolve the same conflicts repeatedly.

## Rebase and merge your commits

When you select the Rebase and merge option on a pull request on GitHub.com, all commits from the topic branch (or head branch) are added onto the base branch individually without a merge commit. In that way, the rebase and merge behavior resembles a fast-forward merge by maintaining a linear project history. However, rebasing achieves this by re-writing the commit history on the base branch with new commits.

The rebase and merge behavior on GitHub deviates slightly from git rebase. Rebase and merge on GitHub will always update the committer information and create new commit SHAs, whereas git rebase outside of GitHub does not change the committer information when the rebase happens on top of an ancestor commit. For more information about git rebase, see git-rebase in the Git documentation.

To rebase and merge pull requests, you must have write permissions in the repository, and the repository must allow rebase merging.

For a visual representation of git rebase, see The "Git Branching - Rebasing" chapter from the Pro Git book.

You aren't able to automatically rebase and merge on GitHub.com when:

- The pull request has merge conflicts.
- Rebasing the commits from the base branch into the head branch runs into conflicts.
- Rebasing the commits is considered "unsafe," such as when a rebase is possible without merge conflicts but would produce a different result than a merge would.

If you still want to rebase the commits but can't rebase and merge automatically on GitHub.com you must:

- Rebase the topic branch (or head branch) onto the base branch locally on the command line
- Resolve any merge conflicts on the command line.
- Force-push the rebased commits to the pull request's topic branch (or remote head branch).

Anyone with write permissions in the repository, can then merge the changes using the rebase and merge button on GitHub.com.

## Indirect merges

A pull request can be merged automatically if its head branch is directly or indirectly merged into the base branch externally. In other words, if the head branch's tip commit becomes reachable from the tip of the target branch. For example:

- Branch main is at commit C.
- Branch feature has been branched off of main and is currently at commit D. This branch has a pull request targeting main.
- Branch feature_2 is branched off of feature and is now at commit E. This branch also has a pull request targeting main.

If pull request E --> main is merged first, pull request D --> main will be marked as merged automatically because all of the commits from feature are now reachable from main. Merging feature_2 into main and pushing main to the server from the command line will mark both pull requests as merged.

Pull requests in this situation will be marked as merged even if branch protection rules have not been satisfied.

## Merging a pull request

Merge a pull request into the upstream branch when work is completed. Anyone with push access to the repository can complete the merge.

In a pull request, you propose that changes you've made on a head branch should be merged into a base branch. By default, any pull request can be merged at any time, unless the head branch is in conflict with the base branch. However, there may be restrictions on when you can merge a pull request into a specific branch. For example, you may only be able to merge a pull request into the default branch if required status checks are passing. Repository administrators can add constraints like this to branches using branch protection rules or repository rulesets.

You can configure a pull request to merge automatically when all merge requirements are met.

If the pull request has merge conflicts, or if you'd like to test the changes before merging, you can check out the pull request locally and merge it using the command line.

You can't merge a draft pull request.

The repository may be configured so that the head branch for a pull request is automatically deleted when you merge a pull request.

Pull requests are merged using the --no-ff option, except for pull requests with squashed or rebased commits, which are merged using the fast-forward option.

You can link a pull request to an issue to show that a fix is in progress and to automatically close the issue when someone merges the pull request.

If you decide you don't want the changes in a topic branch to be merged to the upstream branch, you can close the pull request without merging.

1. Under your repository name, click Pull requests.
2. In the "Pull Requests" list, click the pull request you'd like to merge.
3. Scroll down to the bottom of the pull request. Depending on the merge options enabled for your repository, you can:
   1. Merge all of the commits into the base branch by clicking Merge pull request. If the Merge pull request option is not shown, click the merge dropdown menu and select Create a merge commit.
   2. Squash the commits into one commit by clicking the merge dropdown menu, selecting Squash and merge and then clicking Squash and merge.
   3. Rebase the commits individually onto the base branch by clicking the merge dropdown menu, selecting Rebase and merge and then clicking Rebase and merge.
4. If prompted, type a commit message, or accept the default message.
5. If you have more than one email address associated with your account on GitHub.com, click the email address drop-down menu and select the email address to use as the Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then <username>@users.noreply.github.com is the default commit author email address.
6. Click Confirm merge, Confirm squash and merge, or Confirm rebase and merge.
7. Optionally, delete the branch. This keeps the list of branches in your repository tidy.

## Automatically merging a pull request

You can increase development velocity by enabling auto-merge for a pull request so that the pull request will merge automatically when all merge requirements are met.

If you enable auto-merge for a pull request, the pull request will merge automatically when all required reviews are met and all required status checks have passed. Auto-merge prevents you from waiting around for requirements to be met, so you can move on to other tasks.

Before you can use auto-merge with a pull request, auto-merge must be enabled for the repository.

After you enable auto-merge for a pull request, if someone who does not have write permissions to the repository pushes new changes to the head branch or switches the base branch of the pull request, auto-merge will be disabled. For example, if a maintainer enables auto-merge for a pull request from a fork, auto-merge will be disabled after a contributor pushes new changes to the pull request.

You can provide feedback about auto-merge through a GitHub Community discussion.

### Enabling auto-merge

People with write permissions to a repository can enable auto-merge for a pull request.

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Pull requests.
3. In the "Pull Requests" list, click the pull request you'd like to auto-merge.
4. Optionally, to choose a merge method, select the dropdown menu, then click a merge method.
5. Click Enable auto-merge.
6. If you chose the merge or squash and merge methods, type a commit message and description and choose the email address you want to author the merge commit.
7. Click Confirm auto-merge.

### Disabling auto-merge

People with write permissions to a repository and pull request authors can disable auto-merge for a pull request.

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Pull requests.
3. In the "Pull Requests" list, click the pull request you'd like to disable auto-merge for.
4. In the merge box, click Disable auto-merge.

## Merging a pull request with a merge queue

If a merge queue is required by the branch protection setting for the branch, you can add your pull requests to a merge queue and GitHub will merge the pull requests for you once all required checks have passed.

A merge queue can increase the rate at which pull requests are merged into a busy target branch while ensuring that all required branch protection checks pass.

Once a pull request has passed all of the required branch protection checks, a user with write access to the repository can add that pull request to a merge queue.

A merge queue may use GitHub Actions.

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Pull requests.
3. In the "Pull Requests" list, click the pull request you would like to add to a merge queue.
4. Click Merge when ready to add the pull request to the merge queue. Alternatively, if you are an administrator, you can:
   1. Directly merge the pull request by checking Merge without waiting for requirements to be met (bypass branch protections), if allowed by branch protection settings, and follow the standard flow.
5. Confirm you want to add the pull request to the merge queue by clicking Confirm merge when ready.

### Removing a pull request from a merge queue

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Pull requests.
3. In the "Pull Requests" list, click the pull request you would like to remove from a merge queue.
4. To remove the pull request from the queue, click Remove from queue.

Alternatively, you can navigate to the merge queue page for the base branch, click ... next to the pull request you want to remove, and select Remove from queue. For information on how to get to the merge queue page for the base branch, see the section below.

### Viewing merge queues

You can view the merge queue for a base branch in various places on GitHub.

- On the Branches page for the repository. We recommend you use this route if you don't have or don't know about a pull request already in a queue, and if you want to see what's in that queue. For more information, see "Viewing branches in your repository."
- On the pull request page when merge queue is required for merging, scroll to the bottom of the timeline and click the merge queue link.
- The merge queue view shows the pull requests that are currently in the queue, with your pull requests clearly marked.

### Handling pull requests removed from the merge queue

After grouping a pull request with the latest version of the target branch and changes ahead of it in the queue, if there are failed required status checks or conflicts with the base branch, GitHub will remove the pull request from the queue. The pull request timeline will display the reason why the pull request was removed from the queue.

## Closing a pull request

You may choose to close a pull request without merging it into the upstream branch. This can be handy if the changes proposed in the branch are no longer needed, or if another solution has been proposed in another branch.

1. Under your repository name, click Pull requests.
2. In the "Pull Requests" list, click the pull request you'd like to close.
3. At the bottom of the pull request, below the comment box, click Close pull request.
4. Optionally, delete the branch. This keeps the list of branches in your repository tidy.

## Reverting a pull request

You can revert a pull request after it's been merged to the upstream branch.

Reverting a pull request on GitHub creates a new pull request that contains one revert of the merge commit from the original merged pull request. To revert pull requests, you must have write permissions in the repository.

1. Under your repository name, click Pull requests.
2. In the "Pull Requests" list, click the pull request you'd like to revert.
3. Near the bottom of the pull request, click Revert. If the Revert option isn't displayed, you'll need to ask the repository administrator for write permissions.
4. Merge the resulting pull request. For more information, see "Merging a pull request."

[How to revert a commit on Github](https://www.youtube.com/watch?v=H2DuJNWbqLw)

[Use of Revert command on Git](https://www.youtube.com/watch?v=U3uwMr3u2Q4)
