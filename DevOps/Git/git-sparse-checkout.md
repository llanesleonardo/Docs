# Git sparse-checkout

Reduce your working tree to a subset of tracked files.

This command is used to create sparse checkouts, which change the working tree from having all tracked files present to only having a subset of those files. It can also switch which subset of files are present, or undo and go back to having all tracked files present in the working copy.

The subset of files is chosen by providing a list of directories in cone mode (the default), or by providing a list of patterns in non-cone mode.

When in a sparse-checkout, other Git commands behave a bit differently. For example, switching branches will not update paths outside the sparse-checkout directories/patterns, and git commit -a will not record paths outside the sparse-checkout directories/patterns as deleted.

## Examples

```
git sparse-checkout set MY/DIR1 SUB/DIR2
```

Change to a sparse checkout with all files (at any depth) under MY/DIR1/ and SUB/DIR2/ present in the working copy (plus all files immediately under MY/ and SUB/ and the toplevel directory). If already in a sparse checkout, change which files are present in the working copy to this new selection. Note that this command will also delete all ignored files in any directory that no longer has either tracked or non-ignored-untracked files present.

```
git sparse-checkout disable
```

Repopulate the working directory with all files, disabling sparse checkouts.

```
git sparse-checkout add SOME/DIR/ECTORY
```

Add all files under SOME/DIR/ECTORY/ (at any depth) to the sparse checkout, as well as all files immediately under SOME/DIR/ and immediately under SOME/. Must already be in a sparse checkout before using this command.

```
git sparse-checkout reapply
```

It is possible for commands to update the working tree in a way that does not respect the selected sparsity directories. This can come from tools external to Git writing files, or even affect Git commands because of either special cases (such as hitting conflicts when merging/rebasing), or because some commands didn’t fully support sparse checkouts (e.g. the old recursive merge backend had only limited support). This command reapplies the existing sparse directory specifications to make the working directory match.

TODO: FIND MORE INFO.
