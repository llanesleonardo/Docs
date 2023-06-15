# Git fetch

Download objects and refs from another repository.

Fetch branches and/or tags (collectively, "refs") from one or more other repositories, along with the objects necessary to complete their histories. Remote-tracking branches are updated (see the description of <refspec> below for ways to control this behavior).

By default, any tag that points into the histories being fetched is also fetched; the effect is to fetch tags that point at branches that you are interested in. This default behavior can be changed by using the --tags or --no-tags options or by configuring remote.<name>.tagOpt. By using a refspec that fetches tags explicitly, you can fetch tags that do not point into branches you are interested in as well.

git fetch can fetch from either a single named repository or URL, or from several repositories at once if <group> is given and there is a remotes.<group> entry in the configuration file.

When no remote is specified, by default the origin remote will be used, unless there’s an upstream branch configured for the current branch.

## Options

```
--all
```

Fetch all remotes.

```
-a
--append
```

Append ref names and object names of fetched refs to the existing contents of .git/FETCH_HEAD. Without this option old data in .git/FETCH_HEAD will be overwritten.

```
--atomic
```

Use an atomic transaction to update local refs. Either all refs are updated, or on error, no refs are updated.

```
--dry-run
```

Show what would be done, without making any changes.

```
--[no-]write-fetch-head
```

Write the list of remote refs fetched in the FETCH_HEAD file directly under $GIT_DIR. This is the default. Passing --no-write-fetch-head from the command line tells Git not to write the file. Under --dry-run option, the file is never written.

```
-k
--keep
```

Keep downloaded pack.

```
--[no-]auto-maintenance
--[no-]auto-gc
```

Run git maintenance run --auto at the end to perform automatic repository maintenance if needed. (--[no-]auto-gc is a synonym.) This is enabled by default.

```
-p
--prune
```

Before fetching, remove any remote-tracking references that no longer exist on the remote. Tags are not subject to pruning if they are fetched only because of the default tag auto-following or due to a --tags option. However, if tags are fetched due to an explicit refspec (either on the command line or in the remote configuration, for example if the remote was cloned with the --mirror option), then they are also subject to pruning. Supplying --prune-tags is a shorthand for providing the tag refspec.

```
-P
--prune-tags
```

Before fetching, remove any local tags that no longer exist on the remote if --prune is enabled. This option should be used more carefully, unlike --prune it will remove any local references (local tags) that have been created. This option is a shorthand for providing the explicit tag refspec along with --prune, see the discussion about that in its documentation.

```
--refetch
```

Instead of negotiating with the server to avoid transferring commits and associated objects that are already present locally, this option fetches all objects as a fresh clone would. Use this to reapply a partial clone filter from configuration or using --filter= when the filter definition has changed. Automatic post-fetch maintenance will perform object database pack consolidation to remove any duplicate objects.

```
-t
--tags
```

Fetch all tags from the remote (i.e., fetch remote tags refs/tags/\* into local tags with the same name), in addition to whatever else would otherwise be fetched. Using this option alone does not subject tags to pruning, even if --prune is used (though tags may be pruned anyway if they are also the destination of an explicit refspec; see --prune).

```
--set-upstream
```

If the remote is fetched successfully, add upstream (tracking) reference, used by argument-less git-pull[1] and other commands. For more information, see branch.<name>.merge and branch.

```
-4
--ipv4
```

Use IPv4 addresses only, ignoring IPv6 addresses.

```
-6
--ipv6
```

Use IPv6 addresses only, ignoring IPv4 addresses.

```
<repository>
```

The "remote" repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section GIT URLS below) or the name of a remote (see the section REMOTES below).

```
<group>
```

A name referring to a list of repositories as the value of remotes.<group> in the configuration file.

## Examples

Update the remote-tracking branches:

```
$ git fetch origin
```

The above command copies all branches from the remote refs/heads/ namespace and stores them to the local refs/remotes/origin/ namespace, unless the remote.<repository>.fetch option is used to specify a non-default refspec.

Using refspecs explicitly:

```
$ git fetch origin +seen:seen maint:tmp
```

This updates (or creates, as necessary) branches seen and tmp in the local repository by fetching from the branches (respectively) seen and maint from the remote repository.

The seen branch will be updated even if it does not fast-forward, because it is prefixed with a plus sign; tmp will not be.

Peek at a remote’s branch, without configuring the remote in your local repository:

```
$ git fetch git://git.kernel.org/pub/scm/git/git.git maint
$ git log FETCH_HEAD

```

The first command fetches the maint branch from the repository at git://git.kernel.org/pub/scm/git/git.git and the second command uses FETCH_HEAD to examine the branch with git-log[1]. The fetched objects will eventually be removed by git’s built-in housekeeping (see git-gc[1]).

## Security

The fetch and push protocols are not designed to prevent one side from stealing data from the other repository that was not intended to be shared. If you have private data that you need to protect from a malicious peer, your best option is to store it in another repository.

This applies to both clients and servers. In particular, namespaces on a server are not effective for read access control; you should only grant read access to a namespace to clients that you would trust with read access to the entire repository.

The known attack vectors are as follows:

- The victim sends "have" lines advertising the IDs of objects it has that are not explicitly intended to be shared but can be used to optimize the transfer if the peer also has them. The attacker chooses an object ID X to steal and sends a ref to X, but isn’t required to send the content of X because the victim already has it. Now the victim believes that the attacker has X, and it sends the content of X back to the attacker later. (This attack is most straightforward for a client to perform on a server, by creating a ref to X in the namespace the client has access to and then fetching it. The most likely way for a server to perform it on a client is to "merge" X into a public branch and hope that the user does additional work on this branch and pushes it back to the server without noticing the merge.)
- As in #1, the attacker chooses an object ID X to steal. The victim sends an object Y that the attacker already has, and the attacker falsely claims to have X and not Y, so the victim sends Y as a delta against X. The delta reveals regions of X that are similar to Y to the attacker.
