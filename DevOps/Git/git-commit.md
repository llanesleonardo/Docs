# Git commit

Record changes to the repository.

Create a new commit containing the current contents of the index and the given log message describing the changes. The new commit is a direct child of HEAD, usually the tip of the current branch, and the branch is updated to point to it (unless no branch is associated with the working tree, in which case HEAD is "detached").

The content to be committed can be specified in several ways:

- by using git-add[1] to incrementally "add" changes to the index before using the commit command (Note: even modified files must be "added");
- by using git-rm[1] to remove files from the working tree and the index, again before using the commit command;
- by listing files as arguments to the commit command (without --interactive or --patch switch), in which case the commit will ignore changes staged in the index, and instead record the current content of the listed files (which must already be known to Git);
- by using the -a switch with the commit command to automatically "add" changes from all known files (i.e. all files that are already listed in the index) and to automatically "rm" files in the index that have been removed from the working tree, and then perform the actual commit;
- by using the --interactive or --patch switches with the commit command to decide one by one which files or hunks should be part of the commit in addition to contents in the index, before finalizing the operation. See the “Interactive Mode” section of git-add[1] to learn how to operate these modes.

The --dry-run option can be used to obtain a summary of what is included by any of the above for the next commit by giving the same set of parameters (options and paths).

If you make a commit and then find a mistake immediately after that, you can recover from it with git reset.

## Options

```
-a
--all
```

Tell the command to automatically stage files that have been modified and deleted, but new files you have not told Git about are not affected.

```
-p
--patch
```

Use the interactive patch selection interface to choose which changes to commit.

```
-C <commit>
--reuse-message=<commit>
```

Take an existing commit object, and reuse the log message and the authorship information (including the timestamp) when creating the commit.

```
-c <commit>
--reedit-message=<commit>
```

Like -C, but with -c the editor is invoked, so that the user can further edit the commit message.

```
--fixup=[(amend|reword):]<commit>

```

Create a new commit which "fixes up" <commit> when applied with git rebase --autosquash. Plain --fixup=<commit> creates a "fixup!" commit which changes the content of <commit> but leaves its log message untouched. --fixup=amend:<commit> is similar but creates an "amend!" commit which also replaces the log message of <commit> with the log message of the "amend!" commit. --fixup=reword:<commit> creates an "amend!" commit which replaces the log message of <commit> with its own log message but makes no changes to the content of <commit>.

The commit created by plain --fixup=<commit> has a subject composed of "fixup!" followed by the subject line from <commit>, and is recognized specially by git rebase --autosquash. The -m option may be used to supplement the log message of the created commit, but the additional commentary will be thrown away once the "fixup!" commit is squashed into <commit> by git rebase --autosquash.

The commit created by --fixup=amend:<commit> is similar but its subject is instead prefixed with "amend!". The log message of <commit> is copied into the log message of the "amend!" commit and opened in an editor so it can be refined. When git rebase --autosquash squashes the "amend!" commit into <commit>, the log message of <commit> is replaced by the refined log message from the "amend!" commit. It is an error for the "amend!" commit’s log message to be empty unless --allow-empty-message is specified.

--fixup=reword:<commit> is shorthand for --fixup=amend:<commit> --only. It creates an "amend!" commit with only a log message (ignoring any changes staged in the index). When squashed by git rebase --autosquash, it replaces the log message of <commit> without making any other changes.

Neither "fixup!" nor "amend!" commits change authorship of <commit> when applied by git rebase --autosquash. See git-rebase[1] for details.

```
--squash=<commit>

```

Construct a commit message for use with rebase --autosquash. The commit message subject line is taken from the specified commit with a prefix of "squash! ". Can be used with additional commit message options (-m/-c/-C/-F). See git-rebase[1] for details.

```
--branch
```

Show the branch and tracking info even in short-format.

```
--porcelain
```

When doing a dry-run, give the output in a porcelain-ready format. See git-status[1] for details. Implies --dry-run.

```
--long
```

When doing a dry-run, give the output in the long-format. Implies --dry-run.

```
-F <file>
--file=<file>
```

Take the commit message from the given file. Use - to read the message from the standard input.

```
-m <msg>
--message=<msg>
```

Use the given <msg> as the commit message. If multiple -m options are given, their values are concatenated as separate paragraphs.

The -m option is mutually exclusive with -c, -C, and -F.

```
-s
--signoff
--no-signoff
```

Add a Signed-off-by trailer by the committer at the end of the commit log message. The meaning of a signoff depends on the project to which you’re committing. For example, it may certify that the committer has the rights to submit the work under the project’s license or agrees to some contributor representation, such as a Developer Certificate of Origin. (See http://developercertificate.org for the one used by the Linux kernel and Git projects.) Consult the documentation or leadership of the project to which you’re contributing to understand how the signoffs are used in that project.

The --no-signoff option can be used to countermand an earlier --signoff option on the command line.

```
-e
--edit
```

The message taken from file with -F, command line with -m, and from commit object with -C are usually used as the commit log message unmodified. This option lets you further edit the message taken from these sources.

```
--amend
```

Replace the tip of the current branch by creating a new commit. The recorded tree is prepared as usual (including the effect of the -i and -o options and explicit pathspec), and the message from the original commit is used as the starting point, instead of an empty message, when no other message is specified from the command line via options such as -m, -F, -c, etc. The new commit has the same parents and author as the current one (the --reset-author option can countermand this).

It can be used to amend a merge commit.

You should understand the implications of rewriting history if you amend a commit that has already been published.

```
-u[<mode>]
--untracked-files[=<mode>]
```

Show untracked files.

The mode parameter is optional (defaults to all), and is used to specify the handling of untracked files; when -u is not used, the default is normal, i.e. show untracked files and directories.

The possible options are:

no - Show no untracked files

normal - Shows untracked files and directories

all - Also shows individual files in untracked directories.
