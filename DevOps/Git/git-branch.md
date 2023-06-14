# Git branch

List, create, or delete branches.

```
git branch

```

If --list is given, or if there are no non-option arguments, existing branches are listed; the current branch will be highlighted in green and marked with an asterisk. Any branches checked out in linked worktrees will be highlighted in cyan and marked with a plus sign. Option -r causes the remote-tracking branches to be listed, and option -a shows both local and remote branches.

Note that this will create the new branch, but it will not switch the working tree to it; use "git switch <newbranch>" to switch to the new branch.

## Options

```
-
--delete

```

Delete a branch. The branch must be fully merged in its upstream branch, or in HEAD if no upstream was set with --track or --set-upstream-to.

---

```
--create-reflog

```

Create the branch’s reflog. This activates recording of all changes made to the branch ref, enabling use of date based sha1 expressions such as "<branchname>@{yesterday}".

The reflog, short for "reference log," is a mechanism in Git that keeps track of changes to references in your repository, such as branches and HEAD. It maintains a local history of each reference's previous positions, recording when they were updated and what the old and new commit pointers were.

By default, the reflog retains this information for a certain period (usually 90 days) or until a Git garbage collection operation occurs. The reflog is particularly useful when you need to recover lost commits or restore branches that were accidentally deleted or modified.

When you run git branch --reflog, Git displays a list of branches in your repository and provides the reflog entries associated with each branch. This can help you understand the history of each branch, including when and how it was updated or moved.

Here's an example of the output you might see:

NOT WORKING

```
$ git branch --reflog
  branch1  50bc589 [branch1@{0}: commit: Added feature A]
  branch2  20a3f1d [branch2@{0}: commit: Fixed bug X]
  master   5b86298 [master@{0}: commit: Updated documentation]

```

YOU MAY WANT TO USE: git show-branch -g

---

```
-f
--force

```

Reset <branchname> to <start-point>, even if <branchname> exists already. Without -f, git branch refuses to change an existing branch. In combination with -d (or --delete), allow deleting the branch irrespective of its merged status, or whether it even points to a valid commit.

---

```
-m
--move

```

Move/rename a branch, together with its config and reflog.

---

```
-c
--copy

```

Copy a branch, together with its config and reflog.

---

```
-i
--ignore-case
```

Sorting and filtering branches are case insensitive.

---

```
--column[=<options>]
--no-column

```

Display branch listing in columns. See configuration variable column.branch for option syntax. --column and --no-column without options are equivalent to always and never respectively.

---

```
-r
--remotes

```

List or delete (if used with -d) the remote-tracking branches.

---

```
--show-current

```

Print the name of the current branch. In detached HEAD state, nothing is printed.

---

```
-v
-vv
--verbose

* gitdocs    eabd088 add, am, archive, hunk, options, embedded repository files
  main       149e384 1st github actions section review

```

When in list mode, show sha1 and commit subject line for each head, along with relationship to upstream branch (if any). If given twice, print the path of the linked worktree (if any) and the name of the upstream branch, as well (see also git remote show <remote>). Note that the current worktree’s HEAD will not have its path printed (it will always be your current directory).

---

```
-t
--track[=(direct|inherit)]

```

When creating a new branch, set up branch.<name>.remote and branch.<name>.merge configuration entries to set "upstream" tracking configuration for the new branch. This configuration will tell git to show the relationship between the two branches in git status and git branch -v. Furthermore, it directs git pull without arguments to pull from the upstream when the new branch is checked out.

---

```
-u <upstream>
--set-upstream-to=<upstream>

```

Set up <branchname>'s tracking information so <upstream> is considered <branchname>'s upstream branch. If no <branchname> is specified, then it defaults to the current branch.

---

```
--unset-upstream
```

Remove the upstream information for <branchname>. If no branch is specified it defaults to the current branch.

---

```
--edit-description
```

Open an editor and edit the text to explain what the branch is for, to be used by various other commands (e.g. format-patch, request-pull, and merge (if enabled)). Multi-line explanations may be used.

---

```
--contains [<commit>]
```

Only list branches which contain the specified commit (HEAD if not specified). Implies --list.

---

```
--no-contains [<commit>]
```

Only list branches which don’t contain the specified commit (HEAD if not specified). Implies --list.

---

```
--merged [<commit>]
```

Only list branches whose tips are reachable from the specified commit (HEAD if not specified). Implies --list.

---

```
--no-merged [<commit>]
```

Only list branches whose tips are not reachable from the specified commit (HEAD if not specified). Implies --list.

---

```
<branchname>

```

The name of the branch to create or delete. The new branch name must pass all checks defined by git-check-ref-format[1]. Some of these checks may restrict the characters allowed in a branch name.

---

```
<start-point>

```

The new branch head will point to this commit. It may be given as a branch name, a commit-id, or a tag. If this option is omitted, the current HEAD will be used instead.

---

## Examples

Start development from a known tag

```
$ git clone git://git.kernel.org/pub/scm/.../linux-2.6 my2.6
$ cd my2.6
$ git branch my2.6.14 v2.6.14   (1)
$ git switch my2.6.14
```

---

Delete an unneeded branch

```
$ git clone git://git.kernel.org/.../git.git my.git
$ cd my.git
$ git branch -d -r origin/todo origin/html origin/man   (1)
$ git branch -D test                                    (2)
```

- Delete the remote-tracking branches "todo", "html" and "man". The next fetch or pull will create them again unless you configure them not to. See git-fetch[1].
- Delete the "test" branch even if the "master" branch (or whichever branch is currently checked out) does not have all commits from the test branch.

---

Listing branches from a specific remote

```
$ git branch -r -l '<remote>/<pattern>'                 (1)
$ git for-each-ref 'refs/remotes/<remote>/<pattern>'    (2)
```

---
