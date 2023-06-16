# Git rebase

Reapply commits on top of another base tip.

If <branch> is specified, git rebase will perform an automatic git switch <branch> before doing anything else. Otherwise it remains on the current branch.

If <upstream> is not specified, the upstream configured in branch.<name>.remote and branch.<name>.merge options will be used (see git-config[1] for details) and the --fork-point option is assumed. If you are currently not on any branch or if the current branch does not have a configured upstream, the rebase will abort.

All changes made by commits in the current branch but that are not in <upstream> are saved to a temporary area. This is the same set of commits that would be shown by git log <upstream>..HEAD; or by git log 'fork_point'..HEAD, if --fork-point is active (see the description on --fork-point below); or by git log HEAD, if the --root option is specified.

The current branch is reset to <upstream> or <newbase> if the --onto option was supplied. This has the exact same effect as git reset --hard <upstream> (or <newbase>). ORIG_HEAD is set to point at the tip of the branch before the reset.

The commits that were previously saved into the temporary area are then reapplied to the current branch, one by one, in order. Note that any commits in HEAD which introduce the same textual changes as a commit in HEAD..<upstream> are omitted (i.e., a patch already accepted upstream with a different commit message or timestamp will be skipped).

It is possible that a merge failure will prevent this process from being completely automatic. You will have to resolve any such merge failure and run git rebase --continue. Another option is to bypass the commit that caused the merge failure with git rebase --skip. To check out the original <branch> and remove the .git/rebase-apply working files, use the command git rebase --abort instead.

Assume the following history exists and the current branch is "topic":

```
          A---B---C topic
         /
    D---E---F---G master
```

From this point, the result of either of the following commands:

```
git rebase master
git rebase master topic
```

would be:

```
                  A'--B'--C' topic
                 /
    D---E---F---G master
```

The latter form is just a short-hand of git checkout topic followed by git rebase master. When rebase exits topic will remain the checked-out branch.

If the upstream branch already contains a change you have made (e.g., because you mailed a patch which was applied upstream), then that commit will be skipped and warnings will be issued (if the merge backend is used). For example, running git rebase master on the following history (in which A' and A introduce the same set of changes, but have different committer information):

```
          A---B---C topic
         /
    D---E---A'---F master
```

will result in:

```
                   B'---C' topic
                  /
    D---E---A'---F master
```

Here is how you would transplant a topic branch based on one branch to another, to pretend that you forked the topic branch from the latter branch, using rebase --onto.

First let’s assume your topic is based on branch next. For example, a feature developed in topic depends on some functionality which is found in next.

```
    o---o---o---o---o  master
         \
          o---o---o---o---o  next
                           \
                            o---o---o  topic
```

We want to make topic forked from branch master; for example, because the functionality on which topic depends was merged into the more stable master branch. We want our tree to look like this:

```
    o---o---o---o---o  master
        |            \
        |             o'--o'--o'  topic
         \
          o---o---o---o---o  next
```

We can get this using the following command:

git rebase --onto master next topic

Another example of --onto option is to rebase part of a branch. If we have the following situation:

```
                            H---I---J topicB
                           /
                  E---F---G  topicA
                 /
    A---B---C---D  master
```

then the command

git rebase --onto master topicA topicB
would result in:

```
                 H'--I'--J'  topicB
                /
                | E---F---G  topicA
                |/
    A---B---C---D  master
```

This is useful when topicB does not depend on topicA.

A range of commits could also be removed with rebase. If we have the following situation:

```
    E---F---G---H---I---J  topicA
```

then the command

git rebase --onto topicA~5 topicA~3 topicA
would result in the removal of commits F and G:

```
    E---H'---I'---J'  topicA
```

This is useful if F and G were flawed in some way, or should not be part of topicA. Note that the argument to --onto and the <upstream> parameter can be any valid commit-ish.

In case of conflict, git rebase will stop at the first problematic commit and leave conflict markers in the tree. You can use git diff to locate the markers (<<<<<<) and make edits to resolve the conflict. For each file you edit, you need to tell Git that the conflict has been resolved, typically this would be done with

```
git add <filename>
```

After resolving the conflict manually and updating the index with the desired resolution, you can continue the rebasing process with

```
git rebase --continue
```

Alternatively, you can undo the git rebase with

```
git rebase --abort
```

## Options

```
--onto <newbase>
```

Starting point at which to create the new commits. If the --onto option is not specified, the starting point is <upstream>. May be any valid commit, and not just an existing branch name.

As a special case, you may use "A...B" as a shortcut for the merge base of A and B if there is exactly one merge base. You can leave out at most one of A and B, in which case it defaults to HEAD.

```
--keep-base
```

Set the starting point at which to create the new commits to the merge base of <upstream> and <branch>. Running git rebase --keep-base <upstream> <branch> is equivalent to running git rebase --reapply-cherry-picks --no-fork-point --onto <upstream>...<branch> <upstream> <branch>.

This option is useful in the case where one is developing a feature on top of an upstream branch. While the feature is being worked on, the upstream branch may advance and it may not be the best idea to keep rebasing on top of the upstream but to keep the base commit as-is. As the base commit is unchanged this option implies --reapply-cherry-picks to avoid losing commits.

Although both this option and --fork-point find the merge base between <upstream> and <branch>, this option uses the merge base as the starting point on which new commits will be created, whereas --fork-point uses the merge base to determine the set of commits which will be rebased.

```
<upstream>
```

Upstream branch to compare against. May be any valid commit, not just an existing branch name. Defaults to the configured upstream for the current branch.

```
<branch>
```

Working branch; defaults to HEAD.

```
--apply
```

Use applying strategies to rebase (calling git-am internally). This option may become a no-op in the future once the merge backend handles everything the apply one does.

```
--empty={drop,keep,ask}
```

How to handle commits that are not empty to start and are not clean cherry-picks of any upstream commit, but which become empty after rebasing (because they contain a subset of already upstream changes). With drop (the default), commits that become empty are dropped. With keep, such commits are kept. With ask (implied by --interactive), the rebase will halt when an empty commit is applied allowing you to choose whether to drop it, edit files more, or just commit the empty changes. Other options, like --exec, will use the default of drop unless -i/--interactive is explicitly specified.

Note that commits which start empty are kept (unless --no-keep-empty is specified), and commits which are clean cherry-picks (as determined by git log --cherry-mark ...) are detected and dropped as a preliminary step (unless --reapply-cherry-picks or --keep-base is passed).

```
--no-keep-empty
--keep-empty
```

Do not keep commits that start empty before the rebase (i.e. that do not change anything from its parent) in the result. The default is to keep commits which start empty, since creating such commits requires passing the --allow-empty override flag to git commit, signifying that a user is very intentionally creating such a commit and thus wants to keep it.

Usage of this flag will probably be rare, since you can get rid of commits that start empty by just firing up an interactive rebase and removing the lines corresponding to the commits you don’t want. This flag exists as a convenient shortcut, such as for cases where external tools generate many empty commits and you want them all removed.

For commits which do not start empty but become empty after rebasing, see the --empty flag.

```
--reapply-cherry-picks
--no-reapply-cherry-picks
```

Reapply all clean cherry-picks of any upstream commit instead of preemptively dropping them. (If these commits then become empty after rebasing, because they contain a subset of already upstream changes, the behavior towards them is controlled by the --empty flag.)

In the absence of --keep-base (or if --no-reapply-cherry-picks is given), these commits will be automatically dropped. Because this necessitates reading all upstream commits, this can be expensive in repositories with a large number of upstream commits that need to be read. When using the merge backend, warnings will be issued for each dropped commit (unless --quiet is given). Advice will also be issued unless advice.skippedCherryPicks is set to false (see git-config[1]).

--reapply-cherry-picks allows rebase to forgo reading all upstream commits, potentially improving performance.

```
-m
--merge
```

Using merging strategies to rebase (default).

Note that a rebase merge works by replaying each commit from the working branch on top of the <upstream> branch. Because of this, when a merge conflict happens, the side reported as ours is the so-far rebased series, starting with <upstream>, and theirs is the working branch. In other words, the sides are swapped.

```
-s <strategy>
--strategy=<strategy>
```

Use the given merge strategy, instead of the default ort. This implies --merge.

Because git rebase replays each commit from the working branch on top of the <upstream> branch using the given strategy, using the ours strategy simply empties all patches from the <branch>, which makes little sense.

```
-X <strategy-option>
--strategy-option=<strategy-option>
```

Pass the <strategy-option> through to the merge strategy. This implies --merge and, if no strategy has been specified, -s ort. Note the reversal of ours and theirs as noted above for the -m option.

```
-r
--rebase-merges[=(rebase-cousins|no-rebase-cousins)]
--no-rebase-merges
```

By default, a rebase will simply drop merge commits from the todo list, and put the rebased commits into a single, linear branch. With --rebase-merges, the rebase will instead try to preserve the branching structure within the commits that are to be rebased, by recreating the merge commits. Any resolved merge conflicts or manual amendments in these merge commits will have to be resolved/re-applied manually. --no-rebase-merges can be used to countermand both the rebase.rebaseMerges config option and a previous --rebase-merges.

```
--autosquash
--no-autosquash
```

When the commit log message begins with "squash! …​" or "fixup! …​" or "amend! …​", and there is already a commit in the todo list that matches the same ..., automatically modify the todo list of rebase -i, so that the commit marked for squashing comes right after the commit to be modified, and change the action of the moved commit from pick to squash or fixup or fixup -C respectively. A commit matches the ... if the commit subject matches, or if the ... refers to the commit’s hash. As a fall-back, partial matches of the commit subject work, too. The recommended way to create fixup/amend/squash commits is by using the --fixup, --fixup=amend: or --fixup=reword: and --squash options respectively of git-commit[1].

If the --autosquash option is enabled by default using the configuration variable rebase.autoSquash, this option can be used to override and disable this setting.

```
--autostash
--no-autostash
```

Automatically create a temporary stash entry before the operation begins, and apply it after the operation ends. This means that you can run rebase on a dirty worktree. However, use with care: the final stash application after a successful rebase might result in non-trivial conflicts.

## Mode Options

[Mode options](https://git-scm.com/docs/git-rebase#_mode_options)

## Recovering from upstream rebase

Rebasing (or any other form of rewriting) a branch that others have based work on is a bad idea: anyone downstream of it is forced to manually fix their history. This section explains how to do the fix from the downstream’s point of view. The real fix, however, would be to avoid rebasing the upstream in the first place.

To illustrate, suppose you are in a situation where someone develops a subsystem branch, and you are working on a topic that is dependent on this subsystem. You might end up with a history like the following:

```
    o---o---o---o---o---o---o---o  master
	 \
	  o---o---o---o---o  subsystem
			   \
			    *---*---*  topic
```

If subsystem is rebased against master, the following happens:

```
    o---o---o---o---o---o---o---o  master
	 \			         \
	  o---o---o---o---o	  o'--o'--o'--o'--o'  subsystem
                        \
                            *---*---*  topic
```

If you now continue development as usual, and eventually merge topic to subsystem, the commits from subsystem will remain duplicated forever:

```
    o---o---o---o---o---o---o---o  master
	     \			                 \
	     o---o---o---o---o	          o'--o'--o'--o'--o'--M	 subsystem
			                \			                 /
			                *---*---*-..........-*--*  topic
```

Such duplicates are generally frowned upon because they clutter up history, making it harder to follow. To clean things up, you need to transplant the commits on topic to the new subsystem tip, i.e., rebase topic. This becomes a ripple effect: anyone downstream from topic is forced to rebase too, and so on!

There are two kinds of fixes, discussed in the following subsections:

Easy case: The changes are literally the same.
This happens if the subsystem rebase was a simple rebase and had no conflicts.

Hard case: The changes are not the same.
This happens if the subsystem rebase had conflicts, or used --interactive to omit, edit, squash, or fixup commits; or if the upstream used one of commit --amend, reset, or a full history rewriting command like filter-repo.

### The easy way

Only works if the changes (patch IDs based on the diff contents) on subsystem are literally the same before and after the rebase subsystem did.

In that case, the fix is easy because git rebase knows to skip changes that are already present in the new upstream (unless --reapply-cherry-picks is given). So if you say (assuming you’re on topic)

```
    $ git rebase subsystem
```

you will end up with the fixed history

```
    o---o---o---o---o---o---o---o  master
				 \
				  o'--o'--o'--o'--o'  subsystem
						   \
						    *---*---*  topic

```

### The hard case

Things get more complicated if the subsystem changes do not exactly correspond to the ones before the rebase.

The idea is to manually tell git rebase "where the old subsystem ended and your topic began", that is, what the old merge base between them was. You will have to find a way to name the last commit of the old subsystem, for example:

- With the subsystem reflog: after git fetch, the old tip of subsystem is at subsystem@{1}. Subsequent fetches will increase the number. (See git-reflog[1].)
- Relative to the tip of topic: knowing that your topic has three commits, the old tip of subsystem must be topic~3.

You can then transplant the old subsystem..topic to the new tip by saying (for the reflog case, and assuming you are on topic already):

```
    $ git rebase --onto subsystem subsystem@{1}
```

The ripple effect of a "hard case" recovery is especially bad: everyone downstream from topic will now have to perform a "hard case" recovery too!

## Rebasing merges

[Rebasing merges](https://git-scm.com/docs/git-rebase#_rebasing_merges)

## Examples

Let's assume the following scenario:

You have a Git repository with two branches: feature and main.
The feature branch contains a series of commits that you want to move onto the main branch.
To achieve this using git rebase --onto, follow these steps:

Ensure you are on the feature branch:

```
git checkout feature

```

Identify the commit range that you want to move from feature to main. Let's say you want to move the commits starting from commit A (exclusive) to commit D (inclusive).

Determine the new base where you want to apply the commits. In this case, it's the main branch. Make sure you are on the main branch:

```
git checkout main
```

Run the git rebase --onto command, specifying the new base (main), the old base (A), and the branch with the commits (feature):

```
git rebase --onto main A feature

```

This command instructs Git to detach the commits starting from A (exclusive) up to and including D from the feature branch, and apply them onto the main branch as new commits.

After executing the git rebase --onto command, the specified range of commits will be moved from the feature branch to the main branch, effectively rewriting the commit history.

It's important to note that the commit hashes (A, B, C, D) represent the actual commit references in your repository and should be replaced with the appropriate commit hashes or branch names from your specific scenario.

Remember that git rebase --onto can be a powerful command, but it modifies the commit history, so it should be used with care, especially when working with shared branches or repositories. It's always recommended to have a backup or create a branch from the original state before performing history-altering operations.

```

```
