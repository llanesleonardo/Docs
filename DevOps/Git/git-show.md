# Git show

Show various types of objects.

Shows one or more objects (blobs, trees, tags and commits).

For commits it shows the log message and textual diff. It also presents the merge commit in a special format as produced by git diff-tree --cc.

For tags, it shows the tag message and the referenced objects.

For trees, it shows the names (equivalent to git ls-tree with --name-only).

For plain blobs, it shows the plain contents.

The command takes options applicable to the git diff-tree command to control how the changes the commit introduces are shown.

## Options

```
<object>…​
```

The names of objects to show (defaults to HEAD).

```
--pretty[=<format>]
--format=<format>
```

Pretty-print the contents of the commit logs in a given format, where <format> can be one of oneline, short, medium, full, fuller, reference, email, raw, format:<string> and tformat:<string>. When <format> is none of the above, and has %placeholder in it, it acts as if --pretty=tformat:<format> were given.

```
--oneline
```

This is a shorthand for "--pretty=oneline --abbrev-commit" used together.

## Pretty formats

[Pretty formats](https://git-scm.com/docs/git-show#_pretty_formats)

## Diff Formatting

[Diff formatting](https://git-scm.com/docs/git-show#_diff_formatting)

## Examples

```
git show v1.0.0
```

Shows the tag v1.0.0, along with the object the tags points at.

```
git show v1.0.0^{tree}
```

Shows the tree pointed to by the tag v1.0.0.

```
git show -s --format=%s v1.0.0^{commit}
```

Shows the subject of the commit pointed to by the tag v1.0.0.

```
git show next~10:Documentation/README
```

Shows the contents of the file Documentation/README as they were current in the 10th last commit of the branch next.

```
git show master:Makefile master:t/Makefile
```

Concatenates the contents of said Makefiles in the head of the branch master.
