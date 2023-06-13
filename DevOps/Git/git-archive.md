# Git archive

Create an archive of files from a named tree.

```
git archive [--format=<format>] [--output=<output>] [<commit>]

```

Creates an archive of the specified format containing the tree structure for the named tree, and writes it out to the standard output. If <prefix> is specified it is prepended to the filenames in the archive.

git archive behaves differently when given a tree ID versus when given a commit ID or tag ID. In the first case the current time is used as the modification time of each file in the archive. In the latter case the commit time as recorded in the referenced commit object is used instead. Additionally the commit ID is stored in a global extended pax header if the tar format is used; it can be extracted using git get-tar-commit-id. In ZIP files it is stored as a file comment.

Note that git archive only includes the contents of the specified commit or tree; it does not include the entire repository's history or metadata.

## Options

```
--format=<fmt>
```

Format of the resulting archive. Possible values are tar, zip, tar.gz, tgz, and any format defined using the configuration option tar.<format>.command. If --format is not given, and the output file is specified, the format is inferred from the filename if possible (e.g. writing to foo.zip makes the output to be in the zip format). Otherwise the output format is tar.

---

```
-l
--list

```

Show all available formats.

---

```
--prefix=<prefix>/

```

Prepend <prefix>/ to paths in the archive. Can be repeated; its rightmost value is used for all tracked files.

---

```
-o <file>
--output=<file>

```

Write the archive to <file> instead of stdout.

---

## Examples

More: [Examples](https://git-scm.com/docs/git-archive#_examples)
