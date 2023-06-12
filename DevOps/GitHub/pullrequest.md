Back: [Table contents](./1-tablecontent.md)

# Pull Request

Pull requests let you tell others about changes you've pushed to a branch in a repository on GitHub. Once a pull request is opened, you can discuss and review the potential changes with collaborators and add follow-up commits before your changes are merged into the base branch.

After initializing a pull request, you'll see a review page that shows a high-level overview of the changes between your branch (the compare branch) and the repository's base branch. You can add a summary of the proposed changes, review the changes made by commits, add labels, milestones, and assignees, and @mention individual contributors or teams.

Once you've created a pull request, you can push commits from your topic branch to add them to your existing pull request. These commits will appear in chronological order within your pull request and the changes will be visible in the "Files changed" tab.

### More information:

- [Video - Update Pull request with mew changes](https://www.youtube.com/watch?v=Hi2mRlmasCU)

Other contributors can review your proposed changes, add review comments, contribute to the pull request discussion, and even add commits to the pull request. Organization owners and repository admins can limit who is able to give approving pull request reviews or request changes.

You can see information about the branch's current deployment status and past deployment activity on the "Conversation" tab.

After you're happy with the proposed changes, you can merge the pull request. If you're working in a shared repository model, you create a pull request and you, or someone else, will merge your changes from your feature branch into the base branch you specify in your pull request.

If status checks are required for a repository, the required status checks must pass before you can merge your branch into the protected branch.

You can link a pull request to an issue to show that a fix is in progress and to automatically close the issue when someone merges the pull request.

You can visit your dashboard to quickly find links to recently updated pull requests you're working on or subscribed to.

## Draft pull requests

When you create a pull request, you can choose to create a pull request that is ready for review or a draft pull request. Draft pull requests cannot be merged, and code owners are not automatically requested to review draft pull requests.

When you're ready to get feedback on your pull request, you can mark your draft pull request as ready for review. Marking a pull request as ready for review will request reviews from any code owners. You can convert a pull request to a draft at any time.

## Differences between commits on compare and pull request pages

---

The compare and pull request pages use different methods to calculate the diff for changed files:

- Compare pages show the diff between the tip of the head ref and the current common ancestor (that is, the merge base) of the head and base ref.
- Pull request pages show the diff between the tip of the head ref and the common ancestor of the head and base ref at the time when the pull request was created. Consequently, the merge base used for the comparison might be different.

## Working with branches

---

### More information:

- [Branches](./branches.md)

Once you're satisfied with your work, you can open a pull request to merge the changes in the current branch (the head branch) into another branch (the base branch).

After a pull request has been merged, or closed, you can delete the head branch as this is no longer needed. You must have write access in the repository to delete branches. You can't delete branches that are directly associated with open pull requests.

If you delete a head branch after its pull request has been merged, GitHub checks for any open pull requests in the same repository that specify the deleted branch as their base branch. GitHub automatically updates any such pull requests, changing their base branch to the merged pull request's base branch. The following diagrams illustrate this.

Here someone has created a branch called feature1 from the main branch, and you've then created a branch called feature2 from feature1. There are open pull requests for both branches. The arrows indicate the current base branch for each pull request. At this point, feature1 is the base branch for feature2. If the pull request for feature2 is merged now, the feature2 branch will be merged into feature1.

### More information:

- [Branches example](https://docs.github.com/assets/cb-2058/mw-1440/images/help/branches/pr-retargeting-diagram1.webp)

In the next diagram, someone has merged the pull request for feature1 into the main branch, and they have deleted the feature1 branch. As a result, GitHub has automatically retargeted the pull request for feature2 so that its base branch is now main.

### More information:

- [Branches example 2](https://docs.github.com/assets/cb-2581/mw-1440/images/help/branches/pr-retargeting-diagram2.webp)

Now when you merge the feature2 pull request, it'll be merged into the main branch.

## About comparing branches in pull request

---

Pull requests display diffs to compare the changes you made in your topic branch against the base branch that you want to merge your changes into.

You can view proposed changes in a pull request in the Files changed tab.

Rather than viewing the commits themselves, you can view the proposed changes as they'll appear in the files once the pull request is merged. The files appear in alphabetical order within the Files changed tab. Additions to the files appear in green and are prefaced by a + sign while content that has been removed appears in red and is prefaced by a - sign.

## Diff view options

---

You have several options for viewing a diff:

- The unified view shows updated and existing content together in a linear view.
- The split view shows old content on one side and new content on the other side.
- The rich diff view shows a preview of how the changes will look once the pull request is merged.
- The source view shows the changes in source without the formatting of the rich diff view.

You can also choose to ignore whitespace changes to get a more accurate view of the substantial changes in a pull request.

### More information:

- [Unified and Split View](https://docs.github.com/assets/cb-186190/mw-1440/images/help/pull_requests/diff-settings-menu.webp)

To simplify reviewing changes in a large pull request, you can filter the diff to only show selected file types, show files you are a CODEOWNER of, hide files you have already viewed, or hide deleted files.

### More information:

- [Filter by extension](https://docs.github.com/assets/cb-48471/mw-1440/images/help/pull_requests/file-filter-menu.webp)

## Three-dot and two-dot Git diff comparisons

---

There are two comparison methods for the git diff command; two-dot (git diff A..B) and three-dot (git diff A...B). By default, pull requests on GitHub show a three-dot diff.

## Three-dot Git diff comparison

---

The three-dot comparison shows the difference between the latest common commit of both branches (merge base) and the most recent version of the topic branch.

## Two-dot Git diff comparison

---

The two-dot comparison shows the difference between the latest state of the base branch (for example, main) and the most recent version of the topic branch.

To see two committish references in a two-dot diff comparison on GitHub, you can edit the URL of your repository's "Comparing changes" page.

or example, this URL uses the shortened seven-character SHA codes to compare commits f75c570 and 3391dcc: https://github.com/github-linguist/linguist/compare/f75c570..3391dcc.

A two-dot diff compares two Git committish references, such as SHAs or OIDs (Object IDs), directly with each other. On GitHub, the Git committish references in a two-dot diff comparison must be pushed to the same repository or its forks.

If you want to simulate a two-dot diff in a pull request and see a comparison between the most recent versions of each branch, you can merge the base branch into your topic branch, which updates the last common ancestor between your branches.

### More information:

- [Git diff options](https://git-scm.com/docs/git-diff#git-diff-emgitdiffemltoptionsgtltcommitgtltcommitgt--ltpathgt82308203)
- [Difference between 2 dots and 3 dots](https://www.youtube.com/watch?v=WRXmm-E77aY)
- [Explaning Git Diff](https://www.youtube.com/watch?v=vXN50AmJjgY)

### Merging often

---

To avoid getting confused, merge the base branch (for example, main) into your topic branch frequently. By merging the base branch, the diffs shown by two-dot and three-dot comparisons are the same. We recommend merging a pull request as soon as possible. This encourages contributors to make pull requests smaller, which is recommended in general.

## Creating a pull request

---

Create a pull request to propose and collaborate on changes to a repository. These changes are proposed in a branch, which ensures that the default branch only contains finished and approved work.

You can specify which branch you'd like to merge your changes into when you create your pull request. Pull requests can only be opened between two branches that are different.

You can link a pull request to an issue to show that a fix is in progress and to automatically close the issue when someone merges the pull request.

### More information:

- [Changing the branch range and destination repository](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

## Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. In the "Branch" menu, choose the branch that contains your commits.
3. Above the list of files, in the yellow banner, click Compare & pull request to create a pull request for the associated branch.
4. Use the base branch dropdown menu to select the branch you'd like to merge your changes into, then use the compare branch drop-down menu to choose the topic branch you made your changes in.
5. Type a title and description for your pull request.
6. To create a pull request that is ready for review, click Create Pull Request. To create a draft pull request, use the drop-down and select Create Draft Pull Request, then click Draft Pull Request. For more information about draft pull requests, see "About pull requests."

After your pull request has been reviewed, it can be merged into the repository.

### More information:

[Creating a pull request video](https://www.youtube.com/watch?v=UpBpb0j7IKA)

## Creating a pull request from a fork

---

You can create a pull request to propose changes you've made to a fork of an upstream repository.

If your pull request compares your topic branch with a branch in the upstream repository as the base branch, then your topic branch is also called the compare branch of the pull request.

### Process' checklist

1. Navigate to the original repository where you created your fork.
2. Above the list of files, in the yellow banner, click Compare & pull request to create a pull request for the associated branch.
3. On the page to create a new pull request, click compare across forks.
4. In the "base branch" dropdown menu, select the branch of the upstream repository you'd like to merge changes into.
5. In the "head fork" dropdown menu, select your fork, then use the "compare branch" drop-down menu to select the branch you made your changes in.
6. Type a title and description for your pull request.
7. On user-owned forks, if you want to allow anyone with push access to the upstream repository to make changes to your pull request, select Allow edits from maintainers.
8. To create a pull request that is ready for review, click Create Pull Request. To create a draft pull request, use the drop-down and select Create Draft Pull Request, then click Draft Pull Request.

## Using query parameters to create a pull request

---

Use query parameters to create custom URLs to open pull requests with pre-populated fields.

You can also create pull request templates that open with default labels, assignees, and an pull request.

### More information:

- [Using template to encourage pull request](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests)

You must have the proper permissions for any action to use the equivalent query parameter. For example, you must have permission to add a label to a pull request to use the labels query parameter.

If you create an invalid URL using query parameters, or if you don’t have the proper permissions, the URL will return a 404 Not Found error page. If you create a URL that exceeds the server limit, the URL will return a 414 URI Too Long error page.

### More information:

- [Query parameters to create a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/using-query-parameters-to-create-a-pull-request)

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the "Pull requests" list, click the pull request you'd like to mark as ready for review.
3. In the merge box, click Ready for review.

### Converting a pull request to a draft

---

You can convert a pull request to a draft at any time. For example, if you accidentally opened a pull request instead of a draft, or if you've received feedback on your pull request that needs to be addressed, you can convert the pull request to a draft to indicate further changes are needed. No one can merge the pull request until you mark the pull request as ready for review again. People who are already subscribed to notifications for the pull request will not be unsubscribed when you convert the pull request to a draft.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the "Pull requests" list, click the pull request you'd like to convert to a draft.
3. In the right sidebar, under "Reviewers," click Convert to draft.
4. Click Convert to draft.

## Changing the stage of a pull request

---

You can mark a draft pull request as ready for review or convert a pull request to a draft.

When you're ready to get feedback on your pull request, you can mark your draft pull request as ready for review. Marking a pull request as ready for review will request reviews from any code owners.

## Requesting a pull request review

---

After you create a pull request, you can ask a specific person to review the changes you've proposed. If you're an organization member, you can also request a specific team to review your changes.

Owners and collaborators on a repository owned by a personal account can assign pull request reviews. Organization members with triage permissions can also assign a reviewer for a pull request.

To assign a reviewer to a pull request, you will need write access to the repository.

If you have write access, you can assign anyone who has read access to the repository as a reviewer.

Organization members with write access can also assign a pull request review to any person or team with read access to a repository. The requested reviewer or team will receive a notification that you asked them to review the pull request. If you request a review from a team and code review assignment is enabled, specific members will be requested and the team will be removed as a reviewer.

Pull request authors can't request reviews unless they are either a repository owner or collaborator with write access to the repository.

You can request a review from either a suggested or specific person. Suggested reviewers are based on git blame data. If you request a review, other people with read access to the repository can still review your pull request. Once someone has reviewed your pull request and you've made the necessary changes, you can re-request review from the same reviewer. If the requested reviewer does not submit a review, and the pull request meets the repository's mergeability requirements, you can still merge the pull request.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request that you'd like to ask a specific person or a team to review.
3. To request a review from a suggested person under Reviewers, next to their username, click Request.
4. Optionally, to request a review from someone other than a suggested person, click Reviewers. If you know the name of the person or team you'd like a review from, type the username of the person or the name of the team you're asking to review your changes. Click their team name or username to request a review.
5. After your pull request is reviewed and you've made the necessary changes, you can ask a reviewer to re-review your pull request. Navigate to Reviewers in the right sidebar and click next to the reviewer's name whose review you'd like.

## Keeping your pull request in sync with the base branch

---

After you open a pull request, you can update the head branch, which contains your changes, with any changes that have been made in the base branch.

Before merging your pull requests, other changes may get merged into the base branch causing your pull request's head branch to be out of sync.

Updating your pull request with the latest changes from the base branch can help catch problems prior to merging.

You can update a pull request's head branch from the command line or the pull request page. The Update branch button is displayed when all of these are true:

- There are no merge conflicts between the pull request branch and the base branch.
- The pull request branch is not up to date with the base branch.
- The base branch requires branches to be up to date before merging or the setting to always suggest updating branches is enabled.

If there are changes to the base branch that cause merge conflicts in your pull request branch, you will not be able to update the branch until all conflicts are resolved.

From the pull request page you can update your pull request's branch using a traditional merge or by rebasing. A traditional merge results in a merge commit that merges the base branch into the head branch of the pull request.

Rebasing applies the changes from your branch onto the latest version of the base branch. The result is a branch with a linear history, since no merge commit is created.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the "Pull requests" list, click the pull request you'd like to update.
3. In the merge section near the bottom of the page, you can:
   1. Click Update branch to perform a traditional merge.
   2. Click the update branch drop down menu, click Update with rebase, and then click Rebase branch to update by rebasing on the base branch.

### More information:

- [Keep in sync with pullrequest changes](https://www.youtube.com/watch?v=M7ZYkjOWr6g)

## Changing the base branch of a pull request

---

After a pull request is opened, you can change the base branch to compare
the changes in the pull request against a different branch.

### Process' checklist:

1. Under your repository name, click Pull requests.
2. In the "Pull Requests" list, click the pull request you'd like to modify.
3. Next to the pull request's title, click Edit.
4. In the base branch drop-down menu, select the base branch you'd like to compare changes against.
5. Read the information about changing the base branch and click Change base.

## Committing changes to a pull request branch created from a fork

---

You can commit changes on a pull request branch that was created from a fork of your repository with permission from the pull request creator.

You can only make commits on pull request branches that:

- are opened in a repository that you have push access to and that were created from a fork of that repository
- are on a user-owned fork
- have permission granted from the pull request creator
- don't have branch restrictions that will prevent you from committing
  Only the user who created the pull request can give you permission to push commits to the user-owned fork.

### Process' checklist

1. On GitHub, navigate to the main page of the fork (or copy of your repository) where the pull request branch was created.
2. Above the list of files, click Code.
3. Copy the URL for the repository.
   1. To clone the repository using HTTPS, under "HTTPS", click .
   2. To clone the repository using an SSH key, including a certificate issued by your organization's SSH certificate authority, click SSH, then click .
   3. To clone a repository using GitHub CLI, click GitHub CLI, then click .
4. Open Git Bash.
5. Change the current working directory to the location where you want to download the cloned directory.
6. Type git clone, and then paste the URL you copied in Step 3.
7. Press Enter. Your local clone will be created.
8. Navigate into your new cloned repository.
9. Switch branches to the compare branch of the pull request where the original changes were made. If you navigate to the original pull request, you'll see the compare branch at the top of the pull request.

In this example, the compare branch is test-branch:

```
    $ git checkout TEST-BRANCH
```

10. At this point, you can do anything you want with this branch. You can push new commits to it, run some local tests, or merge other branches into the branch. Make modifications as you like.
11. After you commit your changes to the head branch of the pull request you can push your changes up to the original pull request directly. In this example, the head branch is test-branch:

```
$ git push origin test-branch
> Counting objects: 32, done.
> Delta compression using up to 8 threads.
> Compressing objects: 100% (26/26), done.
> Writing objects: 100% (29/29), 74.94 KiB | 0 bytes/s, done.
> Total 29 (delta 8), reused 0 (delta 0)
> To https://github.com/USERNAME/FORK-OF-THE-REPOSITORY.git
> 12da2e9..250e946  TEST-BRANCH -> TEST-BRANCH

```

Your new commits will be reflected on the original pull request on GitHub.com.

## About collaborative development models

---

The way you use pull requests depends on the type of development model you use in your project. You can use the fork and pull model or the shared repository model.

You can use query parameters to open pull requests. Query parameters are optional parts of a URL you can customize to share a specific web page view, such as search filter results or a pull request template on GitHub. To create your own query parameters, you must match the key and value pair.

## Fork an pull model

---

In the fork and pull model, anyone can fork an existing repository and push changes to their personal fork. You do not need permission to the source repository to push to a user-owned fork. The changes can be pulled into the source repository by the project maintainer. When you open a pull request proposing changes from your user-owned fork to a branch in the source (upstream) repository, you can allow anyone with push access to the upstream repository to make changes to your pull request. This model is popular with open source projects as it reduces the amount of friction for new contributors and allows people to work independently without upfront coordination.

### More information:

- [Open Source Guides](https://opensource.guide/)
- [Github Skills](https://skills.github.com/)

## Shared repository model

---

In the shared repository model, collaborators are granted push access to a single shared repository and topic branches are created when changes need to be made. Pull requests are useful in this model as they initiate code review and general discussion about a set of changes before the changes are merged into the main development branch. This model is more prevalent with small teams and organizations collaborating on private projects.

## About status checks

---

Status checks let you know if your commits meet the conditions set for the repository you're contributing to.

Status checks are based on external processes, such as continuous integration builds, which run for each push you make to a repository.

You can see the pending, passing, or failing state of status checks next to individual commits in your pull request.

Anyone with write permissions to a repository can set the state for any status check in the repository.

You can see the overall state of the last commit to a branch on your repository's branches page or in your repository's list of pull requests.

If status checks are required for a repository, the required status checks must pass before you can merge your branch into the protected branch.

### More information:

- [About protected repositories](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-before-merging)

## Types of status checks on GitHub

There are two types of status checks on GitHub:

- Checks
- Statuses

Checks are different from statuses in that they provide line annotations, more detailed messaging, and are only available for use with GitHub Apps.

Organization owners and users with push access to a repository can create checks and statuses with GitHub's API.

### Checks

When checks are set up in a repository, pull requests have a Checks tab where you can view detailed build output from status checks and rerun failed checks.

When a specific line in a commit causes a check to fail, you will see details about the failure, warning, or notice next to the relevant code in the Files tab of the pull request.

You can navigate between the checks summaries for various commits in a pull request, using the commit drop-down menu under the Checks tab.

### More information:

- [Checks](https://docs.github.com/assets/cb-345021/mw-1440/images/help/pull_requests/checks-summary-for-various-commits.webp)
- [Skipping checks for individual commits](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks#skipping-and-requesting-checks-for-individual-commits)

You can also skip workflow runs triggered by the push and pull_request events by including a command in your commit message.

### More information:

- [Skipping workflow runs](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs)

### Retention of status checks

---

GitHub.com retains check data for 400 days. After 400 days, the data is archived.

For archived check data, a rollup commit status appears that represents the state of all of the checks for the commit. To merge a pull request with checks that are both required and archived, you must rerun the checks.

## Working with protected branches

---

Repository administrators or custom roles with the "edit repository rules" permission can enable protections on a branch. If you're working on a branch that's protected, you won't be able to delete or force push to the branch. Repository administrators can additionally enable several other protected branch settings to enforce various workflows before a branch can be merged.

To see if your pull request can be merged, look in the merge box at the bottom of the pull request's Conversation tab.

When a branch is protected:

- You won't be able to delete or force push to the branch.
- If required status checks are enabled on the branch, you won't be able to merge changes into the branch until all of the required CI tests pass. For more information, see "About status checks."
- If required pull request reviews are enabled on the branch, you won't be able to merge changes into the branch until all requirements in the pull request review policy have been met. For more information, see "Merging a pull request."
- If required review from a code owner is enabled on a branch, and a pull request modifies code that has an owner, a code owner must approve the pull request before it can be merged. For more information, see "About code owners."
- If required commit signing is enabled on a branch, you won't be able to push any commits to the branch that are not signed and verified. For more information, see "About commit signature verification" and "About protected branches."
- If you use GitHub's conflict editor to fix conflicts for a pull request that you created from a protected branch, GitHub helps you to create an alternative branch for the pull request, so that your resolution of the conflicts can be merged.

### More information:

- [Resolving a merge conflict on Github](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github)
- [Restrictions for a branch](https://www.youtube.com/watch?v=rYwwz1b2Nss)

## Create and delete branches

---

### More information:

- [Create and Delete branches](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository)
- [Branches](./branches.md)
