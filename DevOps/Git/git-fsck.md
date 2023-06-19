# Git fsck

Verifies the connectivity and validity of the objects in the database.

In Git, a dangling blob or dangling commit refers to an object that exists in the Git database but is not referenced by any branch, tag, or other Git object. These objects are essentially unreachable and have no direct association with any part of the repository's history.

A dangling blob specifically refers to an unreferenced or orphaned Git blob object. A blob object in Git represents the content of a file at a specific point in time. When a file is modified, Git creates a new blob object to store the updated content.

Dangling blobs typically occur in Git repositories due to operations like:

- Deleting or modifying files without committing the changes.
- Forcefully removing branches or tags.
- Interrupted operations or failures that leave Git objects unreferenced.

These dangling blobs occupy space in the Git repository and can be safely removed if they are no longer needed. Git provides a built-in mechanism called "garbage collection" to clean up these unreferenced objects and optimize repository storage. However, Git's automatic garbage collection is designed to run periodically and may not immediately remove all dangling objects.

If you want to manually identify and remove dangling blobs in Git, you can use the git fsck command with the --unreachable or --dangling option. For example:

```
git fsck --unreachable
git fsck --dangling
```

Running these commands will display a list of unreferenced or dangling objects, including dangling blobs, in your repository. To remove them, you can use the git prune command:

```
git prune
```

Note that the git prune command is a low-level Git command and should be used with caution. It permanently removes unreferenced objects, including dangling blobs, from the repository. Make sure you have a backup of your repository before performing any manual cleanup operations.

## Options

```
<object>
```

An object to treat as the head of an unreachability trace.

If no objects are given, git fsck defaults to using the index file, all SHA-1 references in refs namespace, and all reflogs (unless --no-reflogs is given) as heads.

```
--unreachable
```

Print out objects that exist but that aren’t reachable from any of the reference nodes.

```
--[no-]dangling
```

Print objects that exist but that are never directly used (default). --no-dangling can be used to omit this information from the output.

```
--root
```

Report root nodes.

```
--tags
```

Report tags.

```
--cache
```

Consider any object recorded in the index also as a head node for an unreachability trace.

```
--no-reflogs
```

Do not consider commits that are referenced only by an entry in a reflog to be reachable. This option is meant only to search for commits that used to be in a ref, but now aren’t, but are still in that corresponding reflog.

## Discussion

git-fsck tests SHA-1 and general object sanity, and it does full tracking of the resulting reachability and everything else. It prints out any corruption it finds (missing or bad objects), and if you use the --unreachable flag it will also print out objects that exist but that aren’t reachable from any of the specified head nodes (or the default set, as mentioned above).

Any corrupt objects you will have to find in backups or other archives (i.e., you can just remove them and do an rsync with some other site in the hopes that somebody else has the object you have corrupted).

If core.commitGraph is true, the commit-graph file will also be inspected using git commit-graph verify.

## Fsck messages

[fsck messages](https://git-scm.com/docs/git-fsck#_fsck_messages)
