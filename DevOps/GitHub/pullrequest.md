# Pull Request

## Commits

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

### Commit branches and tag labels

You can see which branch a commit is on by looking at the labels beneath the commit on the commit page.

1. On GitHub.com, navigate to the main page of the repository.
2. On the main page of the repository, above the file list, click commits.
3. To navigate to a specific commit, click the commit message for that commit.
4. To see what branch the commit is on, check the label below the commit message.

If your commit is not on the default branch (main), the label will show the branches which contain the commit. If the commit is part of an unmerged pull request, you can click the link to go to the pull request.

Once the commit is on the default branch, any tags that contain the commit will be shown and the default branch will be the only branch listed

### Using the file tree

You can use the file tree to navigate between files in a commit.

1. On GitHub.com, navigate to the main page of the repository.
2. On the main page of the repository, above the file list, click commits.
3. To navigate to a specific commit, click the commit message for that commit.
4. Click on a file in the file tree to view the corresponding file diff. If the file tree is hidden, click to display the file tree.
5. To filter by file path, enter part or all of the file path in the Filter changed files search box.

### Creating a commit with multiple authors

You can attribute a commit to more than one author by adding one or more Co-authored-by trailers to the commit's message. Co-authored commits are visible on GitHub.
Before you can add a co-author to a commit, you must know the appropriate email to use for each co-author. For the co-author's commit to count as a contribution, you must use the email associated with their account on GitHub.com.

If a person chooses to keep their email address private, you should use their GitHub-provided no-reply email to protect their privacy. Otherwise, the co-author's email will be available to the public in the commit message. If you want to keep your email private, you can choose to use a GitHub-provided no-reply email for Git operations and ask other co-authors to list your no-reply email in commit trailers.

#### Creating co-authored commits on the command line

1. Collect the name and email address for each co-author. If a person chooses to keep their email address private, you should use their GitHub-provided no-reply email to protect their privacy.
2. Type your commit message and a short, meaningful description of your changes. After your commit description, instead of a closing quotation, add two empty lines.
3. On the next line of the commit message, type Co-authored-by: name <name@example.com> with specific information for each co-author. After the co-author information, add a closing quotation mark.

If you're adding multiple co-authors, give each co-author their own line and Co-authored-by: commit trailer.

    $ git commit -m "Refactor usability tests.
    > Co-authored-by: NAME <NAME@EXAMPLE.COM>
    > Co-authored-by: ANOTHER-NAME <ANOTHER-NAME@EXAMPLE.COM>"

#### Creating co-authored commits on GitHub

1. Collect the name and email address for each co-author. If a person chooses to keep their email address private, you should use their GitHub-provided no-reply email to protect their privacy.
2. Click Commit changes...
3. In the "Commit message" field, type a short, meaningful commit message that describes the changes you made.
4. In the text box below your commit message, add Co-authored-by: name <name@example.com> with specific information for each co-author. If you're adding multiple co-authors, give each co-author their own line and Co-authored-by: commit trailer.
5. Click Commit changes or Propose changes.

### Changing a commit message

If a commit message contains unclear, incorrect, or sensitive information, you can amend it locally and push a new commit with a new message to GitHub. You can also change a commit message to add missing information.

#### Rewriting the most recent commit message

If a commit message contains unclear, incorrect, or sensitive information, you can amend it locally and push a new commit with a new message to GitHub. You can also change a commit message to add missing information.

You can change the most recent commit message using the git commit --amend command.

In Git, the text of the commit message is part of the commit. Changing the commit message will change the commit ID--i.e., the SHA1 checksum that names the commit. Effectively, you are creating a new commit that replaces the old one.

#### Commit has not been pushed online

If the commit only exists in your local repository and has not been pushed to GitHub.com, you can amend the commit message with the git commit --amend command.

1. On the command line, navigate to the repository that contains the commit you want to amend.
2. Type git commit --amend and press Enter.
3. In your text editor, edit the commit message, and save the commit.
   1. You can add a co-author by adding a trailer to the commit. For more information, see "Creating a commit with multiple authors."
   2. You can create commits on behalf of your organization by adding a trailer to the commit. For more information, see "Creating a commit on behalf of an organization"

#### Amending older or multiple commit messages

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
