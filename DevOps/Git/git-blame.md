# Git blame

Show what revision and author last modified each line of a file.

Annotates each line in the given file with information from the revision which last modified the line. Optionally, start annotating from the given revision.

When specified one or more times, -L restricts annotation to the requested lines.

The origin of lines is automatically followed across whole-file renames (currently there is no option to turn the rename-following off). To follow lines moved from one file to another, or to follow lines that were copied and pasted from another file, etc., see the -C and -M options.

The report does not tell you anything about lines which have been deleted or replaced; you need to use a tool such as git diff or the "pickaxe" interface briefly mentioned in the following paragraph.

Apart from supporting file annotation, Git also supports searching the development history for when a code snippet occurred in a change. This makes it possible to track when a code snippet was added to a file, moved or copied between files, and eventually deleted or replaced. It works by searching for a text string in the diff. A small example of the pickaxe interface that searches for blame_usage:

```
$ git log --pretty=oneline -S'blame_usage'
5040f17eba15504bad66b14a645bddd9b015ebb7 blame -S <ancestry-file>
ea4c7f9bf69e781dd0cd88d2bccb2bf5cc15c9a7 git-blame: Make the output
```

## Options

```
-b
```

Show blank SHA-1 for boundary commits. This can also be controlled via the blame.blankBoundary config option.

```
--root
```

Do not treat root commits as boundaries. This can also be controlled via the blame.showRoot config option.

```
--show-stats
```

Include additional statistics at the end of blame output.

```
-L <start>,<end>
-L :<funcname>
```

Annotate only the line range given by <start>,<end>, or by the function name regex <funcname>. May be specified multiple times. Overlapping ranges are allowed.

<start> and <end> are optional. -L <start> or -L <start>, spans from <start> to end of file. -L ,<end> spans from start of file to <end>.

<start> and <end> can take one of these forms:

number

If <start> or <end> is a number, it specifies an absolute line number (lines count from 1).

/regex/

This form will use the first line matching the given POSIX regex. If <start> is a regex, it will search from the end of the previous -L range, if any, otherwise from the start of file. If <start> is ^/regex/, it will search from the start of file. If <end> is a regex, it will search starting at the line given by <start>.

+offset or -offset

This is only valid for <end> and will specify a number of lines before or after the line given by <start>.

If :<funcname> is given in place of <start> and <end>, it is a regular expression that denotes the range from the first funcname line that matches <funcname>, up to the next funcname line. :<funcname> searches from the end of the previous -L range, if any, otherwise from the start of file. ^:<funcname> searches from the start of file. The function names are determined in the same way as git diff works out patch hunk headers (see Defining a custom hunk-header in gitattributes[5]).

```
-l
```

Show long rev (Default: off).

```
-t
```

Show raw timestamp (Default: off).

```
-S <revs-file>
```

Use revisions from revs-file instead of calling git-rev-list[1].

```
--reverse <rev>..<rev>
```

Walk history forward instead of backward. Instead of showing the revision in which a line appeared, this shows the last revision in which a line has existed. This requires a range of revision like START..END where the path to blame exists in START. git blame --reverse START is taken as git blame --reverse START..HEAD for convenience.

```
--first-parent
```

Follow only the first parent commit upon seeing a merge commit. This option can be used to determine when a line was introduced to a particular integration branch, rather than when it was introduced to the history overall.

```
--color-lines
```

Color line annotations in the default format differently if they come from the same commit as the preceding line. This makes it easier to distinguish code blocks introduced by different commits. The color defaults to cyan and can be adjusted using the color.blame.repeatedLines config option.

```
--color-by-age
```

Color line annotations depending on the age of the line in the default format. The color.blame.highlightRecent config option controls what color is used for each range of age.

```
-f
--show-name
```

Show the filename in the original commit. By default the filename is shown if there is any line that came from a file with a different name, due to rename detection.

```
-n
--show-number
```

Show the line number in the original commit (Default: off).

```
-s
```

Suppress the author name and timestamp from the output.

```
-e
--show-email
```

Show the author email instead of author name (Default: off). This can also be controlled via the blame.showEmail config option.

```
-w
```

Ignore whitespace when comparing the parent’s version and the child’s to find where the lines came from.

## Specifying ranges

[Specifying ranges](https://git-scm.com/docs/git-blame#_specifying_ranges)

## Examples

https://www.youtube.com/watch?v=8uuueHkWy-E
