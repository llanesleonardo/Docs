Back: [Pull Requests](./pullrequest.md)

# Reviews

## About pull request reviews

---

Reviews allow collaborators to comment on the changes proposed in pull requests, approve the changes, or request further changes before the pull request is merged. Repository administrators can require that all pull requests are approved before being merged.

After a pull request is opened, anyone with read access can review and comment on the changes it proposes. You can also suggest specific changes to lines of code, which the author can apply directly from the pull request.

By default, in public repositories, any user can submit reviews that approve or request changes to a pull request. Organization owners and repository admins can limit who is able to give approving pull request reviews or request changes.

Repository owners and collaborators can request a pull request review from a specific person. Organization members can also request a pull request review from a team with read access to the repository. You can specify a subset of team members to be automatically assigned in the place of the whole team.

Reviews allow for discussion of proposed changes and help ensure that the changes meet the repository's contributing guidelines and other quality standards. You can define which individuals or teams own certain types or areas of code in a CODEOWNERS file. When a pull request modifies code that has a defined owner, that individual or team will automatically be requested as a reviewer.

You can schedule reminders for pull requests that need to be reviewed.

A review has three possible statuses:

- Comment: Submit general feedback without explicitly approving the changes or requesting additional changes.
- Approve: Submit feedback and approve merging the changes proposed in the pull request.
- Request changes: Submit feedback that must

You can view all of the reviews a pull request has received in the Conversation timeline, and you can see reviews by repository owners and collaborators in the pull request's merge box.

## Resolving conversations

---

You can resolve a conversation in a pull request if you opened the pull request or if you have write access to the repository where the pull request was opened.

To indicate that a conversation on the Files changed tab is complete, click Resolve conversation.

The entire conversation will be collapsed and marked as resolved, making it easier to find conversations that still need to be addressed.

If the suggestion in a comment is out of your pull request's scope, you can open a new issue that tracks the feedback and links back to the original comment.

## Discovering and navigating conversations

---

You can discover and navigate to all the conversations in your pull request using the Conversations menu that's shown at the top of the Files Changed tab.

From this view, you can see which conversations are unresolved, resolved, and outdated. This makes it easy to discover and resolve conversations.

## Re-requesting a review

---

You can re-request a review, for example, after you've made substantial changes to your pull request. To request a fresh review from a reviewer, in the sidebar of the Conversation tab, click the (refresh icon).

## Required reviews

---

Repository administrators or custom roles with the "edit repository rules" permission can require that all pull requests receive a specific number of approving reviews before someone merges the pull request into a protected branch. You can require approving reviews from people with write permissions in the repository or from a designated code owner.

## Reviewing proposed changes in a pull request

---

In a pull request, you can review and discuss commits, changed files, and the differences (or "diff") between the files in the base and compare branches.

You can review changes in a pull request one file at a time. While reviewing the files in a pull request, you can leave individual comments on specific changes. After you finish reviewing each file, you can mark the file as viewed. This collapses the file, helping you identify the files you still need to review. A progress bar in the pull request header shows the number of files you've viewed. After reviewing as many files as you want, you can approve the pull request or request additional changes by submitting your review with a summary comment.

## Starting a review

---

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to review.
3. On the pull request, click Files changed.

You can change the format of the diff view in this tab by clicking and choosing the unified or split view. The choice you make will apply when you view the diff for other pull requests.

You can also choose to hide whitespace differences. The choice you make only applies to this pull request and will be remembered the next time you visit this page.

4. Optionally, filter the files to show only the files you want to review or use the file tree to navigate to a specific file.
5. Hover over the line of code where you'd like to add a comment, and click the blue comment icon. To add a comment on multiple lines, click and drag to select the range of lines, then click the blue comment icon.
6. In the comment field, type your comment.
7. Optionally, to suggest a specific change to the line or lines, click , then edit the text within the suggestion block.
8. To comment directly on a file, to the right of the file, click and type your comment.
9. When you're done, click Start a review. If you have already started a review, you can click Add review comment.

Before you submit your review, your line comments are pending and only visible to you. You can edit pending comments anytime before you submit your review. To cancel a pending review, including all of its pending comments, click Review changes above the changed code, then click Cancel review.

### Reviewing dependency changes

---

If the pull request contains changes to dependencies you can use the dependency review for a manifest or lock file to see what has changed and check whether the changes introduce security vulnerabilities.

### Process' checklist

1. On the pull request, click Files changed.
2. On the right of the header for a manifest or lock file, display the dependency review by clicking the rich diff button.
3. You may also want to review the source diff, because there could be changes to the manifest or lock file that don't change dependencies, or there could be dependencies that GitHub can't parse and which, as a result, don't appear in the dependency review.

### Marking a file as viewed

---

After you finish reviewing a file, you can mark the file as viewed, and the file will collapse. If the file changes after you view the file, it will be unmarked as viewed.

### Process' checklist

1. On the pull request, click Files changed.
2. On the right of the header of the file you've finished reviewing, select Viewed.

### Submitting your review

---

After you've finished reviewing all the files you want in the pull request, submit your review.

### Process' checklist

1. On the pull request, click Files changed.
2. Above the changed code, click Review changes.
3. Type a comment summarizing your feedback on the proposed changes.
4. Select the type of review you'd like to leave:
   1. Select Comment to leave general feedback without explicitly approving the changes or requesting additional changes.
   2. Select Approve to submit your feedback and approve merging the changes proposed in the pull request.
   3. Select Request changes to submit feedback that must be addressed before the pull request can be merged.
5. Click Submit review.

## Filtering files in a pull request

---

To help you quickly review changes in a large pull request, you can filter changed files or use the file tree to navigate between files.

You can filter files in a pull request by file extension type, such as .html or .js, lack of an extension, code ownership, or dotfiles. You can also use the file tree to filter by file path, navigate between files, or see a high level view of the changed files.

## Using the file filter dropdown

---

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to filter.
3. On the pull request, click Files changed.
4. Use the File filter dropdown menu, and select, deselect, or click the desired filters.
5. Optionally, to clear the filter selection, under the Files changed tab, click Clear filters.

## Using the file tree

---

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to filter.
3. On the pull request, click Files changed.
4. Click on a file in the file tree to view the corresponding file diff. If the file tree is hidden, click to display the file tree.
5. To filter by file path, enter part or all of the file path in the Filter changed files search box. Alternatively, use the file filter dropdown.

## Finding changed methods and functions in a pull request

---

You can quickly find proposed changes to a method or function in a pull request in .go, .js, .ts, .py, .php, and .rb files.

Anyone with read access to a repository can see a summary list of the functions and methods changes in certain files of a pull request.

The summary list of methods and functions is created from these supported file types:

- Go
- JavaScript (includes Typescript, Flow, and other types of JavaScript)
- PHP
- Python
- Ruby

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request where you'd like to find the changed functions and methods.
3. On the pull request, click Files changed.
4. To see a summary list of the changed functions and methods, click Jump to.
5. Select the changed function or method from the drop-down menu. You can also enter the name of the function or method to filter results.
6. You'll be redirected to the first line of the function or method you selected.

## Commenting on a pull request

---

After you open a pull request in a repository, collaborators or team members can comment on the comparison of files between the two specified branches, or leave general comments on the project as a whole.

You can comment on a pull request's Conversation tab to leave general comments, questions, or props. You can also suggest changes that the author of the pull request can apply directly from your comment.

You can also comment on specific files or sections of a file in a pull request's Files changed tab in the form of individual line or file comments, or as part of a pull request review. Adding line or file comments is a great way to discuss questions about implementation or provide feedback to the author.

To reply to an existing line or file comment, you'll need to navigate to the comment on either the Conversation tab or Files changed tab and add an additional comment below it.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request where you'd like to leave line comments.
3. On the pull request, click Files changed.
4. Hover over the line of code where you'd like to add a comment, and click the blue comment icon. To add a comment on multiple lines, click and drag to select the range of lines, then click the blue comment icon.
5. In the comment field, type your comment.
6. Optionally, to suggest a specific change to the line or lines, click , then edit the text within the suggestion block.
7. To comment directly on a file, to the right of the file, click and type your comment.
8. When you're done, click Add single comment.

Anyone watching the pull request or repository will receive a notification of your comment.

## Viewing a pull request review

---

You can view all of the comments made in a single pull request review.

You can find a pull request where you or a team you're a member of is requested for review with the search qualifier review-requested:[USERNAME] or team-review-requested:[TEAMNAME].

When you view a full review, you'll see the same version of the pull request as the reviewer did at the time of the review.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to review.
3. On the "Conversation" tab, scroll to the review you'd like to see, then click View changes.

## Reviewing dependency changes in a pull request

---

If a pull request contains changes to dependencies, you can view a summary of what has changed and whether there are known vulnerabilities in any of the dependencies.

Dependency review helps you understand dependency changes and the security impact of these changes at every pull request. It provides an easily understandable visualization of dependency changes with a rich diff on the "Files Changed" tab of a pull request. Dependency review informs you of:

- Which dependencies were added, removed, or updated, along with the release dates.
- How many projects use these components.
- Vulnerability data for these dependencies.

Dependency review allows you to "shift left". You can use the provided predictive information to catch vulnerable dependencies before they hit production.

You can use the dependency review action to help enforce dependency reviews on pull requests in your repository. The dependency review action scans your pull requests for dependency changes and raises an error if any new dependencies have known vulnerabilities.

The action is supported by an API endpoint that compares the dependencies between two revisions and reports any differences.

You can configure the dependency review action to better suit your needs by specifying the type of dependency vulnerability you wish to catch.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to review.
3. On the pull request, click Files changed.
4. If the pull request contains many files, use the File filter drop-down menu to collapse all files that don't record dependencies. This will make it easier to focus your review on the dependency changes.

The dependency review provides a clearer view of what has changed in large lock files, where the source diff is not rendered by default.

5. On the right of the header for a manifest or lock file, display the dependency review by clicking .
6. Check the dependencies listed in the dependency review.

Any added or changed dependencies that have vulnerabilities are listed first, ordered by severity and then by dependency name. This means that the highest severity dependencies are always at the top of a dependency review. Other dependencies are listed alphabetically by dependency name.

The icon beside each dependency indicates whether the dependency has been added (), updated (), or removed () in this pull request.

Other information includes:

- The version, or version range, of the new, updated, or deleted dependency.

For a specific version of a dependency:

- The age of that release of the dependency.
- The number of projects that are dependent on this software. This information is taken from the dependency graph. Checking the number of dependents can help you avoid accidentally adding the wrong dependency.
- The license used by this dependency, if this information is available. This is useful if you want to avoid code with certain licenses being used in your project.

Where a dependency has a known vulnerability, the warning message includes:

- A brief description of the vulnerability.
- A Common Vulnerabilities and Exposures (CVE) or GitHub Security
- Advisories (GHSA) identification number. You can click this ID to find out more about the vulnerability.
- The severity of the vulnerability.
- The version of the dependency in which the vulnerability was fixed. If you are reviewing a pull request for someone, you might ask the contributor to update the dependency to the patched version, or a later release.

7. You may also want to review the source diff, because there could be changes to the manifest or lock file that don't change dependencies, or there could be dependencies that GitHub can't parse and which, as a result, don't appear in the dependency review.

To return to the source diff view, click the button.

## Incorporating feedback in your pull request

---

When reviewers suggest changes in a pull request, you can automatically incorporate the changes into the pull request or open an issue to track out-of-scope suggestions.

Other people can suggest specific changes to your pull request. You can apply these suggested changes directly in a pull request if you have write access to the repository. If the pull request was created from a fork and the author allowed edits from maintainers, you can also apply suggested changes if you have write access to the upstream repository.

To quickly incorporate more than one suggested change into a single commit, you can also apply suggested changes as a batch. Applying one suggested change or a batch of suggested changes creates a single commit on the compare branch of the pull request.

Each person who suggested a change included in the commit will be a co-author of the commit. The person who applies the suggested changes will be a co-author and the committer of the commit.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to apply a suggested change to.
3. Navigate to the first suggested change you'd like to apply.
   1. To apply the change in its own commit, click Commit suggestion.
   2. To add the suggestion to a batch of changes, click Add suggestion to batch. Continue to add the suggested changes you want to include in a single commit. When you've finished adding suggested changes, click Commit suggestions.
4. In the commit message field, type a short, meaningful commit message that describes the change you made to the file or files.
5. Click Commit changes.

### More information:

- [Open a commit suggestion](https://www.youtube.com/watch?v=AFWwVPrULaY)

## Re-requesting a review

---

You can re-request a review, for example, after you've made substantial changes to your pull request. To request a fresh review from a reviewer, in the sidebar of the Conversation tab, click the (refresh icon).

## Opening an issue for an out-of-scope suggestion

---

If someone suggests changes to your pull request and the changes are out of the pull request's scope, you can open a new issue to track the feedback.

## Approving a pull request with required reviews

---

If your repository requires reviews, pull requests must have a specific number of approving reviews from people with write or admin permissions in the repository before they can be merged.

You can comment on a pull request, approve the changes, or request improvements before approving.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to review.
3. On the pull request, click Files changed.
4. Review the changes in the pull request, and optionally, comment on specific lines or files.
5. Above the changed code, click Review changes.
6. Type a comment summarizing your feedback on the proposed changes.
7. Select Approve to approve merging the changes proposed in the pull request.
8. Click Submit review.

## Dismissing a pull request review

---

If your repository requires reviews, you can dismiss pull request reviews that are no longer valid or are unable to be approved by the reviewer.

If a pull request has changed since it was reviewed and the person who requested changes isn't available to give an approving review, repository administrators or people with write access can dismiss a review. This changes the status of the review to a review comment. When you dismiss a review, you must add a comment explaining why you dismissed it. Your comment will be added to the pull request conversation.

### Process checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to review.
3. On the "Conversation" tab, next to the summary of reviews, click .
4. Next. to the review you'd like to dismiss, select the dropdown menu, then click Dismiss review.
5. Type your reason for dismissing the review, then click Dismiss review.

## Checking out pull requests locally

---

When someone sends you a pull request from a fork or branch of your repository, you can merge it locally to resolve a merge conflict or to test and verify the changes before merging on GitHub.

To Modify an active pull request locally:

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the list of pull requests, click the pull request you'd like to modify.
3. To choose where you'd like to open the pull request, select the Code dropdown and click one of the tabs.

To Modify an inactive pull request locally:

- If a pull request's author is unresponsive to requests or has deleted their fork, the pull request can still be merged. However, if you want to make changes to a pull request and the author is not responding, you'll need to perform some additional steps to update the pull request.
- Once a pull request is opened, GitHub stores all of the changes remotely. In other words, commits in a pull request are available in a repository even before the pull request is merged. You can fetch an open pull request and recreate it as your own.
- Anyone can work with a previously opened pull request to continue working on it, test it out, or even open a new pull request with additional changes. However, only collaborators with push access can merge pull requests.

1. Under your repository name, click Issues or Pull requests.
2. In the "Pull Requests" list, click the pull request you'd like to merge.
3. Find the ID number of the inactive pull request. This is the sequence of digits right after the pull request's title.
4. Git Bash.
5. Fetch the reference to the pull request based on its ID number, creating a new branch in the process.
6. Switch to the new branch that's based on this pull request:

```
$ git fetch origin pull/ID/head:BRANCH_NAME
```

7. At this point, you can do anything you want with this branch. You can run some local tests, or merge other branches into the branch.
8. When you're ready, you can push the new branch up:

```
[pull-inactive-pull-request] $ git push origin BRANCH_NAME
> Counting objects: 32, done.
> Delta compression using up to 8 threads.
> Compressing objects: 100% (26/26), done.
> Writing objects: 100% (29/29), 74.94 KiB | 0 bytes/s, done.
> Total 29 (delta 8), reused 0 (delta 0)
> To https://github.com/USERNAME/REPOSITORY.git
>  * [new branch]      BRANCH_NAME -> BRANCH_NAME
```

9. Create a new pull request with your new branch.
