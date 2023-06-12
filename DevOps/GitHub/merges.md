Back: [Pull Request](./pullrequest.md)

# Merge

## Address merge conflicts

---

Merge conflicts happen when you merge branches that have competing commits, and Git needs your help to decide which changes to incorporate in the final merge.

Git can often resolve differences between branches and merge them automatically. Usually, the changes are on different lines, or even in different files, which makes the merge simple for computers to understand.

However, sometimes there are competing changes that Git can't resolve without your help. Often, merge conflicts happen when people make different changes to the same line of the same file, or when one person edits a file and another person deletes the same file.

You must resolve all merge conflicts before you can merge a pull request on GitHub. If you have a merge conflict between the compare branch and base branch in your pull request, you can view a list of the files with conflicting changes above the Merge pull request button. The Merge pull request button is deactivated until you've resolved all conflicts between the compare branch and base branch.

To resolve a merge conflict, you must manually edit the conflicted file to select the changes that you want to keep in the final merge. There are a couple of different ways to resolve a merge conflict:

If your merge conflict is caused by competing line changes, such as when people make different changes to the same line of the same file on different branches in your Git repository, you can resolve it on GitHub using the conflict editor.

For all other types of merge conflicts, you must resolve the merge conflict in a local clone of the repository and push the change to your branch on GitHub. You can use the command line or a tool like GitHub Desktop to push the change.

If you have a merge conflict on the command line, you cannot push your local changes to GitHub until you resolve the merge conflict locally on your computer. If you try merging branches on the command line that have a merge conflict, you'll get an error message.

```
$ git merge BRANCH-NAME
> Auto-merging styleguide.md
> CONFLICT (content): Merge conflict in styleguide.md
> Automatic merge failed; fix conflicts and then commit the result
```

## Resolving a merge conflict on GitHub

---

You can resolve simple merge conflicts that involve competing line changes on GitHub, using the conflict editor.

You can only resolve merge conflicts on GitHub that are caused by competing line changes, such as when people make different changes to the same line of the same file on different branches in your Git repository. For all other types of merge conflicts, you must resolve the conflict locally on the command line.

When you resolve a merge conflict on GitHub, the entire base branch of your pull request is merged into the head branch. Make sure you really want to commit to this branch. If the head branch is the default branch of your repository, you'll be given the option of creating a new branch to serve as the head branch for your pull request. If the head branch is protected you won't be able to merge your conflict resolution into it, so you'll be prompted to create a new head branch.

### Process' checklist

1. Under your repository name, click Pull requests.
2. In the "Pull Requests" list, click the pull request with a merge conflict that you'd like to resolve.
3. Near the bottom of your pull request, click Resolve conflicts.
4. Decide if you want to keep only your branch's changes, keep only the other branch's changes, or make a brand new change, which may incorporate changes from both branches. Delete the conflict markers <<<<<<<, =======, >>>>>>> and make the changes you want in the final merge.
5. If you have more than one merge conflict in your file, scroll down to the next set of conflict markers and repeat steps four and five to resolve your merge conflict.
6. Once you've resolved all the conflicts in the file, click Mark as resolved.
7. If you have more than one file with a conflict, select the next file you want to edit on the left side of the page under "conflicting files" and repeat steps four through seven until you've resolved all of your pull request's merge conflicts.
8. Once you've resolved all your merge conflicts, click Commit merge. This merges the entire base branch into your head branch.
9. If prompted, review the branch that you are committing to.

If the head branch is the default branch of the repository, you can choose either to update this branch with the changes you made to resolve the conflict, or to create a new branch and use this as the head branch of the pull request.

If you choose to create a new branch, enter a name for the branch.

If the head branch of your pull request is protected you must create a new branch. You won't get the option to update the protected branch.

Click Create branch and update my pull request or I understand, continue updating BRANCH. The button text corresponds to the action you are performing.

10. To merge your pull request, click Merge pull request.

## Resolving a merge conflict using the command line

---

You can resolve merge conflicts using the command line and a text editor.

Merge conflicts occur when competing changes are made to the same line of a file, or when one person edits a file and another person deletes the same file.

### Competing line change merge conflicts

---

To resolve a merge conflict caused by competing line changes, you must choose which changes to incorporate from the different branches in a new commit.

For example, if you and another person both edited the file styleguide.md on the same lines in different branches of the same Git repository, you'll get a merge conflict error when you try to merge these branches. You must resolve this merge conflict with a new commit before you can merge these branches.

### Process' checklist

1. Git Bash.
2. Navigate into the local Git repository that has the merge conflict.
3. Generate a list of the files affected by the merge conflict. In this example, the file styleguide.md has a merge conflict.
4. Open your favorite text editor, such as Visual Studio Code, and navigate to the file that has merge conflicts.
5. To see the beginning of the merge conflict in your file, search the file for the conflict marker <<<<<<<. When you open the file in your text editor, you'll see the changes from the HEAD or base branch after the line <<<<<<< HEAD. Next, you'll see =======, which divides your changes from the changes in the other branch, followed by >>>>>>> BRANCH-NAME. In this example, one person wrote "open an issue" in the base or HEAD branch and another person wrote "ask your question in IRC" in the compare branch or branch-a.

```
If you have questions, please
#<<<<<<< HEAD
open an issue
=======
ask your question in IRC.
#>>>>>>> branch-a
```

6. Decide if you want to keep only your branch's changes, keep only the other branch's changes, or make a brand new change, which may incorporate changes from both branches. Delete the conflict markers <<<<<<<, =======, >>>>>>> and make the changes you want in the final merge. In this example, both changes are incorporated into the final merge:

"If you have questions, please open an issue or ask in our IRC channel if it's more urgent.
"

7. Add or stage your changes.
8. Commit your changes with a comment.

```
$ git commit -m "Resolved merge conflict by incorporating both suggestions."

```

### Removed file merge conflicts

---

To resolve a merge conflict caused by competing changes to a file, where a person deletes a file in one branch and another person edits the same file, you must choose whether to delete or keep the removed file in a new commit.

For example, if you edited a file, such as README.md, and another person removed the same file in another branch in the same Git repository, you'll get a merge conflict error when you try to merge these branches. You must resolve this merge conflict with a new commit before you can merge these branches.

### Process' checklist

1. Open Git Bash.
2. Navigate into the local Git repository that has the merge conflict.
3. Generate a list of the files affected by the merge conflict. In this example, the file README.md has a merge conflict.

```
$ git status
> # On branch main
> # Your branch and 'origin/main' have diverged,
> # and have 1 and 2 different commits each, respectively.
> #  (use "git pull" to merge the remote branch into yours)
> # You have unmerged paths.
> #  (fix conflicts and run "git commit")
> #
> # Unmerged paths:
> #  (use "git add/rm ..." as appropriate to mark resolution)
> #
> #	deleted by us:   README.md
> #
> # no changes added to commit (use "git add" and/or "git commit -a")
```

4. Open your favorite text editor, such as Visual Studio Code, and navigate to the file that has merge conflicts.
5. Decide if you want keep the removed file. You may want to view the latest changes made to the removed file in your text editor.

To add the removed file back to your repository:

```
$ git add README.md
```

To remove this file from your repository:

```
$ git rm README.md
> README.md: needs merge
> rm 'README.md'
```

Commit your changes with a comment.

```
$ git commit -m "Resolved merge conflict by keeping README.md file."
> [branch-d 6f89e49] Merge branch 'branch-c' into branch-d
```
