# Commits

You can save small groups of meaningful changes as commits.

Similar to saving a file that's been edited, a commit records changes to one or more files in your branch. Git assigns each commit a unique ID, called a SHA or hash, that identifies:

- The specific changes
- When the changes were made
- Who created the changes

When you make a commit, you must include a commit message that briefly describes the changes.

If the repository you are committing to has compulsory commit signoffs enabled, and you are committing via the web interface, you will automatically sign off on the commit as part of the commit process.

You can add a co-author on any commits you collaborate on.

You can also create a commit on behalf of an organization.

Rebasing allows you to change a series of commits and can modify the order of the commits in your timeline.

## Commit branches and tag labels

You can see which branch a commit is on by looking at the labels beneath the commit on the commit page.

1. On GitHub.com, navigate to the main page of the repository.
2. On the main page of the repository, above the file list, click commits.
3. To navigate to a specific commit, click the commit message for that commit.
4. To see what branch the commit is on, check the label below the commit message.

If your commit is not on the default branch (main), the label will show the branches which contain the commit. If the commit is part of an unmerged pull request, you can click the link to go to the pull request.

Once the commit is on the default branch, any tags that contain the commit will be shown and the default branch will be the only branch listed

## Using the file tree

You can use the file tree to navigate between files in a commit.

1. On GitHub.com, navigate to the main page of the repository.
2. On the main page of the repository, above the file list, click commits.
3. To navigate to a specific commit, click the commit message for that commit.
4. Click on a file in the file tree to view the corresponding file diff. If the file tree is hidden, click to display the file tree.
5. To filter by file path, enter part or all of the file path in the Filter changed files search box.

## Creating a commit with multiple authors

You can attribute a commit to more than one author by adding one or more Co-authored-by trailers to the commit's message. Co-authored commits are visible on GitHub.
Before you can add a co-author to a commit, you must know the appropriate email to use for each co-author. For the co-author's commit to count as a contribution, you must use the email associated with their account on GitHub.com.

If a person chooses to keep their email address private, you should use their GitHub-provided no-reply email to protect their privacy. Otherwise, the co-author's email will be available to the public in the commit message. If you want to keep your email private, you can choose to use a GitHub-provided no-reply email for Git operations and ask other co-authors to list your no-reply email in commit trailers.

### Creating co-authored commits on the command line

1. Collect the name and email address for each co-author. If a person chooses to keep their email address private, you should use their GitHub-provided no-reply email to protect their privacy.
2. Type your commit message and a short, meaningful description of your changes. After your commit description, instead of a closing quotation, add two empty lines.
3. On the next line of the commit message, type Co-authored-by: name <name@example.com> with specific information for each co-author. After the co-author information, add a closing quotation mark.

If you're adding multiple co-authors, give each co-author their own line and Co-authored-by: commit trailer.

    $ git commit -m "Refactor usability tests.
    > Co-authored-by: NAME <NAME@EXAMPLE.COM>
    > Co-authored-by: ANOTHER-NAME <ANOTHER-NAME@EXAMPLE.COM>"

### Creating co-authored commits on GitHub

1. Collect the name and email address for each co-author. If a person chooses to keep their email address private, you should use their GitHub-provided no-reply email to protect their privacy.
2. Click Commit changes...
3. In the "Commit message" field, type a short, meaningful commit message that describes the changes you made.
4. In the text box below your commit message, add Co-authored-by: name <name@example.com> with specific information for each co-author. If you're adding multiple co-authors, give each co-author their own line and Co-authored-by: commit trailer.
5. Click Commit changes or Propose changes.

## Changing a commit message

If a commit message contains unclear, incorrect, or sensitive information, you can amend it locally and push a new commit with a new message to GitHub. You can also change a commit message to add missing information.

### Rewriting the most recent commit message

If a commit message contains unclear, incorrect, or sensitive information, you can amend it locally and push a new commit with a new message to GitHub. You can also change a commit message to add missing information.

You can change the most recent commit message using the git commit --amend command.

In Git, the text of the commit message is part of the commit. Changing the commit message will change the commit ID--i.e., the SHA1 checksum that names the commit. Effectively, you are creating a new commit that replaces the old one.

### Commit has not been pushed online

If the commit only exists in your local repository and has not been pushed to GitHub.com, you can amend the commit message with the git commit --amend command.

1. On the command line, navigate to the repository that contains the commit you want to amend.
2. Type git commit --amend and press Enter.
3. In your text editor, edit the commit message, and save the commit.
   1. You can add a co-author by adding a trailer to the commit. For more information, see "Creating a commit with multiple authors."
   2. You can create commits on behalf of your organization by adding a trailer to the commit. For more information, see "Creating a commit on behalf of an organization"

### Amending older or multiple commit messages

If you have already pushed the commit to GitHub.com, you will have to force push a commit with an amended message.
Changing the message of the most recently pushed commit

1. Follow the steps above to amend the commit message.
2. Use the push --force-with-lease command to force push over the old commit.

   $ git push --force-with-lease origin EXAMPLE-BRANCH

Changing the message of older or multiple commit messages

If you need to amend the message for multiple commits or an older commit, you can use interactive rebase, then force push to change the commit history.

1. On the command line, navigate to the repository that contains the commit you want to amend.
2. Use the git rebase -i HEAD~n command to display a list of the last n commits in your default text editor.

Displays a list of the last 3 commits on the current branch

    $ git rebase -i HEAD~3

The list will look similar to the following:

    pick e499d89 Delete CNAME
    pick 0c39034 Better README
    pick f7fde4a Change the commit message but push the same commit.

    # Rebase 9fdb3bd..f7fde4a onto 9fdb3bd
    #
    # Commands:
    # p, pick = use commit
    # r, reword = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    # s, squash = use commit, but meld into previous commit
    # f, fixup = like "squash", but discard this commit's log message
    # x, exec = run command (the rest of the line) using shell
    #
    # These lines can be re-ordered; they are executed from top to bottom.
    #
    # If you remove a line here THAT COMMIT WILL BE LOST.
    #
    # However, if you remove everything, the rebase will be aborted.
    #
    # Note that empty commits are commented out

3. Replace pick with reword before each commit message you want to change.
4. Save and close the commit list file.
5. In each resulting commit file, type the new commit message, save the file, and close it.
6. When you're ready to push your changes to GitHub, use the push --force command to force push over the old commit.

   $ git push --force origin EXAMPLE-BRANCH

## View & compare commits

You can compare the state of your repository across branches, tags, commits, forks, and dates.
To compare different versions of your repository, append /compare to your repository's path.

Every repository's Compare view contains two drop down menus: base and compare.

base should be considered the starting point of your comparison, and compare is the endpoint. During a comparison, you can always change your base and compare points by clicking on Edit.

### Comparing branches

The most common use of Compare is to compare branches, such as when you're starting a new pull request. You'll always be taken to the branch comparison view when starting a new pull request.

To compare branches, you can select a branch name from the compare drop down menu at the top of the page.

Here's an example of a comparison between two branches.

[A good example](https://github.com/octocat/linguist/compare/master...octocat:an-example-comparison-for-docs)

### Comparing tags

Comparing release tags will show you changes to your repository since the last release. For more information, see "Comparing releases."

To compare tags, you can select a tag name from the compare drop-down menu at the top of the page.

Here's an example of a comparison between two tags.

[A good example](https://github.com/octocat/linguist/compare/v2.2.0...octocat:v2.3.3)

### Comparing commits

You can also compare two arbitrary commits in your repository or its forks on GitHub in a two-dot diff comparison.

To quickly compare two commits or Git Object IDs (OIDs) directly with each other in a two-dot diff comparison on GitHub, edit the URL of your repository's "Comparing changes" page.

For example, this URL uses the shortened seven-character SHA codes to compare commits f75c570 and 3391dcc: https://github.com/github-linguist/linguist/compare/f75c570..3391dcc.

To learn more about other comparison options, see "About comparing branches in pull requests."

[A good example](https://github.com/github-linguist/linguist/compare/f75c570..3391dcc)

### Comparison across commits

[Comaprison across commits](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/viewing-and-comparing-commits/comparing-commits#comparisons-across-commits)

### Differences between commit views

[Difference between commit views](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/viewing-and-comparing-commits/differences-between-commit-views)

## Troubleshooting commits

Sometimes a commit will be viewable on GitHub, but will not exist in your local clone of the repository.

When you use git show to view a specific commit on the command line, you may get a fatal error.

For example, you may receive a bad object error locally:

    $ git show 1095ff3d0153115e75b7bca2c09e5136845b5592
    > fatal: bad object 1095ff3d0153115e75b7bca2c09e5136845b5592

However, when you view the commit on GitHub.com, you'll be able to see it without any problems:

    github.com/$account/$repository/commit/1095ff3d0153115e75b7bca2c09e5136845b5592

There are several possible explanations:

- The local repository is out of date.[Solution](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/troubleshooting-commits/commit-exists-on-github-but-not-in-my-local-clone#the-local-repository-is-out-of-date)
- The branch that contains the commit was deleted, so the commit is no longer referenced.[Solution](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/troubleshooting-commits/commit-exists-on-github-but-not-in-my-local-clone#the-branch-that-contained-the-commit-was-deleted)
- Someone force pushed over the commit. (Avoid force pushing to a repository unless absolutely necessary. This is especially true if more than one person can push to the repository. If someone force pushes to a repository, the force push may overwrite commits that other people based their work on. Force pushing changes the repository history and can corrupt pull requests.)

## Why are my commits linked to the wrong user?

[Why are my commits linked to the wrong user?](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/troubleshooting-commits/why-are-my-commits-linked-to-the-wrong-user)

[How to revert a commit on Github](https://www.youtube.com/watch?v=H2DuJNWbqLw)
