# Git submodule

Initialize, update or inspect submodules.

Inspects, updates and manages submodules.

## Commands

[Commands](https://git-scm.com/docs/git-submodule#_commands)

## Options

```
-b <branch>
--branch <branch>
```

Branch of repository to add as submodule. The name of the branch is recorded as submodule.<name>.branch in .gitmodules for update --remote. A special value of . is used to indicate that the name of the branch in the submodule should be the same name as the current branch in the current repository. If the option is not specified, it defaults to the remote HEAD.

```
--cached
```

This option is only valid for status and summary commands. These commands typically use the commit found in the submodule HEAD, but with this option, the commit stored in the index is used instead.

```
--files
```

This option is only valid for the summary command. This command compares the commit in the index with that in the submodule HEAD when this option is used.

```
--remote
```

This option is only valid for the update command. Instead of using the superproject’s recorded SHA-1 to update the submodule, use the status of the submodule’s remote-tracking branch. The remote used is branch’s remote (branch.<name>.remote), defaulting to origin. The remote branch used defaults to the remote HEAD, but the branch name may be overridden by setting the submodule.<name>.branch option in either .gitmodules or .git/config (with .git/config taking precedence).

This works for any of the supported update procedures (--checkout, --rebase, etc.). The only change is the source of the target SHA-1. For example, submodule update --remote --merge will merge upstream submodule changes into the submodules, while submodule update --merge will merge superproject gitlink changes into the submodules.

In order to ensure a current tracking branch state, update --remote fetches the submodule’s remote repository before calculating the SHA-1. If you don’t want to fetch, you should use submodule update --remote --no-fetch.

Use this option to integrate changes from the upstream subproject with your submodule’s current HEAD. Alternatively, you can run git pull from the submodule, which is equivalent except for the remote branch name: update --remote uses the default upstream repository and submodule.<name>.branch, while git pull uses the submodule’s branch.<name>.merge. Prefer submodule.<name>.branch if you want to distribute the default upstream branch with the superproject and branch.<name>.merge if you want a more native feel while working in the submodule itself.

```
-N
--no-fetch
```

This option is only valid for the update command. Don’t fetch new objects from the remote site.

```
--checkout
```

This option is only valid for the update command. Checkout the commit recorded in the superproject on a detached HEAD in the submodule. This is the default behavior, the main use of this option is to override submodule.$name.update when set to a value other than checkout. If the key submodule.$name.update is either not explicitly set or set to checkout, this option is implicit.

```
--merge
```

This option is only valid for the update command. Merge the commit recorded in the superproject into the current branch of the submodule. If this option is given, the submodule’s HEAD will not be detached. If a merge failure prevents this process, you will have to resolve the resulting conflicts within the submodule with the usual conflict resolution tools. If the key submodule.$name.update is set to merge, this option is implicit.

```
--rebase
```

This option is only valid for the update command. Rebase the current branch onto the commit recorded in the superproject. If this option is given, the submodule’s HEAD will not be detached. If a merge failure prevents this process, you will have to resolve these failures with git-rebase[1]. If the key submodule.$name.update is set to rebase, this option is implicit.

```
--init
```

This option is only valid for the update command. Initialize all submodules for which "git submodule init" has not been called so far before updating.

```
--name
```

This option is only valid for the add command. It sets the submodule’s name to the given string instead of defaulting to its path. The name must be valid as a directory name and may not end with a /.

```
--reference <repository>
```

This option is only valid for add and update commands. These commands sometimes need to clone a remote repository. In this case, this option will be passed to the git-clone[1] command.

```
--dissociate
```

This option is only valid for add and update commands. These commands sometimes need to clone a remote repository. In this case, this option will be passed to the git-clone[1] command.

NOTE: see the NOTE for the --reference option.

```
--recursive
```

This option is only valid for foreach, update, status and sync commands. Traverse submodules recursively. The operation is performed not only in the submodules of the current repo, but also in any nested submodules inside those submodules (and so on).

```
--depth
```

This option is valid for add and update commands. Create a shallow clone with a history truncated to the specified number of revisions. See git-clone[1]

```
--[no-]recommend-shallow
```

This option is only valid for the update command. The initial clone of a submodule will use the recommended submodule.<name>.shallow as provided by the .gitmodules file by default. To ignore the suggestions use --no-recommend-shallow.

```
<path>…​
```

Paths to submodule(s). When specified this will restrict the command to only operate on the submodules found at the specified paths. (This argument is required with add).
