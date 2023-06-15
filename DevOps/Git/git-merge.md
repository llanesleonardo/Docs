# Git merge

Join two or more development histories together.

Incorporates changes from the named commits (since the time their histories diverged from the current branch) into the current branch. This command is used by git pull to incorporate changes from another repository and can be used by hand to merge changes from one branch into another.

Assume the following history exists and the current branch is "master":

```
	  A---B---C topic
	 /
    D---E---F---G master
```

Then "git merge topic" will replay the changes made on the topic branch since it diverged from master (i.e., E) until its current commit (C) on top of master, and record the result in a new commit along with the names of the two parent commits and a log message from the user describing the changes. Before the operation, ORIG_HEAD is set to the tip of the current branch (C).

```
	  A---B---C topic
	 /         \
    D---E---F---G---H master
```

The second syntax ("git merge --abort") can only be run after the merge has resulted in conflicts. git merge --abort will abort the merge process and try to reconstruct the pre-merge state. However, if there were uncommitted changes when the merge started (and especially if those changes were further modified after the merge was started), git merge --abort will in some cases be unable to reconstruct the original (pre-merge) changes. Therefore:

## Options

[Options](https://git-scm.com/docs/git-merge#_options)

```
--commit
--no-commit
```

Perform the merge and commit the result. This option can be used to override --no-commit.

With --no-commit perform the merge and stop just before creating a merge commit, to give the user a chance to inspect and further tweak the merge result before committing.

Note that fast-forward updates do not create a merge commit and therefore there is no way to stop those merges with --no-commit. Thus, if you want to ensure your branch is not changed or updated by the merge command, use --no-ff with --no-commit.

```
--ff
--no-ff
--ff-only
```

Specifies how a merge is handled when the merged-in history is already a descendant of the current history. --ff is the default unless merging an annotated (and possibly signed) tag that is not stored in its natural place in the refs/tags/ hierarchy, in which case --no-ff is assumed.

With --ff, when possible resolve the merge as a fast-forward (only update the branch pointer to match the merged branch; do not create a merge commit). When not possible (when the merged-in history is not a descendant of the current history), create a merge commit.

With --no-ff, create a merge commit in all cases, even when the merge could instead be resolved as a fast-forward.

With --ff-only, resolve the merge as a fast-forward when possible. When not possible, refuse to merge and exit with a non-zero status.

```
--stat
-n
--no-stat
```

Show a diffstat at the end of the merge. The diffstat is also controlled by the configuration option merge.stat.

With -n or --no-stat do not show a diffstat at the end of the merge.

```
--squash
--no-squash
```

Produce the working tree and index state as if a real merge happened (except for the merge information), but do not actually make a commit, move the HEAD, or record $GIT_DIR/MERGE_HEAD (to cause the next git commit command to create a merge commit). This allows you to create a single commit on top of the current branch whose effect is the same as merging another branch (or more in case of an octopus).

With --no-squash perform the merge and commit the result. This option can be used to override --squash.

With --squash, --commit is not allowed, and will fail.

```--autostash
--no-autostash
```

Automatically create a temporary stash entry before the operation begins, record it in the special ref MERGE_AUTOSTASH and apply it after the operation ends. This means that you can run the operation on a dirty worktree. However, use with care: the final stash application after a successful merge might result in non-trivial conflicts.

```
--allow-unrelated-histories
```

By default, git merge command refuses to merge histories that do not share a common ancestor. This option can be used to override this safety when merging histories of two projects that started their lives independently. As that is a very rare occasion, no configuration variable to enable this by default exists and will not be added.

```
-m <msg>
```

Set the commit message to be used for the merge commit (in case one is created).

```
git merge --abort
```

Is equivalent to git reset --merge when MERGE_HEAD is present unless MERGE_AUTOSTASH is also present in which case git merge --abort applies the stash entry to the worktree whereas git reset --merge will save the stashed changes in the stash list.

```
--continue
```

After a git merge stops due to conflicts you can conclude the merge by running git merge --continue

## Pre merge checks

Before applying outside changes, you should get your own work in good shape and committed locally, so it will not be clobbered if there are conflicts. See also git-stash[1]. git pull and git merge will stop without doing anything when local uncommitted changes overlap with files that git pull/git merge may need to update.

To avoid recording unrelated changes in the merge commit, git pull and git merge will also abort if there are any changes registered in the index relative to the HEAD commit. (Special narrow exceptions to this rule may exist depending on which merge strategy is in use, but generally, the index must match HEAD.)

If all named commits are already ancestors of HEAD, git merge will exit early with the message "Already up to date."

## Fast forward merge

Often the current branch head is an ancestor of the named commit. This is the most common case especially when invoked from git pull: you are tracking an upstream repository, you have committed no local changes, and now you want to update to a newer upstream revision. In this case, a new commit is not needed to store the combined history; instead, the HEAD (along with the index) is updated to point at the named commit, without creating an extra merge commit.

## Merging tag

When merging an annotated (and possibly signed) tag, Git always creates a merge commit even if a fast-forward merge is possible, and the commit message template is prepared with the tag message. Additionally, if the tag is signed, the signature check is reported as a comment in the message template.

When you want to just integrate with the work leading to the commit that happens to be tagged, e.g. synchronizing with an upstream release point, you may not want to make an unnecessary merge commit.

In such a case, you can "unwrap" the tag yourself before feeding it to git merge, or pass --ff-only when you do not have any work on your own. e.g.

```
git fetch origin
git merge v1.2.3^0
git merge --ff-only v1.2.3
```

## How conflicts are presented

During a merge, the working tree files are updated to reflect the result of the merge. Among the changes made to the common ancestor’s version, non-overlapping ones (that is, you changed an area of the file while the other side left that area intact, or vice versa) are incorporated in the final result verbatim. When both sides made changes to the same area, however, Git cannot randomly pick one side over the other, and asks you to resolve it by leaving what both sides did to that area.

By default, Git uses the same style as the one used by the "merge" program from the RCS suite to present such a conflicted hunk, like this:

```
Here are lines that are either unchanged from the common
ancestor, or cleanly resolved because only one side changed,
or cleanly resolved because both sides changed the same way.
'<<<<<<< yours:sample.txt
Conflict resolution is hard;
let's go shopping.
=======
Git makes conflict resolution easy.
''>>>>>>> theirs:sample.txt
And here is another line that is cleanly resolved or unmodified.
```

The area where a pair of conflicting changes happened is marked with markers <<<<<<<, =======, and >>>>>>>. The part before the ======= is typically your side, and the part afterwards is typically their side.

The default format does not show what the original said in the conflicting area. You cannot tell how many lines are deleted and replaced with Barbie’s remark on your side. The only thing you can tell is that your side wants to say it is hard and you’d prefer to go shopping, while the other side wants to claim it is easy.

## How to resolve conflicts

After seeing a conflict, you can do two things:

- Decide not to merge. The only clean-ups you need are to reset the index file to the HEAD commit to reverse 2. and to clean up working tree changes made by 2. and 3.; git merge --abort can be used for this.
- Resolve the conflicts. Git will mark the conflicts in the working tree. Edit the files into shape and git add them to the index. Use git commit or git merge --continue to seal the deal. The latter command checks whether there is a (interrupted) merge in progress before calling git commit.

You can work through the conflict with a number of tools:

- Use a mergetool. git mergetool to launch a graphical mergetool which will work you through the merge.
- Look at the diffs. git diff will show a three-way diff, highlighting changes from both the HEAD and MERGE_HEAD versions.
- Look at the diffs from each branch. git log --merge -p <path> will show diffs first for the HEAD version and then the MERGE_HEAD version.
- Look at the originals. git show :1:filename shows the common ancestor, git show :2:filename shows the HEAD version, and git show :3:filename shows the MERGE_HEAD version.

TODO: FIND MORE INFO.

## Examples

Merge branches fixes and enhancements on top of the current branch, making an octopus merge:

```
$ git merge fixes enhancements
```

Merge branch obsolete into the current branch, using ours merge strategy:

```
$ git merge -s ours obsolete
```

Merge branch maint into the current branch, but do not make a new commit automatically:

```
$ git merge --no-commit maint
```

This can be used when you want to include further changes to the merge, or want to write your own merge commit message.

You should refrain from abusing this option to sneak substantial changes into a merge commit. Small fixups like bumping release/version name would be acceptable.

## Merge strategies

The merge mechanism (git merge and git pull commands) allows the backend merge strategies to be chosen with -s option. Some strategies can also take their own options, which can be passed by giving -X<option> arguments to git merge and/or git pull.

```
git merge --strategy=recursive my-branch

```

### ort

This is the default merge strategy when pulling or merging one branch. This strategy can only resolve two heads using a 3-way merge algorithm. When there is more than one common ancestor that can be used for 3-way merge, it creates a merged tree of the common ancestors and uses that as the reference tree for the 3-way merge. This has been reported to result in fewer merge conflicts without causing mismerges by tests done on actual merge commits taken from Linux 2.6 kernel development history. Additionally this strategy can detect and handle merges involving renames. It does not make use of detected copies. The name for this algorithm is an acronym ("Ostensibly Recursive’s Twin") and came from the fact that it was written as a replacement for the previous default algorithm, recursive.

This is the default strategy used by Git. It performs a three-way merge and creates a new merge commit that combines the changes from the merged branches. If there are conflicts, Git attempts to automatically resolve them. Otherwise, manual intervention is required to resolve conflicts.

### recursive

This can only resolve two heads using a 3-way merge algorithm. When there is more than one common ancestor that can be used for 3-way merge, it creates a merged tree of the common ancestors and uses that as the reference tree for the 3-way merge. This has been reported to result in fewer merge conflicts without causing mismerges by tests done on actual merge commits taken from Linux 2.6 kernel development history. Additionally this can detect and handle merges involving renames. It does not make use of detected copies. This was the default strategy for resolving two heads from Git v0.99.9k until v2.33.0.

The recursive strategy takes the same options as ort.

### resolve

This can only resolve two heads (i.e. the current branch and another branch you pulled from) using a 3-way merge algorithm. It tries to carefully detect criss-cross merge ambiguities. It does not handle renames.

This strategy is similar to the recursive merge strategy but resolves conflicts using the "resolve" algorithm instead of the default "merge" algorithm. It attempts to automatically resolve conflicts based on the changes made in the conflicting files.

### octopus

This resolves cases with more than two heads, but refuses to do a complex merge that needs manual resolution. It is primarily meant to be used for bundling topic branch heads together. This is the default merge strategy when pulling or merging more than one branch.

The Octopus merge strategy allows merging multiple branches simultaneously. It is useful when merging more than two branches into a single branch. Git creates a new merge commit that combines the changes from all the merged branches.

### ours

This resolves any number of heads, but the resulting tree of the merge is always that of the current branch head, effectively ignoring all changes from all other branches. It is meant to be used to supersede old development history of side branches. Note that this is different from the -Xours option to the recursive merge strategy.

This strategy is similar to the recursive merge strategy but resolves conflicts by favoring the changes from the branch being merged into. It automatically selects the changes from the current branch, ignoring the changes from the other branch.

### subtree

This is a modified ort strategy. When merging trees A and B, if B corresponds to a subtree of A, B is first adjusted to match the tree structure of A, instead of reading the trees at the same level. This adjustment is also done to the common ancestor tree.

With the strategies that use 3-way merge (including the default, ort), if a change is made on both branches, but later reverted on one of the branches, that change will be present in the merged result; some people find this behavior confusing. It occurs because only the heads and the merge base are considered when performing a merge, not the individual commits. The merge algorithm therefore considers the reverted change as no change at all, and substitutes the changed version instead.

### Fast-Forward Merge

If the branch being merged into is directly ahead of the branch being merged, Git performs a fast-forward merge. Instead of creating a new merge commit, Git moves the branch pointer forward to the same commit as the branch being merged. This strategy results in a linear history with no additional merge commits.

### No Fast-Forward Merge:

This strategy forces Git to create a new merge commit, even if a fast-forward merge is possible. It preserves the branch history and indicates that a merge has occurred. It is useful to maintain a clear history and explicitly show when branches have been merged.

### Recursive Strategy with Theirs

This strategy is similar to the recursive merge strategy but resolves conflicts by favoring the changes from the branch being merged. It automatically selects the changes from the other branch, ignoring the changes from the current branch.

## A Three way merge

A three-way merge is a type of merge operation performed by Git when combining changes from two branches with a common ancestor. It is the default merge strategy used by Git's recursive merge algorithm.

Here's how a three-way merge works:

1. Consider a scenario where you have two branches: branchA and branchB, which have diverged from a common ancestor commit.
2. Git identifies the common ancestor commit (often called the "merge base") of the two branches. The merge base represents the last commit that both branches have in common.
3. Git compares the changes made in branchA and branchB since the merge base. It identifies the differences or conflicting changes between the branches.
4. During the merge process, Git creates a new merge commit that combines the changes from both branches.
5. Git automatically attempts to merge the changes by applying the non-conflicting changes from both branches. These non-conflicting changes are merged automatically, without requiring manual intervention.
6. If there are conflicting changes, Git cannot determine the correct merge automatically. Git identifies the conflicting regions and marks them as merge conflicts.
7. The user is then responsible for manually resolving the conflicts by editing the conflicting regions in the affected files. The conflicts need to be resolved according to the desired outcome of the merge.
8. Once all conflicts are resolved, the user can proceed to complete the merge by adding the resolved files and creating a new merge commit.

The three-way merge takes into account the changes made in both branches since the common ancestor. It attempts to combine the changes while preserving the maximum amount of information from both branches.

This merge strategy is called a "three-way" merge because it involves three commits: the two branch heads being merged (branchA and branchB) and the common ancestor commit from which they diverged.

The three-way merge algorithm used by Git is powerful and handles most merging scenarios automatically. However, manual conflict resolution may be necessary when Git cannot determine the correct merge automatically due to conflicting changes.
