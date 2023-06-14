# Git checkout

Switch branches or restore working tree files.

Updates files in the working tree to match the version in the index or the specified tree. If no pathspec was given, git checkout will also update HEAD to set the specified branch as the current branch.

## Options

```
--ours
--theirs
```

When checking out paths from the index, check out stage #2 (ours) or #3 (theirs) for unmerged paths.

Note that during git rebase and git pull --rebase, ours and theirs may appear swapped; --ours gives the version from the branch the changes are rebased onto, while --theirs gives the version from the branch that holds your work that is being rebased.

This is because rebase is used in a workflow that treats the history at the remote as the shared canonical one, and treats the work done on the branch you are rebasing as the third-party work to be integrated, and you are temporarily assuming the role of the keeper of the canonical history during the rebase. As the keeper of the canonical history, you need to view the history from the remote as ours (i.e. "our shared canonical history"), while what you did on your side branch as theirs (i.e. "one contributor’s work on top of it").

In Git, the --ours and --theirs options can be used with the git checkout command to specify which version of a file to check out in a merge conflict resolution scenario.

Here's how these options work:

--ours: When resolving a merge conflict, using git checkout --ours <file> will replace the conflicting file with the version from the branch you are currently on (the branch you are merging into). It selects "our" version of the file, meaning the changes made on the current branch.

--theirs: Conversely, using git checkout --theirs <file> will replace the conflicting file with the version from the branch being merged (the branch you are merging from). It selects "their" version of the file, meaning the changes made on the other branch.

These options are helpful when you want to quickly resolve merge conflicts by choosing one side's changes over the other without manually editing the conflicting file.

Here's an example to illustrate their usage:

1. You initiate a merge between two branches: branchA and branchB.
2. During the merge, Git encounters conflicts in a file called myfile.txt.
3. To accept the changes from branchA (the current branch), you can run:

```
git checkout --ours myfile.txt

```

4. This replaces myfile.txt with the version from branchA, discarding the conflicting changes from branchB.
   Conversely, to accept the changes from branchB (the branch being merged), you can run:

```
git checkout --theirs myfile.txt

```

This replaces myfile.txt with the version from branchB, discarding the conflicting changes from branchA.

Remember to mark the conflict as resolved after using either --ours or --theirs with git add <file> and complete the merge with git commit.

```
-b <new-branch>
```

Create a new branch named <new-branch>, start it at <start-point>, and check the resulting branch out; see git-branch[1] for details.

```
-B <new-branch>
```

Creates the branch <new-branch>, start it at <start-point>; if it already exists, then reset it to <start-point>. And then check the resulting branch out. This is equivalent to running "git branch" with "-f" followed by "git checkout" of that branch; see git-branch[1] for details.

```
-t
--track[=(direct|inherit)]
```

When creating a new branch, set up "upstream" configuration. See "--track" in git-branch[1] for details.

If no -b option is given, the name of the new branch will be derived from the remote-tracking branch, by looking at the local part of the refspec configured for the corresponding remote, and then stripping the initial part up to the "\*". This would tell us to use hack as the local branch when branching off of origin/hack (or remotes/origin/hack, or even refs/remotes/origin/hack). If the given name has no slash, or the above guessing results in an empty name, the guessing is aborted. You can explicitly give a name with -b in such a case.

```
-l

```

Create the new branch’s reflog;

```
-d
--detach
```

Rather than checking out a branch to work on it, check out a commit for inspection and discardable experiments. This is the default behavior of git checkout <commit> when <commit> is not a branch name. See the "DETACHED HEAD" section below for details.
