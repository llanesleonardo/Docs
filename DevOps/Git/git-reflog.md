# Git reflog

Manage reflog information.

This command manages the information recorded in the reflogs.

Reference logs, or "reflogs", record when the tips of branches and other references were updated in the local repository. Reflogs are useful in various Git commands, to specify the old value of a reference.

For example, HEAD@{2} means "where HEAD used to be two moves ago", master@{one.week.ago} means "where master used to point to one week ago in this local repository", and so on.

The command takes various subcommands, and different options depending on the subcommand:

The "show" subcommand (which is also the default, in the absence of any subcommands) shows the log of the reference provided in the command-line (or HEAD, by default). The reflog covers all recent actions, and in addition the HEAD reflog records branch switching. git reflog show is an alias for git log -g --abbrev-commit --pretty=oneline.

## Options

[Options](https://git-scm.com/docs/git-reflog#_options)
