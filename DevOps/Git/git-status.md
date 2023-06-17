# Git status

Show the working tree status.

Displays paths that have differences between the index file and the current HEAD commit, paths that have differences between the working tree and the index file, and paths in the working tree that are not tracked by Git.

The first are what you would commit by running git commit; the second and third are what you could commit by running git add before running git commit.

## Options

```
-s
--short
```

Give the output in the short-format.

```
-b
--branch
```

Show the branch and tracking info even in short-format.

```
--show-stash
```

Show the number of entries currently stashed away.

```
-u[<mode>]
--untracked-files[=<mode>]
```

Show untracked files.

The mode parameter is used to specify the handling of untracked files. It is optional: it defaults to all, and if specified, it must be stuck to the option (e.g. -uno, but not -u no).

The possible options are:

- no - Show no untracked files.
- normal - Shows untracked files and directories.
- all - Also shows individual files in untracked directories.

When -u option is not used, untracked files and directories are shown (i.e. the same as specifying normal), to help you avoid forgetting to add newly created files. Because it takes extra work to find untracked files in the filesystem, this mode may take some time in a large working tree. Consider enabling untracked cache and split index if supported (see git update-index --untracked-cache and git update-index --split-index), Otherwise you can use no to have git status return more quickly without showing untracked files.

The default can be changed using the status.showUntrackedFiles configuration variable documented in git-config[1].

```
--ignore-submodules[=<when>]
```

Ignore changes to submodules when looking for changes. <when> can be either "none", "untracked", "dirty" or "all", which is the default. Using "none" will consider the submodule modified when it either contains untracked or modified files or its HEAD differs from the commit recorded in the superproject and can be used to override any settings of the ignore option in git-config[1] or gitmodules[5]. When "untracked" is used submodules are not considered dirty when they only contain untracked content (but they are still scanned for modified content). Using "dirty" ignores all changes to the work tree of submodules, only changes to the commits stored in the superproject are shown (this was the behavior before 1.7.0). Using "all" hides all changes to submodules (and suppresses the output of submodule summaries when the config option status.submoduleSummary is set).

```
--ignored[=<mode>]
```

Show ignored files as well.

The mode parameter is used to specify the handling of ignored files. It is optional: it defaults to traditional.

The possible options are:

- traditional - Shows ignored files and directories, unless --untracked-files=all is specified, in which case individual files in ignored directories are displayed.
- no - Show no ignored files.
- matching - Shows ignored files and directories matching an ignore pattern.

When matching mode is specified, paths that explicitly match an ignored pattern are shown. If a directory matches an ignore pattern, then it is shown, but not paths contained in the ignored directory. If a directory does not match an ignore pattern, but all contents are ignored, then the directory is not shown, but all contents are shown.
