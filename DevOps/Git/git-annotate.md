# Git annotate

Annotates each line in the given file with information from the commit which introduced the line. Optionally annotates from a given revision.

The only difference between this command and git-blame[1] is that they use slightly different output formats, and this command exists only for backward compatibility to support existing scripts, and provide a more familiar command name for people coming from other SCM systems.

## Options

```
-b
```

Show blank SHA-1 for boundary commits.

```
--root
```

Do not treat root commits as boundaries. This can also be controlled via the blame.showRoot config option.

```
--show-stats
```

Include additional statistics at the end of blame output.

```
-l
```

Show long rev (Default: off).

```
-t
```

Show raw timestamp (Default: off).

```
--first-parent
```

Follow only the first parent commit upon seeing a merge commit. This option can be used to determine when a line was introduced to a particular integration branch, rather than when it was introduced to the history overall.

```
--contents <file>
```

Annotate using the contents from the named file, starting from <rev> if it is specified, and HEAD otherwise. You may specify - to make the command read from the standard input for the file contents.

```
--date <format>
```

Specifies the format used to output dates. If --date is not provided, the value of the blame.date config variable is used. If the blame.date config variable is also not set, the iso format is used.

```
--[no-]progress
```

Progress status is reported on the standard error stream by default when it is attached to a terminal. This flag enables progress reporting even if not attached to a terminal. Can’t use --progress together with --porcelain or --incremental.

```
-M[<num>]
```

Detect moved or copied lines within a file. When a commit moves or copies a block of lines (e.g. the original file has A and then B, and the commit changes it to B and then A), the traditional blame algorithm notices only half of the movement and typically blames the lines that were moved up (i.e. B) to the parent and assigns blame to the lines that were moved down (i.e. A) to the child commit. With this option, both groups of lines are blamed on the parent by running extra passes of inspection.

<num> is optional but it is the lower bound on the number of alphanumeric characters that Git must detect as moving/copying within a file for it to associate those lines with the parent commit. The default value is 20.

```
-C[<num>]
```

In addition to -M, detect lines moved or copied from other files that were modified in the same commit. This is useful when you reorganize your program and move code around across files. When this option is given twice, the command additionally looks for copies from other files in the commit that creates the file. When this option is given three times, the command additionally looks for copies from other files in any commit.

<num> is optional but it is the lower bound on the number of alphanumeric characters that Git must detect as moving/copying between files for it to associate those lines with the parent commit. And the default value is 40. If there are more than one -C options given, the <num> argument of the last -C will take effect.
