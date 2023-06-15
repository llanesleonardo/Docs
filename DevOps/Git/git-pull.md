# Git pull

Fetch from and integrate with another repository or a local branch.

Incorporates changes from a remote repository into the current branch. If the current branch is behind the remote, then by default it will fast-forward the current branch to match the remote. If the current branch and the remote have diverged, the user needs to specify how to reconcile the divergent branches with --rebase or --no-rebase (or the corresponding configuration option in pull.rebase).

More precisely, git pull runs git fetch with the given parameters and then depending on configuration options or command line flags, will call either git rebase or git merge to reconcile diverging branches.

<repository> should be the name of a remote repository as passed to git-fetch[1]. <refspec> can name an arbitrary remote ref (for example, the name of a tag) or even a collection of refs with corresponding remote-tracking branches (e.g., refs/heads/_:refs/remotes/origin/_), but usually it is the name of a branch in the remote repository.

Default values for <repository> and <branch> are read from the "remote" and "merge" configuration for the current branch as set by git-branch[1] --track.

Assume the following history exists and the current branch is "master":

```
      A---B---C master on origin
     /
    D---E---F---G master
    ^
    origin/master in your repository
```

Then "git pull" will fetch and replay the changes from the remote master branch since it diverged from the local master (i.e., E) until its current commit (C) on top of master and record the result in a new commit along with the names of the two parent commits and a log message from the user describing the changes.

```
      A---B---C origin/master
     /         \
    D---E---F---G---H master
```

See git-merge[1] for details, including how conflicts are presented and handled.

In Git 1.7.0 or later, to cancel a conflicting merge, use git reset --merge. Warning: In older versions of Git, running git pull with uncommitted changes is discouraged: while possible, it leaves you in a state that may be hard to back out of in the case of a conflict.

If any of the remote changes overlap with local uncommitted changes, the merge will be automatically canceled and the work tree untouched. It is generally best to get any local changes in working order before pulling or stash them away with git-stash[1].

## Default behaviour

Often people use git pull without giving any parameter. Traditionally, this has been equivalent to saying git pull origin. However, when configuration branch.<name>.remote is present while on branch <name>, that value is used instead of origin.

In order to determine what URL to use to fetch from, the value of the configuration remote.<origin>.url is consulted and if there is not any such variable, the value on the URL: line in $GIT_DIR/remotes/<origin> is used.

In order to determine what remote branches to fetch (and optionally store in the remote-tracking branches) when the command is run without any refspec parameters on the command line, values of the configuration variable remote.<origin>.fetch are consulted, and if there aren’t any, $GIT_DIR/remotes/<origin> is consulted and its Pull: lines are used. In addition to the refspec formats described in the OPTIONS section, you can have a globbing refspec that looks like this:

```
refs/heads/*:refs/remotes/origin/*
```

A globbing refspec must have a non-empty RHS (i.e. must store what were fetched in remote-tracking branches), and its LHS and RHS must end with /\*. The above specifies that all remote branches are tracked using remote-tracking branches in refs/remotes/origin/ hierarchy under the same name.

The rule to determine which remote branch to merge after fetching is a bit involved, in order not to break backward compatibility.

If explicit refspecs were given on the command line of git pull, they are all merged.

When no refspec was given on the command line, then git pull uses the refspec from the configuration or $GIT_DIR/remotes/<origin>. In such cases, the following rules apply:

1. If branch.<name>.merge configuration for the current branch <name> exists, that is the name of the branch at the remote site that is merged.
2. If the refspec is a globbing one, nothing is merged.
3. Otherwise the remote branch of the first refspec is merged.

## Examples

Update the remote-tracking branches for the repository you cloned from, then merge one of them into your current branch:

```
$ git pull
$ git pull origin
```

Normally the branch merged in is the HEAD of the remote repository, but the choice is determined by the branch.<name>.remote and branch.<name>.merge options; see git-config[1] for details.

Merge into the current branch the remote branch next:

```
$ git pull origin next
```

This leaves a copy of next temporarily in FETCH_HEAD, and updates the remote-tracking branch origin/next. The same can be done by invoking fetch and merge:

```
$ git fetch origin
$ git merge origin/next
```

If you tried a pull which resulted in complex conflicts and would want to start over, you can recover with git reset.
