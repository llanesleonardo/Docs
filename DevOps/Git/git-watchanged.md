# Git watchanged

Shows commit logs and diff output each commit introduces.

New users are encouraged to use git-log[1] instead. The whatchanged command is essentially the same as git-log[1] but defaults to show the raw format diff output and to skip merges.

The command is kept primarily for historical reasons; fingers of many people who learned Git long before git log was invented by reading Linux kernel mailing list are trained to type it.

## Examples

```
git whatchanged -p v2.6.12.. include/scsi drivers/scsi
```

Show as patches the commits since version v2.6.12 that changed any file in the include/scsi or drivers/scsi subdirectories

```
git whatchanged --since="2 weeks ago" -- gitk
```

Show the changes during the last two weeks to the file gitk. The "--" is necessary to avoid confusion with the branch named gitk
