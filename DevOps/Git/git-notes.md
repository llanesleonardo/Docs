# Git notes

Add or inspect object notes.

Adds, removes, or reads notes attached to objects, without touching the objects themselves.

By default, notes are saved to and read from refs/notes/commits, but this default can be overridden. See the OPTIONS, CONFIGURATION, and ENVIRONMENT sections below. If this ref does not exist, it will be quietly created when it is first needed to store a note.

A typical use of notes is to supplement a commit message without changing the commit itself. Notes can be shown by git log along with the original commit message. To distinguish these notes from the message stored in the commit object, the notes are indented like the message, after an unindented line saying "Notes (<refname>):" (or "Notes:" for refs/notes/commits).

Notes can also be added to patches prepared with git format-patch by using the --notes option. Such notes are added as a patch commentary after a three dash separator line.

To change which notes are shown by git log, see the "notes.displayRef" discussion in CONFIGURATION.

See the "notes.rewrite.<command>" configuration for a way to carry notes across commands that rewrite commits.

```
root@DESKTOP-7UN911T:/var/www/html/devOpsDocs# git notes add -m '50% of the whole git documentation' dd333ea
root@DESKTOP-7UN911T:/var/www/html/devOpsDocs# git show -S dd333ea
root@DESKTOP-7UN911T:/var/www/html/devOpsDocs# git show -s dd333ea
commit dd333eadf9da887f23234a2520713682ff159203 (HEAD -> gitdocs, origin/main, main)
Author: Leonardo Llanes <llanesleonardo.developer@gmail.com>
Date:   Wed Jun 14 19:57:56 2023 -0700

    log,maintenance, grep,gc,fetch,format-patch,init

Notes:
    50% of the whole git documentation
```
