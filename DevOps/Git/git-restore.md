# Git restore

Restore working tree files.

Restore specified paths in the working tree with some contents from a restore source. If a path is tracked but does not exist in the restore source, it will be removed to match the source.

The command can also be used to restore the content in the index with --staged, or restore both the working tree and the index with --staged --worktree.

By default, if --staged is given, the contents are restored from HEAD, otherwise from the index. Use --source to restore from a different commit.

See "Reset, restore and revert" in git[1] for the differences between the three commands.

THIS COMMAND IS EXPERIMENTAL. THE BEHAVIOR MAY CHANGE.

## Options

[Options](https://git-scm.com/docs/git-restore#_options)

## Examples

The following sequence switches to the master branch, reverts the Makefile to two revisions back, deletes hello.c by mistake, and gets it back from the index.

```
$ git switch master
$ git restore --source master~2 Makefile  (1)
$ rm -f hello.c
$ git restore hello.c                     (2)
```

take a file out of another commit

restore hello.c from the index

If you want to restore all C source files to match the version in the index, you can say

```
$ git restore '*.c'
```

Note the quotes around \*.c. The file hello.c will also be restored, even though it is no longer in the working tree, because the file globbing is used to match entries in the index (not in the working tree by the shell).

To restore all files in the current directory

```
$ git restore .
```

or to restore all working tree files with top pathspec magic (see gitglossary[7])

```
$ git restore :/

```

To restore a file in the index to match the version in HEAD (this is the same as using git-reset[1])

```
$ git restore --staged hello.c
```

or you can restore both the index and the working tree (this the same as using git-checkout[1])

```
$ git restore --source=HEAD --staged --worktree hello.c
```

or the short form which is more practical but less readable:

```
$ git restore -s@ -SW hello.c
```
