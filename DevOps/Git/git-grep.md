# Git grep

Print lines matching a pattern.

Look for specified patterns in the tracked files in the work tree, blobs registered in the index file, or blobs in given tree objects. Patterns are lists of one or more search expressions separated by newline characters. An empty string as search expression matches all lines.

The git grep command in Git allows you to search for a specific pattern or regular expression within your repository. It searches through the contents of files in your repository, including commit history, and displays the matching lines.

1. Open your terminal or command prompt.
2. Navigate to the Git repository directory where you want to perform the search.
3. Run the following command to search for a pattern or regular expression:

```
git grep <pattern>
# git grep example

```

Replace <pattern> with the specific pattern or regular expression you want to search for. For example, if you want to search for the word "example" in your repository, you can use:

```
git grep example
```

By default, git grep searches all tracked files in the repository.

Git will display the matching lines that contain the specified pattern, along with the file name and line number where the match was found.

Example output:

```
path/to/file.txt:42:This is an example line.
path/to/another-file.txt:10:Another example line.

```

The output shows the file paths, line numbers, and the lines themselves that contain the matching pattern.

---

```
--cached
```

Instead of searching tracked files in the working tree, search blobs registered in the index file.

```
--no-index
```

Search files in the current directory that is not managed by Git.

```
--untracked

```

In addition to searching in the tracked files in the working tree, search also in untracked files.

```
--no-exclude-standard

```

Also search in ignored files by not honoring the .gitignore mechanism. Only useful with --untracked.

```
--exclude-standard

```

Do not pay attention to ignored files specified via the .gitignore mechanism. Only useful when searching files in the current directory with --no-index.

```
-a
--text
```

Process binary files as if they were text.

```
-i
--ignore-case
```

Ignore case differences between the patterns and the files.

```
-r
--recursive
```

Same as --max-depth=-1; this is the default.

```
--full-name
```

When run from a subdirectory, the command usually outputs paths relative to the current directory. This option forces paths to be output relative to the project top directory.

```
-c
--count
#DevOps/Git/git-diff.md:2
#DevOps/GitHub/pullrequest.md:1
```

Instead of showing every matched line, show the number of lines that match.

```
--color[=<when>]
```

Show colored matches. The value must be always (the default), never, or auto.

```
--break
```

Print an empty line between matches from different files.

```
--heading

DevOps/Git/git-diff.md
[Diff Options](https://git-scm.com/docs/git-diff#_options)
[Git diff examples](https://git-scm.com/docs/git-diff#_examples)
DevOps/GitHub/pullrequest.md
- [Git diff options](https://git-scm.com/docs/git-diff#git-diff-emgitdiffemltoptionsgtltcommitgtltcommitgt--ltpathgt82308203)
```

Show the filename above the matches in that file instead of at the start of each shown line.

## Examples

```
git grep 'time_t' -- '\*.[ch]'
```

Looks for time_t in all tracked .c and .h files in the working directory and its subdirectories.

```
git grep -e '#define' --and \( -e MAX_PATH -e PATH_MAX \)
```

Looks for a line that has #define and either MAX_PATH or PATH_MAX.

```
git grep --all-match -e NODE -e Unexpected
```

Looks for a line that has NODE or Unexpected in files that have lines that match both.

```
git grep solution -- :^Documentation
```

Looks for solution, excluding files in Documentation.
