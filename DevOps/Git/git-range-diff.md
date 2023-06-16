# Git range diff

Compare two commit ranges (e.g. two versions of a branch).

This command shows the differences between two versions of a patch series, or more generally, two commit ranges (ignoring merge commits).

In the presence of <path> arguments, these commit ranges are limited accordingly.

To that end, it first finds pairs of commits from both commit ranges that correspond with each other. Two commits are said to correspond when the diff between their patches (i.e. the author information, the commit message and the commit diff) is reasonably small compared to the patches' size. See `Algorithm` below for details.

Finally, the list of matching commits is shown in the order of the second commit range, with unmatched commits being inserted just after all of their ancestors have been shown.

There are three ways to specify the commit ranges:

- <range1> <range2>: Either commit range can be of the form <base>..
- <rev>, <rev>^! or <rev>^-<n>. See SPECIFYING RANGES in gitrevisions[7] for more details.
- <rev1>...<rev2>. This is equivalent to <rev2>..<rev1> <rev1>..<rev2>.
- <base> <rev1> <rev2>: This is equivalent to <base>..<rev1> <base>..<rev2>.

## Options

[Options](https://git-scm.com/docs/git-range-diff#_options)

## Examples

When a rebase required merge conflicts to be resolved, compare the changes introduced by the rebase directly afterwards using:

```
$ git range-diff @{u} @{1} @
```

A typical output of git range-diff would look like this:

```
-:  ------- > 1:  0ddba11 Prepare for the inevitable!
1:  c0debee = 2:  cab005e Add a helpful message at the start
2:  f00dbal ! 3:  decafe1 Describe a bug
    @@ -1,3 +1,3 @@
     Author: A U Thor <author@example.com>

    -TODO: Describe a bug
    +Describe a bug
    @@ -324,5 +324,6
      This is expected.

    -+What is unexpected is that it will also crash.
    ++Unexpectedly, it also crashes. This is a bug, and the jury is
    ++still out there how to fix it best. See ticket #314 for details.

      Contact
3:  bedead < -:  ------- TO-UNDO
```

In this example, there are 3 old and 3 new commits, where the developer removed the 3rd, added a new one before the first two, and modified the commit message of the 2nd commit as well its diff.

When the output goes to a terminal, it is color-coded by default, just like regular git diff's output. In addition, the first line (adding a commit) is green, the last line (deleting a commit) is red, the second line (with a perfect match) is yellow like the commit header of git show's output, and the third line colors the old commit red, the new one green and the rest like git show's commit header.

A naive color-coded diff of diffs is actually a bit hard to read, though, as it colors the entire lines red or green. The line that added "What is unexpected" in the old commit, for example, is completely red, even if the intent of the old commit was to add something.

To help with that, range uses the --dual-color mode by default. In this mode, the diff of diffs will retain the original diff colors, and prefix the lines with -/+ markers that have their background red or green, to make it more obvious that they describe how the diff itself changed.

```
 git range-diff gitdocs~3..gitdocs main~3..main

-:  ------- > 1:  4a115e6 Using -u as a parameter when executing git commit.
1:  69b8806 = 2:  69b8806 commit,describe,diff
2:  dd333ea = 3:  dd333ea log,maintenance, grep,gc,fetch,format-patch,init
3:  5a347e9 < -:  ------- merge,mv,notes, pull
```

TODO: FIND MORE INFO.
