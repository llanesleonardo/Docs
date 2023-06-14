# Git clean

Remove untracked files from the working tree.

Cleans the working tree by recursively removing files that are not under version control, starting from the current directory.

Normally, only files unknown to Git are removed, but if the -x option is specified, ignored files are also removed. This can, for example, be useful to remove all build products.

If any optional <pathspec>... arguments are given, only those paths that match the pathspec are affected.

## Options

```
-d

```

Normally, when no <pathspec> is specified, git clean will not recurse into untracked directories to avoid removing too much. Specify -d to have it recurse into such directories as well. If a <pathspec> is specified, -d is irrelevant; all untracked files matching the specified paths (with exceptions for nested git directories mentioned under --force) will be removed.

```
-f
--force
```

If the Git configuration variable clean.requireForce is not set to false, git clean will refuse to delete files or directories unless given -f or -i. Git will refuse to modify untracked nested git repositories (directories with a .git subdirectory) unless a second -f is given.

```
-i
--interactive
```

Show what would be done and clean files interactively. See “Interactive mode” for details.

[Interactive mode](https://git-scm.com/docs/git-clean#_interactive_mode)

```
-n
--dry-run
```

Don’t actually remove anything, just show what would be done.

```
-e <pattern>
--exclude=<pattern>
```

Use the given exclude pattern in addition to the standard ignore rules (see gitignore[5]).

```
-X
```

Remove only files ignored by Git. This may be useful to rebuild everything from scratch, but keep manually created files.
