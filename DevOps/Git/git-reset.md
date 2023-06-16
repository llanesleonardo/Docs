# Git reset

Reset current HEAD to the specified state.

In Git, the git reset command allows you to move the HEAD and the current branch pointer to a specified commit. It is a powerful command that can be used to manipulate the commit history, undo changes, and control the state of your working directory and staging area. The git reset command has several modes or options, each with a different effect on the repository state. Let's explore the most commonly used modes:

- Soft reset (git reset --soft): This mode moves the branch pointer to the specified commit while keeping the changes in the commit and staging area intact. It effectively "undoes" the commits but leaves the changes staged, allowing you to make further modifications or create a new commit.

- Mixed reset (git reset --mixed, default behavior): This mode is similar to a soft reset but also resets the staging area, effectively unstaging any changes. The commit contents remain intact, but the changes are uncommitted and need to be staged again before creating a new commit.

- Hard reset (git reset --hard): This mode moves the branch pointer to the specified commit and discards any changes in the working directory, staging area, and previous commits. It resets the repository to the exact state of the specified commit, permanently discarding any local modifications or uncommitted changes. Caution should be exercised when using a hard reset since it can lead to permanent data loss.

The basic syntax of the git reset command is as follows:

```
git reset <commit>
```

Here, <commit> represents the commit to which you want to reset. It can be specified using various formats, such as a commit hash, branch name, or a relative reference like HEAD~N to refer to a previous commit.

It's important to note that using git reset can rewrite history and discard commits, so it should be used with caution, especially when working with shared branches or repositories. Once you have reset a branch, it's generally not recommended to push the changes to a shared repository unless you are certain about the implications and have communicated with your team.

Before using git reset, it's advisable to create a backup or branch off from the current state if you want to preserve the original commits in case you need to revert the reset operation.

## Examples

### Undo add

```
$ edit                                     (1)
$ git add frotz.c filfre.c
$ mailx                                    (2)
$ git reset                                (3)
$ git pull git://info.example.com/ nitfol  (4)

```

- You are happily working on something, and find the changes in these files are in good order. You do not want to see them when you run git diff, because you plan to work on other files and changes with these files are distracting.
- Somebody asks you to pull, and the changes sound worthy of merging.
- However, you already dirtied the index (i.e. your index does not match the HEAD commit). But you know the pull you are going to make does not affect frotz.c or filfre.c, so you revert the index changes for these two files. Your changes in working tree remain there.
- Then you can pull and merge, leaving frotz.c and filfre.c changes still in the working tree.

### Undo a commit and redo

```
$ git commit ...
$ git reset --soft HEAD^      (1)
$ edit                        (2)
$ git commit -a -c ORIG_HEAD  (3)
```

- This is most often done when you remembered what you just committed is incomplete, or you misspelled your commit message, or both. Leaves working tree as it was before "reset".
- Make corrections to working tree files.
- "reset" copies the old head to .git/ORIG_HEAD; redo the commit by starting with its log message. If you do not need to edit the message further, you can give -C option instead.

### Undo a commit, making it a topic branch

```
$ git branch topic/wip          (1)
$ git reset --hard HEAD~3       (2)
$ git switch topic/wip          (3)
```

- You have made some commits, but realize they were premature to be in the master branch. You want to continue polishing them in a topic branch, so create topic/wip branch off of the current HEAD.
- Rewind the master branch to get rid of those three commits.
- Switch to topic/wip branch and keep working.

### Undo commits permanently

```
$ git commit ...
$ git reset --hard HEAD~3   (1)
```

The last three commits (HEAD, HEAD^, and HEAD~2) were bad and you do not want to ever see them again. Do not do this if you have already given these commits to somebody else. (See the "RECOVERING FROM UPSTREAM REBASE" section in git-rebase[1] for the implications of doing so.)

### Undo a merge or pull

```
$ git pull                         (1)
Auto-merging nitfol
CONFLICT (content): Merge conflict in nitfol
Automatic merge failed; fix conflicts and then commit the result.
$ git reset --hard                 (2)
$ git pull . topic/branch          (3)
Updating from 41223... to 13134...
Fast-forward
$ git reset --hard ORIG_HEAD       (4)

```

- Try to update from the upstream resulted in a lot of conflicts; you were not ready to spend a lot of time merging right now, so you decide to do that later.
- "pull" has not made merge commit, so git reset --hard which is a synonym for git reset --hard HEAD clears the mess from the index file and the working tree.
- Merge a topic branch into the current branch, which resulted in a fast-forward.
- But you decided that the topic branch is not ready for public consumption yet. "pull" or "merge" always leaves the original tip of the current branch in ORIG_HEAD, so resetting hard to it brings your index file and the working tree back to that state, and resets the tip of the branch to that commit.

### Undo a merge or pull inside a dirty working tree

```
$ git pull                         (1)
Auto-merging nitfol
Merge made by recursive.
 nitfol                |   20 +++++----
 ...
$ git reset --merge ORIG_HEAD      (2)
```

Even if you may have local modifications in your working tree, you can safely say git pull when you know that the change in the other branch does not overlap with them.

After inspecting the result of the merge, you may find that the change in the other branch is unsatisfactory. Running git reset --hard ORIG_HEAD will let you go back to where you were, but it will discard your local changes, which you do not want. git reset --merge keeps your local changes.

### Interrupted workflow

Suppose you are interrupted by an urgent fix request while you are in the middle of a large change. The files in your working tree are not in any shape to be committed yet, but you need to get to the other branch for a quick bugfix.

```
$ git switch feature  ;# you were working in "feature" branch and
$ work work work      ;# got interrupted
$ git commit -a -m "snapshot WIP"                 (1)
$ git switch master
$ fix fix fix
$ git commit ;# commit with real log
$ git switch feature
$ git reset --soft HEAD^ ;# go back to WIP state  (2)
$ git reset                                       (3)
```

- This commit will get blown away so a throw-away log message is OK.
- This removes the WIP commit from the commit history, and sets your working tree to the state just before you made that snapshot.
- At this point the index file still has all the WIP changes you committed as snapshot WIP. This updates the index to show your WIP files as uncommitted.

### Reset a single file in the index

Suppose you have added a file to your index, but later decide you do not want to add it to your commit. You can remove the file from the index while keeping your changes with git reset.

```
$ git reset -- frotz.c                      (1)
$ git commit -m "Commit files in index"     (2)
$ git add frotz.c                           (3)
```

- This removes the file from the index while keeping it in the working directory.
- This commits all other changes in the index.
- Adds the file to the index again.

### Keep changes in working tree while discarding some previous commits

Suppose you are working on something and you commit it, and then you continue working a bit more, but now you think that what you have in your working tree should be in another branch that has nothing to do with what you committed previously. You can start a new branch and reset it while keeping the changes in your working tree.

```
$ git tag start
$ git switch -c branch1
$ edit
$ git commit ... (1)
$ edit
$ git switch -c branch2 (2)
$ git reset --keep start (3)
```

- This commits your first edits in branch1.
- In the ideal world, you could have realized that the earlier commit did not belong to the new topic when you created and switched to branch2 (i.e. git switch -c branch2 start), but nobody is perfect.
- But you can use reset --keep to remove the unwanted commit after you switched to branch2.

### Split a commit apart into a sequence of commits

Suppose that you have created lots of logically separate changes and committed them together. Then, later you decide that it might be better to have each logical chunk associated with its own commit. You can use git reset to rewind history without changing the contents of your local files, and then successively use git add -p to interactively select which hunks to include into each commit, using git commit -c to pre-populate the commit message.

```
$ git reset -N HEAD^                        (1)
$ git add -p                                (2)
$ git diff --cached                         (3)
$ git commit -c HEAD@{1}                    (4)
...                                         (5)
$ git add ...                               (6)
$ git diff --cached                         (7)
$ git commit ...                            (8)`

```

First, reset the history back one commit so that we remove the original commit, but leave the working tree with all the changes. The -N ensures that any new files added with HEAD are still marked so that git add -p will find them.

Next, we interactively select diff hunks to add using the git add -p facility. This will ask you about each diff hunk in sequence and you can use simple commands such as "yes, include this", "No don’t include this" or even the very powerful "edit" facility.

Once satisfied with the hunks you want to include, you should verify what has been prepared for the first commit by using git diff --cached. This shows all the changes that have been moved into the index and are about to be committed.

Next, commit the changes stored in the index. The -c option specifies to pre-populate the commit message from the original message that you started with in the first commit. This is helpful to avoid retyping it. The HEAD@{1} is a special notation for the commit that HEAD used to be at prior to the original reset commit (1 change ago). See git-reflog[1] for more details. You may also use any other valid commit reference.

You can repeat steps 2-4 multiple times to break the original code into any number of commits.

Now you’ve split out many of the changes into their own commits, and might no longer use the patch mode of git add, in order to select all remaining uncommitted changes.

Once again, check to verify that you’ve included what you want to. You may also wish to verify that git diff doesn’t show any remaining changes to be committed later.

And finally create the final commit.
