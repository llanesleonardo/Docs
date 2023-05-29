# Tags

[Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

## Pushing tags

By default, and without additional parameters, git push sends all matching branches that have the same names as remote branches.

To push a single tag, you can issue the same command as pushing a branch:

    git push REMOTE-NAME TAG-NAME

To push all your tags, you can type the command:

    git push REMOTE-NAME --tags
