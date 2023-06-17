# Git Shortlog

Summarize git log output.

Summarizes git log output in a format suitable for inclusion in release announcements. Each commit will be grouped by author and title.

Additionally, "[PATCH]" will be stripped from the commit description.

If no revisions are passed on the command line and either standard input is not a terminal or there is no current branch, git shortlog will output a summary of the log read from standard input, without reference to the current repository.

## History simplification

[History simplification](https://git-scm.com/docs/git-shortlog#_history_simplification)
