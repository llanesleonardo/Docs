# Git diff

Show changes between commits, commit and working tree, etc.

Show changes between the working tree and the index or a tree, changes between the index and a tree, changes between two trees, changes resulting from a merge, changes between two blob objects, or changes between two files on disk.

## Options

[Diff Options](https://git-scm.com/docs/git-diff#_options)

## Examples

[Git diff examples](https://git-scm.com/docs/git-diff#_examples)

Various ways to check your working tree:

```
$ git diff            (1)
$ git diff --cached   (2)
$ git diff HEAD       (3)
```

1. Changes in the working tree not yet staged for the next commit.
2. Changes between the index and your last commit; what you would be committing if you run git commit without -a option.
3. Changes in the working tree since your last commit; what you would be committing if you run git commit -a

Comparing with arbitrary commits

```
$ git diff test            (1)
$ git diff HEAD -- ./test  (2)
$ git diff HEAD^ HEAD      (3)
```

Instead of using the tip of the current branch, compare with the tip of "test" branch.

Instead of comparing with the tip of "test" branch, compare with the tip of the current branch, but limit the comparison to the file "test".

Compare the version before the last commit and the last commit.

Comparing branches

```
$ git diff topic master    (1)
$ git diff topic..master   (2)
$ git diff topic...master  (3)
```

Changes between the tips of the topic and the master branches.

Same as above.

Changes that occurred on the master branch since when the topic branch was started off it.

Limiting the diff output

```
$ git diff --diff-filter=MRC            (1)
$ git diff --name-status                (2)
$ git diff arch/i386 include/asm-i386   (3)
```

- Show only modification, rename, and copy, but not addition or deletion.
- Show only names and the nature of change, but not actual diff output.
- Limit diff output to named subtrees.

```
Munging the diff output
$ git diff --find-copies-harder -B -C  (1)
$ git diff -R                          (2)
```

Spend extra cycles to find renames, copies and complete rewrites (very expensive).

Output diff in reverse.
