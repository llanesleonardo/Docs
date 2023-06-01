# Pull Request

Pull requests let you tell others about changes you've pushed to a branch in a repository on GitHub. Once a pull request is opened, you can discuss and review the potential changes with collaborators and add follow-up commits before your changes are merged into the base branch.

You can create pull requests on GitHub.com, with GitHub Desktop, in GitHub Codespaces, on GitHub Mobile, and when using GitHub CLI.

After initializing a pull request, you'll see a review page that shows a high-level overview of the changes between your branch (the compare branch) and the repository's base branch. You can add a summary of the proposed changes, review the changes made by commits, add labels, milestones, and assignees, and @mention individual contributors or teams.

Once you've created a pull request, you can push commits from your topic branch to add them to your existing pull request. These commits will appear in chronological order within your pull request and the changes will be visible in the "Files changed" tab.

[Video - Update Pull request with mew changes](https://www.youtube.com/watch?v=Hi2mRlmasCU)

Other contributors can review your proposed changes, add review comments, contribute to the pull request discussion, and even add commits to the pull request. By default, in public repositories, any user can submit reviews that approve or request changes to a pull request. Organization owners and repository admins can limit who is able to give approving pull request reviews or request changes.

You can see information about the branch's current deployment status and past deployment activity on the "Conversation" tab.

After you're happy with the proposed changes, you can merge the pull request. If you're working in a shared repository model, you create a pull request and you, or someone else, will merge your changes from your feature branch into the base branch you specify in your pull request.

If status checks are required for a repository, the required status checks must pass before you can merge your branch into the protected branch.

You can link a pull request to an issue to show that a fix is in progress and to automatically close the issue when someone merges the pull request.

You can visit your dashboard to quickly find links to recently updated pull requests you're working on or subscribed to.

## Draft pull requests

Draft pull requests are available in public repositories with GitHub Free for organizations and legacy per-repository billing plans, and in public and private repositories with GitHub Team, GitHub Enterprise Server, and GitHub Enterprise Cloud.

When you create a pull request, you can choose to create a pull request that is ready for review or a draft pull request. Draft pull requests cannot be merged, and code owners are not automatically requested to review draft pull requests.

When you're ready to get feedback on your pull request, you can mark your draft pull request as ready for review. Marking a pull request as ready for review will request reviews from any code owners. You can convert a pull request to a draft at any time.

## Differences between commits on compare and pull request pages

The compare and pull request pages use different methods to calculate the diff for changed files:

- Compare pages show the diff between the tip of the head ref and the current common ancestor (that is, the merge base) of the head and base ref.
- Pull request pages show the diff between the tip of the head ref and the common ancestor of the head and base ref at the time when the pull request was created. Consequently, the merge base used for the comparison might be different.

## About comparing branches in pull request

Pull requests display diffs to compare the changes you made in your topic branch against the base branch that you want to merge your changes into.

You can view proposed changes in a pull request in the Files changed tab.

Rather than viewing the commits themselves, you can view the proposed changes as they'll appear in the files once the pull request is merged. The files appear in alphabetical order within the Files changed tab. Additions to the files appear in green and are prefaced by a + sign while content that has been removed appears in red and is prefaced by a - sign.

### Diff view options

You have several options for viewing a diff:

- The unified view shows updated and existing content together in a linear view.
- The split view shows old content on one side and new content on the other side.
- The rich diff view shows a preview of how the changes will look once the pull request is merged.
- The source view shows the changes in source without the formatting of the rich diff view.

You can also choose to ignore whitespace changes to get a more accurate view of the substantial changes in a pull request.

[Unified and Split View](https://docs.github.com/assets/cb-186190/mw-1440/images/help/pull_requests/diff-settings-menu.webp)

To simplify reviewing changes in a large pull request, you can filter the diff to only show selected file types, show files you are a CODEOWNER of, hide files you have already viewed, or hide deleted files.

[Filter by extension](https://docs.github.com/assets/cb-48471/mw-1440/images/help/pull_requests/file-filter-menu.webp)

## Three-dot and two-dot Git diff comparisons

There are two comparison methods for the git diff command; two-dot (git diff A..B) and three-dot (git diff A...B). By default, pull requests on GitHub show a three-dot diff.

#### Three-dot Git diff comparison

The three-dot comparison shows the difference between the latest common commit of both branches (merge base) and the most recent version of the topic branch.

#### Two-dot Git diff comparison

The two-dot comparison shows the difference between the latest state of the base branch (for example, main) and the most recent version of the topic branch.

To see two committish references in a two-dot diff comparison on GitHub, you can edit the URL of your repository's "Comparing changes" page.

or example, this URL uses the shortened seven-character SHA codes to compare commits f75c570 and 3391dcc: https://github.com/github-linguist/linguist/compare/f75c570..3391dcc.

A two-dot diff compares two Git committish references, such as SHAs or OIDs (Object IDs), directly with each other. On GitHub, the Git committish references in a two-dot diff comparison must be pushed to the same repository or its forks.

If you want to simulate a two-dot diff in a pull request and see a comparison between the most recent versions of each branch, you can merge the base branch into your topic branch, which updates the last common ancestor between your branches.

[Git diff options](https://git-scm.com/docs/git-diff#git-diff-emgitdiffemltoptionsgtltcommitgtltcommitgt--ltpathgt82308203)

[Difference between 2 dots and 3 dots](https://www.youtube.com/watch?v=WRXmm-E77aY)

[Explaning Git Diff](https://www.youtube.com/watch?v=vXN50AmJjgY)

#### Merging often

To avoid getting confused, merge the base branch (for example, main) into your topic branch frequently. By merging the base branch, the diffs shown by two-dot and three-dot comparisons are the same. We recommend merging a pull request as soon as possible. This encourages contributors to make pull requests smaller, which is recommended in general.

## About collaborative development models

The way you use pull requests depends on the type of development model you use in your project. You can use the fork and pull model or the shared repository model.

## Fork an pull model

In the fork and pull model, anyone can fork an existing repository and push changes to their personal fork. You do not need permission to the source repository to push to a user-owned fork. The changes can be pulled into the source repository by the project maintainer. When you open a pull request proposing changes from your user-owned fork to a branch in the source (upstream) repository, you can allow anyone with push access to the upstream repository to make changes to your pull request. This model is popular with open source projects as it reduces the amount of friction for new contributors and allows people to work independently without upfront coordination.

[Open Source Guides](https://opensource.guide/)
[Github Skills](https://skills.github.com/)

## Shared repository model

In the shared repository model, collaborators are granted push access to a single shared repository and topic branches are created when changes need to be made. Pull requests are useful in this model as they initiate code review and general discussion about a set of changes before the changes are merged into the main development branch. This model is more prevalent with small teams and organizations collaborating on private projects.

## About status checks

Status checks let you know if your commits meet the conditions set for the repository you're contributing to.

Status checks are based on external processes, such as continuous integration builds, which run for each push you make to a repository. You can see the pending, passing, or failing state of status checks next to individual commits in your pull request.

Anyone with write permissions to a repository can set the state for any status check in the repository.

You can see the overall state of the last commit to a branch on your repository's branches page or in your repository's list of pull requests.

If status checks are required for a repository, the required status checks must pass before you can merge your branch into the protected branch.

[About protected repositories](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-before-merging)

### Types of status checks on GitHub

There are two types of status checks on GitHub:

- Checks
- Statuses

Checks are different from statuses in that they provide line annotations, more detailed messaging, and are only available for use with GitHub Apps.

Organization owners and users with push access to a repository can create checks and statuses with GitHub's API.

### Checks

When checks are set up in a repository, pull requests have a Checks tab where you can view detailed build output from status checks and rerun failed checks.

When a specific line in a commit causes a check to fail, you will see details about the failure, warning, or notice next to the relevant code in the Files tab of the pull request.

You can navigate between the checks summaries for various commits in a pull request, using the commit drop-down menu under the Checks tab.

[Checks](https://docs.github.com/assets/cb-345021/mw-1440/images/help/pull_requests/checks-summary-for-various-commits.webp)
[Skipping checks for individual commits](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks#skipping-and-requesting-checks-for-individual-commits)

You can also skip workflow runs triggered by the push and pull_request events by including a command in your commit message. [Skipping workflow runs](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs)

### Retention of status c hecks

GitHub.com retains check data for 400 days. After 400 days, the data is archived.

For archived check data, a rollup commit status appears that represents the state of all of the checks for the commit. To merge a pull request with checks that are both required and archived, you must rerun the checks.

## Propose changes

### About branches

Use a branch to isolate development work without affecting other branches in the repository. Each repository has one default branch, and can have multiple other branches. You can merge a branch into another branch using a pull request.

Branches allow you to develop features, fix bugs, or safely experiment with new ideas in a contained area of your repository.

You always create a branch from an existing branch. Typically, you might create a new branch from the default branch of your repository. You can then work on this new branch in isolation from changes that other people are making to the repository. A branch you create to build a feature is commonly referred to as a feature branch or topic branch.

You can also use a branch to publish a GitHub Pages site.

You must have write access to a repository to create a branch, open a pull request, or delete and restore branches in a pull request.

### About the default branch

When you create a repository with content on GitHub.com, GitHub creates the repository with a single branch. This first branch in the repository is the default branch. The default branch is the branch that GitHub displays when anyone visits your repository. The default branch is also the initial branch that Git checks out locally when someone clones the repository. Unless you specify a different branch, the default branch in a repository is the base branch for new pull requests and code commits.

By default, GitHub names the default branch main in any new repository.

You can change the default branch for an existing repository.

You can set the name of the default branch for new repositories.

### Working with branches

Once you're satisfied with your work, you can open a pull request to merge the changes in the current branch (the head branch) into another branch (the base branch).

After a pull request has been merged, or closed, you can delete the head branch as this is no longer needed. You must have write access in the repository to delete branches. You can't delete branches that are directly associated with open pull requests.

If you delete a head branch after its pull request has been merged, GitHub checks for any open pull requests in the same repository that specify the deleted branch as their base branch. GitHub automatically updates any such pull requests, changing their base branch to the merged pull request's base branch. The following diagrams illustrate this.

Here someone has created a branch called feature1 from the main branch, and you've then created a branch called feature2 from feature1. There are open pull requests for both branches. The arrows indicate the current base branch for each pull request. At this point, feature1 is the base branch for feature2. If the pull request for feature2 is merged now, the feature2 branch will be merged into feature1.

[Branches example](https://docs.github.com/assets/cb-2058/mw-1440/images/help/branches/pr-retargeting-diagram1.webp)

In the next diagram, someone has merged the pull request for feature1 into the main branch, and they have deleted the feature1 branch. As a result, GitHub has automatically retargeted the pull request for feature2 so that its base branch is now main.

[Branches example 2](https://docs.github.com/assets/cb-2581/mw-1440/images/help/branches/pr-retargeting-diagram2.webp)

Now when you merge the feature2 pull request, it'll be merged into the main branch.

### Working with protected branches

Repository administrators or custom roles with the "edit repository rules" permission can enable protections on a branch. If you're working on a branch that's protected, you won't be able to delete or force push to the branch. Repository administrators can additionally enable several other protected branch settings to enforce various workflows before a branch can be merged.

To see if your pull request can be merged, look in the merge box at the bottom of the pull request's Conversation tab.

When a branch is protected:

- You won't be able to delete or force push to the branch.
- If required status checks are enabled on the branch, you won't be able to merge changes into the branch until all of the required CI tests pass. For more information, see "About status checks."
- If required pull request reviews are enabled on the branch, you won't be able to merge changes into the branch until all requirements in the pull request review policy have been met. For more information, see "Merging a pull request."
- If required review from a code owner is enabled on a branch, and a pull request modifies code that has an owner, a code owner must approve the pull request before it can be merged. For more information, see "About code owners."
- If required commit signing is enabled on a branch, you won't be able to push any commits to the branch that are not signed and verified. For more information, see "About commit signature verification" and "About protected branches."
- If you use GitHub's conflict editor to fix conflicts for a pull request that you created from a protected branch, GitHub helps you to create an alternative branch for the pull request, so that your resolution of the conflicts can be merged. For more information, see "Resolving a merge conflict on GitHub." [Resolving a merge conflict on Github](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github)

## Create and delete branches

[Create and Delete branches](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository)
