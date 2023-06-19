# Git merge-tree

Perform merge without touching index or working tree.

This command has a modern --write-tree mode and a deprecated --trivial-merge mode. With the exception of the DEPRECATED DESCRIPTION section at the end, the rest of this documentation describes modern --write-tree mode.

Performs a merge, but does not make any new commits and does not read from or write to either the working tree or index.

The performed merge will use the same feature as the "real" git-merge[1], including:

- three way content merges of individual files
- rename detection
- proper directory/file conflict handling
- recursive ancestor consolidation (i.e. when there is more than one merge base, creating a virtual merge base by merging the merge bases)

After the merge completes, a new toplevel tree object is created. See OUTPUT below for details.

## Options

[Options](https://git-scm.com/docs/git-merge-tree#_options)
