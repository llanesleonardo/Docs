# Git log

Show commit logs.

List commits that are reachable by following the parent links from the given commit(s), but exclude commits that are reachable from the one(s) given with a ^ in front of them. The output is given in reverse chronological order by default.

You can think of this as a set operation. Commits reachable from any of the commits given on the command line form a set, and then commits reachable from any of the ones given with ^ in front are subtracted from that set. The remaining commits are what comes out in the command’s output. Various other options and paths parameters can be used to further limit the result.

## Options

```
--follow
```

Continue listing the history of a file beyond renames (works only for a single file).

```
--no-decorate
--decorate[=short|full|auto|no]
```

Print out the ref names of any commits that are shown. If short is specified, the ref name prefixes refs/heads/, refs/tags/ and refs/remotes/ will not be printed. If full is specified, the full ref name (including prefix) will be printed. If auto is specified, then if the output is going to a terminal, the ref names are shown as if short were given, otherwise no ref names are shown. The option --decorate is short-hand for --decorate=short. Default to configuration value of log.decorate if configured, otherwise, auto.

```
--source
```

Print out the ref name given on the command line by which each commit was reached.

```
-[no-]mailmap
--[no-]use-mailmap
```

Use mailmap file to map author and committer names and email addresses to canonical real names and email addresses.

```
-<number>
-n <number>
--max-count=<number>
```

Limit the number of commits to output.

```
--skip=<number>

```

Skip number commits before starting to show the commit output.

```
--since=<date>
--after=<date>`
```

Show commits more recent than a specific date.

```
--author=<pattern>
--committer=<pattern>
```

Limit the commits output to ones with author/committer header lines that match the specified pattern (regular expression). With more than one --author=<pattern>, commits whose author matches any of the given patterns are chosen (similarly for multiple --committer=<pattern>).

```
--merges
```

Print only merge commits.

```
--all
```

Pretend as if all the refs in refs/, along with HEAD, are listed on the command line as <commit>.

```
--branches[=<pattern>]
```

Pretend as if all the refs in refs/heads are listed on the command line as <commit>. If <pattern> is given, limit branches to ones matching given shell glob. If pattern lacks ?, _, or [, /_ at the end is implied.

```
--tags[=<pattern>]
```

Pretend as if all the refs in refs/tags are listed on the command line as <commit>. If <pattern> is given, limit tags to ones matching given shell glob. If pattern lacks ?, _, or [, /_ at the end is implied.

```
--cherry-pick
```

Omit any commit that introduces the same change as another commit on the “other side” when the set of commits are limited with symmetric difference.

```
--pretty[=<format>]
--format=<format>
```

Pretty-print the contents of the commit logs in a given format, where <format> can be one of oneline, short, medium, full, fuller, reference, email, raw, format:<string> and tformat:<string>. When <format> is none of the above, and has %placeholder in it, it acts as if --pretty=tformat:<format> were given.

```
--oneline
```

This is a shorthand for "--pretty=oneline --abbrev-commit" used together.

```
--parents
```

Print also the parents of the commit (in the form "commit parent…​"). Also enables parent rewriting, see History Simplification above.

```
--children
```

Print also the children of the commit (in the form "commit child…​"). Also enables parent rewriting, see History Simplification above.

```
--graph
```

Draw a text-based graphical representation of the commit history on the left hand side of the output. This may cause extra lines to be printed in between commits, in order for the graph history to be drawn properly. Cannot be combined with --no-walk.

## Examples

```
git log --no-merges
```

Show the whole commit history, but skip any merges

```
git log v2.6.12.. include/scsi drivers/scsi
```

Show all commits since version v2.6.12 that changed any file in the include/scsi or drivers/scsi subdirectories

```
git log --since="2 weeks ago" -- gitk
```

Show the changes during the last two weeks to the file gitk. The -- is necessary to avoid confusion with the branch named gitk

```
git log --name-status release..test
```

Show the commits that are in the "test" branch but not yet in the "release" branch, along with the list of paths each commit modifies.

```
git log --follow builtin/rev-list.c
```

Shows the commits that changed builtin/rev-list.c, including those commits that occurred before the file was given its present name.

```
git log --branches --not --remotes=origin
```

Shows all commits that are in any of local branches but not in any of remote-tracking branches for origin (what you have that origin doesn’t).

```
git log master --not --remotes=\*/master
```

Shows all commits that are in local master but not in any remote repository master branches.

```
git log -p -m --first-parent
```

Shows the history including change diffs, but only from the “main branch” perspective, skipping commits that come from merged branches, and showing full diffs of changes introduced by the merges. This makes sense only when following a strict policy of merging all topic branches when staying on a single integration branch.

```
git log -L '/int main/',/^}/:main.c
```

Shows how the function main() in the file main.c evolved over time.

```
git log -3
```

Limits the number of commits to show to 3.
