# Git scalar

A tool for managing large Git repositories.

Scalar is a repository management tool that optimizes Git for use in large repositories. Scalar improves performance by configuring advanced Git settings, maintaining repositories in the background, and helping to reduce data sent across the network.

An important Scalar concept is the enlistment: this is the top-level directory of the project. It usually contains the subdirectory src/ which is a Git worktree. This encourages the separation between tracked files (inside src/) and untracked files, such as build artifacts (outside src/). When registering an existing Git worktree with Scalar whose name is not src, the enlistment will be identical to the worktree.

The scalar command implements various subcommands, and different options depending on the subcommand. With the exception of clone, list and reconfigure --all, all subcommands expect to be run in an enlistment.

The following options can be specified before the subcommand:

```
-C <directory>
```

Before running the subcommand, change the working directory. This option imitates the same option of git[1].

```
-c <key>=<value>
```

For the duration of running the specified subcommand, configure this setting. This option imitates the same option of git[1].

## Examples

[Example](https://www.youtube.com/watch?v=8iZqagosc5w)
