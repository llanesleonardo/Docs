# Git stash

Stash the changes in a dirty working directory away.

Use git stash when you want to record the current state of the working directory and the index, but want to go back to a clean working directory. The command saves your local modifications away and reverts the working directory to match the HEAD commit.

The modifications stashed away by this command can be listed with git stash list, inspected with git stash show, and restored (potentially on top of a different commit) with git stash apply. Calling git stash without any arguments is equivalent to git stash push. A stash is by default listed as "WIP on branchname …​", but you can give a more descriptive message on the command line when you create one.

The latest stash you created is stored in refs/stash; older stashes are found in the reflog of this reference and can be named using the usual reflog syntax (e.g. stash@{0} is the most recently created stash, stash@{1} is the one before it, stash@{2.hours.ago} is also possible). Stashes may also be referenced by specifying just the stash index (e.g. the integer n is equivalent to stash@{n}).

## Commands

[Commands](https://git-scm.com/docs/git-stash#_commands)

## Options

```
-a
--all
```

This option is only valid for push and save commands.

All ignored and untracked files are also stashed and then cleaned up with git clean.

```
-u
--include-untracked
--no-include-untracked
```

When used with the push and save commands, all untracked files are also stashed and then cleaned up with git clean.

When used with the show command, show the untracked files in the stash entry as part of the diff.

```
--only-untracked
```

This option is only valid for the show command.

Show only the untracked files in the stash entry as part of the diff.

```
--index`
```

This option is only valid for pop and apply commands.

Tries to reinstate not only the working tree’s changes, but also the index’s ones. However, this can fail, when you have conflicts (which are stored in the index, where you therefore can no longer apply the changes as they were originally).

```
-k
--keep-index
--no-keep-index
```

This option is only valid for push and save commands.

All changes already added to the index are left intact.

```
-p
--patch
```

This option is only valid for push and save commands.

Interactively select hunks from the diff between HEAD and the working tree to be stashed. The stash entry is constructed such that its index state is the same as the index state of your repository, and its worktree contains only the changes you selected interactively. The selected changes are then rolled back from your worktree. See the “Interactive Mode” section of git-add[1] to learn how to operate the --patch mode.

The --patch option implies --keep-index. You can use --no-keep-index to override this.

```
-S
--staged
```

This option is only valid for push and save commands.

Stash only the changes that are currently staged. This is similar to basic git commit except the state is committed to the stash instead of current branch.

The --patch option has priority over this one.

```
<pathspec>…​
```

This option is only valid for push command.

The new stash entry records the modified states only for the files that match the pathspec. The index entries and working tree files are then rolled back to the state in HEAD only for these files, too, leaving files that do not match the pathspec intact.

For more details, see the pathspec entry in gitglossary[7].

```
<stash>
```

This option is only valid for apply, branch, drop, pop, show commands.

A reference of the form stash@{<revision>}. When no <stash> is given, the latest stash is assumed (that is, stash@{0}).

## Examples

### Pulling into a dirty tree

When you are in the middle of something, you learn that there are upstream changes that are possibly relevant to what you are doing. When your local changes do not conflict with the changes in the upstream, a simple git pull will let you move forward.

However, there are cases in which your local changes do conflict with the upstream changes, and git pull refuses to overwrite your changes. In such a case, you can stash your changes away, perform a pull, and then unstash, like this:

```
$ git pull
 ...
file foobar not up to date, cannot merge.
$ git stash
$ git pull
$ git stash pop
```

### Interrupted workflow

When you are in the middle of something, your boss comes in and demands that you fix something immediately. Traditionally, you would make a commit to a temporary branch to store your changes away, and return to your original branch to make the emergency fix, like this:

```
# ... hack hack hack ...
$ git switch -c my_wip
$ git commit -a -m "WIP"
$ git switch master
$ edit emergency fix
$ git commit -a -m "Fix in a hurry"
$ git switch my_wip
$ git reset --soft HEAD^
# ... continue hacking ...
```

You can use git stash to simplify the above, like this:

```
# ... hack hack hack ...
$ git stash
$ edit emergency fix
$ git commit -a -m "Fix in a hurry"
$ git stash pop
# ... continue hacking ...
```

### Testing partial commits

You can use git stash push --keep-index when you want to make two or more commits out of the changes in the work tree, and you want to test each change before committing:

```
# ... hack hack hack ...

$ git add --patch foo # add just first part to the index
$ git stash push --keep-index # save all other changes to the stash
$ edit/build/test first part
$ git commit -m 'First part' # commit fully tested change
$ git stash pop # prepare to work on all other changes
# ... repeat above five steps until one commit remains ...
$ edit/build/test remaining parts
$ git commit foo -m 'Remaining parts'

```

### Saving unrelated changes for future use

When you are in the middle of massive changes and you find some unrelated issue that you don’t want to forget to fix, you can do the change(s), stage them, and use git stash push --staged to stash them out for future use. This is similar to committing the staged changes, only the commit ends-up being in the stash and not on the current branch.

```
# ... hack hack hack ...
$ git add --patch foo           # add unrelated changes to the index
$ git stash push --staged       # save these changes to the stash
# ... hack hack hack, finish curent changes ...
$ git commit -m 'Massive'       # commit fully tested changes
$ git switch fixup-branch       # switch to another branch
$ git stash pop                 # to finish work on the saved changes
```

### Recovering stash entries that were cleared/dropped erroneously

If you mistakenly drop or clear stash entries, they cannot be recovered through the normal safety mechanisms. However, you can try the following incantation to get a list of stash entries that are still in your repository, but not reachable any more:

git fsck --unreachable |
grep commit | cut -d\ -f3 |
xargs git log --merges --no-walk --grep=WIP
