# Git describe

Give an object a human readable name based on an available ref.

The command finds the most recent tag that is reachable from a commit. If the tag points to the commit, then only the tag is shown. Otherwise, it suffixes the tag name with the number of additional commits on top of the tagged object and the abbreviated object name of the most recent commit. The result is a "human-readable" object name which can also be used to identify the commit to other git commands.

By default (without --all or --tags) git describe only shows annotated tags.

If the given object refers to a blob, it will be described as <commit-ish>:<path>, such that the blob can be found at <path> in the <commit-ish>, which itself describes the first commit in which this blob occurs in a reverse revision walk from HEAD.

```
<commit-ish>…​
```

Commit-ish object names to describe. Defaults to HEAD if omitted.

```
--dirty[=<mark>]
--broken[=<mark>]
```

Describe the state of the working tree. When the working tree matches HEAD, the output is the same as "git describe HEAD". If the working tree has local modification "-dirty" is appended to it. If a repository is corrupt and Git cannot determine if there is local modification, Git will error out, unless ‘--broken’ is given, which appends the suffix "-broken" instead.

```
--all
```

Instead of using only the annotated tags, use any ref found in refs/ namespace. This option enables matching any known branch, remote-tracking branch, or lightweight tag.

```
--tags
```

Instead of using only the annotated tags, use any tag found in refs/tags namespace. This option enables matching a lightweight (non-annotated) tag.

```
--contains
```

Instead of finding the tag that predates the commit, find the tag that comes after the commit, and thus contains it. Automatically implies --tags.

```
--abbrev=<n>
```

Instead of using the default number of hexadecimal digits (which will vary according to the number of objects in the repository with a default of 7) of the abbreviated object name, use <n> digits, or as many digits as needed to form a unique object name. An <n> of 0 will suppress long format, only showing the closest tag.

```
--debug
```

Verbosely display information about the searching strategy being employed to standard error. The tag name will still be printed to standard out.

## Examples

With something like git.git current tree, I get:

```
[torvalds@g5 git]$ git describe parent
v1.0.4-14-g2414721
```

i.e. the current head of my "parent" branch is based on v1.0.4, but since it has a few commits on top of that, describe has added the number of additional commits ("14") and an abbreviated object name for the commit itself ("2414721") at the end.

Doing a git describe on a tag-name will just show the tag name:

```
[torvalds@g5 git]$ git describe v1.0.4
v1.0.4
```

With --all, the command can use branch heads as references, so the output shows the reference path as well:

```
[torvalds@g5 git]$ git describe --all --abbrev=4 v1.0.5^2
tags/v1.0.0-21-g975b
```

```
[torvalds@g5 git]$ git describe --all --abbrev=4 HEAD^
heads/lt/describe-7-g975b
```

With --abbrev set to 0, the command can be used to find the closest tagname without any suffix:

```
[torvalds@g5 git]$ git describe --abbrev=0 v1.0.5^2
tags/v1.0.0
```

TODO: CREATE A TAG AND TRY THIS CODE

## Search strategy

For each commit-ish supplied, git describe will first look for a tag which tags exactly that commit. Annotated tags will always be preferred over lightweight tags, and tags with newer dates will always be preferred over tags with older dates. If an exact match is found, its name will be output and searching will stop.

If an exact match was not found, git describe will walk back through the commit history to locate an ancestor commit which has been tagged. The ancestor’s tag will be output along with an abbreviation of the input commit-ish’s SHA-1. If --first-parent was specified then the walk will only consider the first parent of each commit.

If multiple tags were found during the walk then the tag which has the fewest commits different from the input commit-ish will be selected and output. Here fewest commits different is defined as the number of commits which would be shown by git log tag..input will be the smallest number of commits possible.
