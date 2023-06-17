# Git replace

Create, list, delete refs to replace objects.

Adds a replace reference in refs/replace/ namespace.

The name of the replace reference is the SHA-1 of the object that is replaced. The content of the replace reference is the SHA-1 of the replacement object.

The replaced object and the replacement object must be of the same type. This restriction can be bypassed using -f.

Unless -f is given, the replace reference must not yet exist.

There is no other restriction on the replaced and replacement objects. Merge commits can be replaced by non-merge commits and vice versa.

Replacement references will be used by default by all Git commands except those doing reachability traversal (prune, pack transfer and fsck).

It is possible to disable use of replacement references for any command using the --no-replace-objects option just after git.

For example if commit foo has been replaced by commit bar:

```
$ git --no-replace-objects cat-file commit foo
```

shows information about commit foo, while:

```
$ git cat-file commit foo
```

shows information about commit bar.

The GIT_NO_REPLACE_OBJECTS environment variable can be set to achieve the same effect as the --no-replace-objects option.

## Options

[Options](https://git-scm.com/docs/git-replace#_options)

## Creating replacement objects

git-hash-object[1], git-rebase[1], and git-filter-repo, among other git commands, can be used to create replacement objects from existing objects. The --edit option can also be used with git replace to create a replacement object by editing an existing object.

If you want to replace many blobs, trees or commits that are part of a string of commits, you may just want to create a replacement string of commits and then only replace the commit at the tip of the target string of commits with the commit at the tip of the replacement string of commits.

## Examples

Git replace is a mechanism that enables you to substitute a commit or tag object with a different one. This can be useful in scenarios where you want to rewrite the history of a repository or fix mistakes in previous commits without altering the existing commit IDs.

When you use the git replace command, you can specify the object you want to replace and the replacement object. The replacement object can be another commit, tag, or any other Git object.

Here's an example of how you can use git replace to replace a commit:

1. Identify the commit you want to replace and the replacement commit.
2. Find the commit ID of the replacement commit.
3. Run the following command:

```
$ git replace <commit-to-replace> <replacement-commit>
```

Replace <commit-to-replace> with the commit ID you want to replace, and <replacement-commit> with the commit ID of the replacement commit.

After running the command, Git will create a "replace reference" that associates the commit you want to replace with the replacement commit. From this point on, Git will use the replacement commit in all operations that involve the replaced commit, such as displaying history, creating diffs, or generating patches.

It's important to note that the replacement is local to your repository and does not affect the original repository or other clones. Other Git users need to explicitly fetch or receive the replacement references to see the changes.

You can remove the replace reference by running git replace -d <commit-to-replace>. This will revert to using the original commit.

Git replace is a powerful but advanced feature that should be used with caution. It's recommended to have a good understanding of Git's internals and the potential consequences before using it.
