# Git revert

Revert some existing commits.

Given one or more existing commits, revert the changes that the related patches introduce, and record some new commits that record them. This requires your working tree to be clean (no modifications from the HEAD commit).

Note: git revert is used to record some new commits to reverse the effect of some earlier commits (often only a faulty one). If you want to throw away all uncommitted changes in your working directory, you should see git-reset[1], particularly the --hard option. If you want to extract specific files as they were in another commit, you should see git-restore[1], specifically the --source option. Take care with these alternatives as both will discard uncommitted changes in your working directory.

## Options

[Options](https://git-scm.com/docs/git-revert#_options)

## Sequencer subcommands

[Sequencer subcommands](https://git-scm.com/docs/git-revert#_sequencer_subcommands)

## Examples

```
git revert HEAD~3
```

Revert the changes specified by the fourth last commit in HEAD and create a new commit with the reverted changes.

```
git revert -n master~5..master~2
```

Revert the changes done by commits from the fifth last commit in master (included) to the third last commit in master (included), but do not create any commit with the reverted changes. The revert only modifies the working tree and the index.
