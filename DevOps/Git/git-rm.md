# Git rm

Remove files from the working tree and from the index.

Remove files matching pathspec from the index, or from the working tree and the index. git rm will not remove a file from just your working directory. (There is no option to remove a file only from the working tree and yet keep it in the index; use /bin/rm if you want to do that.) The files being removed have to be identical to the tip of the branch, and no updates to their contents can be staged in the index, though that default behavior can be overridden with the -f option. When --cached is given, the staged content has to match either the tip of the branch or the file on disk, allowing the file to be removed from just the index. When sparse-checkouts are in use (see git-sparse-checkout[1]), git rm will only remove paths within the sparse-checkout patterns.

## Options

```
<pathspec>…​
```

Files to remove. A leading directory name (e.g. dir to remove dir/file1 and dir/file2) can be given to remove all files in the directory, and recursively all sub-directories, but this requires the -r option to be explicitly given.

The command removes only the paths that are known to Git.

File globbing matches across directory boundaries. Thus, given two directories d and d2, there is a difference between using git rm 'd*' and git rm 'd/*', as the former will also remove all of directory d2.

```
-f
--force
```

Override the up-to-date check.

```
-n
--dry-run
```

Don’t actually remove any file(s). Instead, just show if they exist in the index and would otherwise be removed by the command.

```
-r
```

Allow recursive removal when a leading directory name is given.

```
--
```

This option can be used to separate command-line options from the list of files, (useful when filenames might be mistaken for command-line options).

```
--cached
```

Use this option to unstage and remove paths only from the index. Working tree files, whether modified or not, will be left alone.

```
--ignore-unmatch
```

Exit with a zero status even if no files matched.

## Examples

```
git rm Documentation/\*.txt
```

Removes all \*.txt files from the index that are under the Documentation directory and any of its subdirectories.

Note that the asterisk \* is quoted from the shell in this example; this lets Git, and not the shell, expand the pathnames of files and subdirectories under the Documentation/ directory.

```
git rm -f git-*.sh
```

Because this example lets the shell expand the asterisk (i.e. you are listing the files explicitly), it does not remove subdir/git-foo.sh.
