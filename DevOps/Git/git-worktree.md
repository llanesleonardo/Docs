# Git worktree

Manage multiple working trees.

Manage multiple working trees attached to the same repository.

A git repository can support multiple working trees, allowing you to check out more than one branch at a time. With git worktree add a new working tree is associated with the repository, along with additional metadata that differentiates that working tree from others in the same repository. The working tree, along with this metadata, is called a "worktree".

This new worktree is called a "linked worktree" as opposed to the "main worktree" prepared by git-init[1] or git-clone[1]. A repository has one main worktree (if it’s not a bare repository) and zero or more linked worktrees. When you are done with a linked worktree, remove it with git worktree remove.

In its simplest form, git worktree add <path> automatically creates a new branch whose name is the final component of <path>, which is convenient if you plan to work on a new topic. For instance, git worktree add ../hotfix creates new branch hotfix and checks it out at path ../hotfix. To instead work on an existing branch in a new worktree, use git worktree add <path> <branch>. On the other hand, if you just plan to make some experimental changes or do testing without disturbing existing development, it is often convenient to create a throwaway worktree not associated with any branch. For instance, git worktree add -d <path> creates a new worktree with a detached HEAD at the same commit as the current branch.

If a working tree is deleted without using git worktree remove, then its associated administrative files, which reside in the repository (see "DETAILS" below), will eventually be removed automatically (see gc.worktreePruneExpire in git-config[1]), or you can run git worktree prune in the main or any linked worktree to clean up any stale administrative files.

If the working tree for a linked worktree is stored on a portable device or network share which is not always mounted, you can prevent its administrative files from being pruned by issuing the git worktree lock command, optionally specifying --reason to explain why the worktree is locked.

## Commands

[Commands](https://git-scm.com/docs/git-worktree#_commands)

## Options

[Options](https://git-scm.com/docs/git-worktree#_options)

## Examples

[Woktree example](https://www.youtube.com/watch?v=cRunWRC8ye0)

You are in the middle of a refactoring session and your boss comes in and demands that you fix something immediately. You might typically use git-stash[1] to store your changes away temporarily, however, your working tree is in such a state of disarray (with new, moved, and removed files, and other bits and pieces strewn around) that you don’t want to risk disturbing any of it. Instead, you create a temporary linked worktree to make the emergency fix, remove it when done, and then resume your earlier refactoring session.

```
$ git worktree add -b emergency-fix ../temp master
$ pushd ../temp
# ... hack hack hack ...
$ git commit -a -m 'emergency fix for boss'
$ popd
$ git worktree remove ../temp
```

## List output format

The worktree list command has two output formats. The default format shows the details on a single line with columns. For example:

```
$ git worktree list
/path/to/bare-source            (bare)
/path/to/linked-worktree        abcd1234 [master]
/path/to/other-linked-worktree  1234abc  (detached HEAD)

```

The command also shows annotations for each worktree, according to its state. These annotations are:

locked, if the worktree is locked.

prunable, if the worktree can be pruned via git worktree prune.

```
$ git worktree list
/path/to/linked-worktree    abcd1234 [master]
/path/to/locked-worktree    acbd5678 (brancha) locked
/path/to/prunable-worktree  5678abc  (detached HEAD) prunable

```

For these annotations, a reason might also be available and this can be seen using the verbose mode. The annotation is then moved to the next line indented followed by the additional information.

```
$ git worktree list --verbose
/path/to/linked-worktree              abcd1234 [master]
/path/to/locked-worktree-no-reason    abcd5678 (detached HEAD) locked
/path/to/locked-worktree-with-reason  1234abcd (brancha)
	locked: worktree path is mounted on a portable device
/path/to/prunable-worktree            5678abc1 (detached HEAD)
	prunable: gitdir file points to non-existent location

```

Note that the annotation is moved to the next line if the additional information is available, otherwise it stays on the same line as the worktree itself.
