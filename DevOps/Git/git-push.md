# Git push

Updates remote refs using local refs, while sending objects necessary to complete the given refs.

You can make interesting things happen to a repository every time you push into it, by setting up hooks there.

When the command line does not specify where to push with the <repository> argument, branch.\*.remote configuration for the current branch is consulted to determine where to push. If the configuration is missing, it defaults to origin.

When the command line does not specify what to push with <refspec>... arguments or --all, --mirror, --tags options, the command finds the default <refspec> by consulting remote.\*.push configuration, and if it is not found, honors push.default configuration to decide what to push.

When neither the command-line nor the configuration specify what to push, the default behavior is used, which corresponds to the simple value for push.default: the current branch is pushed to the corresponding upstream branch, but as a safety measure, the push is aborted if the upstream branch does not have the same name as the local one.

## Options

```
<repository>
```

The "remote" repository that is destination of a push operation. This parameter can be either a URL or the name of a remote.

```
--all
--branches
```

Push all branches (i.e. refs under refs/heads/); cannot be used with other <refspec>.

```
--prune
```

Remove remote branches that don’t have a local counterpart. For example a remote branch tmp will be removed if a local branch with the same name doesn’t exist any more. This also respects refspecs, e.g. git push --prune remote refs/heads/_:refs/tmp/_ would make sure that remote refs/tmp/foo will be removed if refs/heads/foo doesn’t exist.

```
-n
--dry-run
```

Do everything except actually send the updates.

```
-d
--delete
```

All listed refs are deleted from the remote repository. This is the same as prefixing all refs with a colon.

```
--tags
```

All refs under refs/tags are pushed, in addition to refspecs explicitly listed on the command line.

```
--[no-]signed
--signed=(true|false|if-asked)
```

GPG-sign the push request to update refs on the receiving side, to allow it to be checked by the hooks and/or be logged. If false or --no-signed, no signing will be attempted. If true or --signed, the push will fail if the server does not support signed pushes. If set to if-asked, sign if and only if the server supports signed pushes. The push will also fail if the actual call to gpg --sign fails.

```
--[no-]atomic
```

Use an atomic transaction on the remote side if available. Either all refs are updated, or on error, no refs are updated. If the server does not support atomic pushes the push will fail.

```
-o <option>
--push-option=<option>
```

Transmit the given string to the server, which passes them to the pre-receive as well as the post-receive hook. The given string must not contain a NUL or LF character. When multiple --push-option=<option> are given, they are all sent to the other side in the order listed on the command line. When no --push-option=<option> is given from the command line, the values of configuration variable push.pushOption are used instead.

```
-u
--set-upstream
```

For every branch that is up to date or successfully pushed, add upstream (tracking) reference, used by argument-less git-pull[1] and other commands.

## Output

The output of "git push" depends on the transport method used; this section describes the output when pushing over the Git protocol (either locally or via ssh).

The status of the push is output in tabular form, with each line representing the status of a single ref. Each line is of the form:

```
 <flag> <summary> <from> -> <to> (<reason>)

```

If --porcelain is used, then each line of the output is of the form:

```
 <flag> \t <from>:<to> \t <summary> (<reason>)

```

The status of up-to-date refs is shown only if --porcelain or --verbose option is used.

flag
A single character indicating the status of the ref:

(space)
for a successfully pushed fast-forward;

'+'
for a successful forced update;

'-'
for a successfully deleted ref;

'\*'
for a successfully pushed new ref;

'!'
for a ref that was rejected or failed to push; and

'='
for a ref that was up to date and did not need pushing.

summary
For a successfully pushed ref, the summary shows the old and new values of the ref in a form suitable for using as an argument to git log (this is <old>..<new> in most cases, and <old>...<new> for forced non-fast-forward updates).

For a failed update, more details are given:

- rejected
  Git did not try to send the ref at all, typically because it is not a fast-forward and you did not force the update.

- remote rejected
  The remote end refused the update. Usually caused by a hook on the remote side, or because the remote repository has one of the following safety options in effect: receive.denyCurrentBranch (for pushes to the checked out branch), receive.denyNonFastForwards (for forced non-fast-forward updates), receive.denyDeletes or receive.denyDeleteCurrent. See git-config[1].

- remote failure
  The remote end did not report the successful update of the ref, perhaps because of a temporary error on the remote side, a break in the network connection, or other transient error.

from
The name of the local ref being pushed, minus its refs/<type>/ prefix. In the case of deletion, the name of the local ref is omitted.

to
The name of the remote ref being updated, minus its refs/<type>/ prefix.

reason
A human-readable explanation. In the case of successfully pushed refs, no explanation is needed. For a failed ref, the reason for failure is described.

## Notes about fast-forwards

When an update changes a branch (or more in general, a ref) that used to point at commit A to point at another commit B, it is called a fast-forward update if and only if B is a descendant of A.

In a fast-forward update from A to B, the set of commits that the original commit A built on top of is a subset of the commits the new commit B builds on top of. Hence, it does not lose any history.

In contrast, a non-fast-forward update will lose history. For example, suppose you and somebody else started at the same commit X, and you built a history leading to commit B while the other person built a history leading to commit A. The history looks like this:

```
      B
     /
 ---X---A
```

Further suppose that the other person already pushed changes leading to A back to the original repository from which you two obtained the original commit X.

The push done by the other person updated the branch that used to point at commit X to point at commit A. It is a fast-forward.

But if you try to push, you will attempt to update the branch (that now points at A) with commit B. This does not fast-forward. If you did so, the changes introduced by commit A will be lost, because everybody will now start building on top of B.

The command by default does not allow an update that is not a fast-forward to prevent such loss of history.

If you do not want to lose your work (history from X to B) or the work by the other person (history from X to A), you would need to first fetch the history from the repository, create a history that contains changes done by both parties, and push the result back.

You can perform "git pull", resolve potential conflicts, and "git push" the result. A "git pull" will create a merge commit C between commits A and B.

```
      B---C
     /   /
 ---X---A
```

Updating A with the resulting merge commit will fast-forward and your push will be accepted.

Alternatively, you can rebase your change between X and B on top of A, with "git pull --rebase", and push the result back. The rebase will create a new commit D that builds the change between X and B on top of A.

```
      B   D
     /   /
 ---X---A
```

Again, updating A with this commit will fast-forward and your push will be accepted.

There is another common situation where you may encounter non-fast-forward rejection when you try to push, and it is possible even when you are pushing into a repository nobody else pushes into. After you push commit A yourself (in the first picture in this section), replace it with "git commit --amend" to produce commit B, and you try to push it out, because forgot that you have pushed A out already. In such a case, and only if you are certain that nobody in the meantime fetched your earlier commit A (and started building on top of it), you can run "git push --force" to overwrite it. In other words, "git push --force" is a method reserved for a case where you do mean to lose history.
