# Git gitk

The Git repository browser.

Displays changes in a repository or a selected set of commits. This includes visualizing the commit graph, showing information related to each commit, and the files in the trees of each revision.

## Examples

```
gitk v2.6.12.. include/scsi drivers/scsi
```

Show the changes since version v2.6.12 that changed any file in the include/scsi or drivers/scsi subdirectories

```
gitk --since="2 weeks ago" -- gitk
```

Show the changes during the last two weeks to the file gitk. The "--" is necessary to avoid confusion with the branch named gitk

```
gitk --max-count=100 --all -- Makefile
```

Show at most 100 changes made to the file Makefile. Instead of only looking for changes in the current branch look in all branches.
