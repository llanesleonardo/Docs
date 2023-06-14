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

```
--orphan <new-branch>
```

Create a new orphan branch, named <new-branch>, started from <start-point> and switch to it. The first commit made on this new branch will have no parents and it will be the root of a new history totally disconnected from all the other branches and commits.

The index and the working tree are adjusted as if you had previously run git checkout <start-point>. This allows you to start a new history that records a set of paths similar to <start-point> by easily running git commit -a to make the root commit.

This can be useful when you want to publish the tree from a commit without exposing its full history. You might want to do this to publish an open source branch of a project whose current tree is "clean", but whose full history contains proprietary or otherwise encumbered bits of code.

If you want to start a disconnected history that records a set of paths that is totally different from the one of <start-point>, then you should clear the index and the working tree right after creating the orphan branch by running git rm -rf . from the top level of the working tree. Afterwards you will be ready to prepare your new files, repopulating the working tree, by copying them from elsewhere, extracting a tarball, etc.

```
-m
--merge
```

When switching branches, if you have local modifications to one or more files that are different between the current branch and the branch to which you are switching, the command refuses to switch branches in order to preserve your modifications in context. However, with this option, a three-way merge between the current branch, your working tree contents, and the new branch is done, and you will be on the new branch.

When a merge conflict happens, the index entries for conflicting paths are left unmerged, and you need to resolve the conflicts and mark the resolved paths with git add (or git rm if the merge should result in deletion of the path).

When checking out paths from the index, this option lets you recreate the conflicted merge in the specified paths.
When switching branches with --merge, staged changes may be lost.

TODO: FIND MORE INFO.

## Examples

HEAD normally refers to a named branch (e.g. master). Meanwhile, each branch refers to a specific commit. Let’s look at a repo with three commits, one of them tagged, and with branch master checked out:

```
           HEAD (refers to branch 'master')
            |
            v
a---b---c  branch 'master' (refers to commit 'c')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
```

When a commit is created in this state, the branch is updated to refer to the new commit. Specifically, git commit creates a new commit d, whose parent is commit c, and then updates branch master to refer to new commit d. HEAD still refers to branch master and so indirectly now refers to commit d:

```
$ edit; git add; git commit

               HEAD (refers to branch 'master')
                |
                v
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
```

It is sometimes useful to be able to checkout a commit that is not at the tip of any named branch, or even to create a new commit that is not referenced by a named branch. Let’s look at what happens when we checkout commit b (here we show two ways this may be done):

```
$ git checkout v2.0  # or
$ git checkout master^^

   HEAD (refers to commit 'b')
    |
    v
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
```

Notice that regardless of which checkout command we use, HEAD now refers directly to commit b. This is known as being in detached HEAD state. It means simply that HEAD refers to a specific commit, as opposed to referring to a named branch. Let’s see what happens when we create a commit:

```
$ edit; git add; git commit

     HEAD (refers to commit 'e')
      |
      v
      e
     /
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
```

There is now a new commit e, but it is referenced only by HEAD. We can of course add yet another commit in this state:

```
$ edit; git add; git commit

	 HEAD (refers to commit 'f')
	  |
	  v
      e---f
     /
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
```

In fact, we can perform all the normal Git operations. But, let’s look at what happens when we then checkout master:

```
$ git checkout master

               HEAD (refers to branch 'master')
      e---f     |
     /          v
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
```

It is important to realize that at this point nothing refers to commit f. Eventually commit f (and by extension commit e) will be deleted by the routine Git garbage collection process, unless we create a reference before that happens. If we have not yet moved away from commit f, any of these will create a reference to it:

```
$ git checkout -b foo  # or "git switch -c foo"  (1)
$ git branch foo                                 (2)
$ git tag foo                                    (3)
```

1. creates a new branch foo, which refers to commit f, and then updates HEAD to refer to branch foo. In other words, we’ll no longer be in detached HEAD state after this command.
2. similarly creates a new branch foo, which refers to commit f, but leaves HEAD detached.
3. creates a new tag foo, which refers to commit f, leaving HEAD detached.

If we have moved away from commit f, then we must first recover its object name (typically by using git reflog), and then we can create a reference to it. For example, to see the last two commits to which HEAD referred, we can use either of these commands:

```
$ git reflog -2 HEAD # or
$ git log -g -2 HEAD
```

## Examples

More: [Git checkout](https://git-scm.com/docs/git-checkout#_examples)
