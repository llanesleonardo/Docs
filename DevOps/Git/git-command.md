Back: [Table contents](./1-tablecontent.md)

# Git command

- [Git tutorial to get started](https://git-scm.com/docs/gittutorial)
- [Git everyday](https://git-scm.com/docs/giteveryday)
- [Most common commands](https://www.youtube.com/watch?v=b4zp02iULYY)

## Description

Git is a fast, scalable, distributed revision control system with an unusually rich command set that provides both high-level operations and full access to internals.

## Options

```
-v
-- version
```

Prints the Git suite version that the git program came from.

---

```
-h
--help
```

Prints the synopsis and a list of the most commonly used commands. If the option --all or -a is given then all available commands are printed.

---

```
-C <path>
```

Run as if git was started in <path> instead of the current working directory. When multiple -C options are given, each subsequent non-absolute -C <path> is interpreted relative to the preceding -C <path>. If <path> is present but empty, e.g. -C "", then the current working directory is left unchanged.

This option affects options that expect path name like --git-dir and --work-tree in that their interpretations of the path names would be made relative to the working directory caused by the -C option. For example the following invocations are equivalent:

The -C <path> option in Git is used to specify a directory or path as the working directory for a specific Git command. It allows you to run a Git command as if you were in a different directory without actually changing your current working directory.

When you use the -C <path> option with a Git command, Git temporarily changes its internal reference to the specified directory, and then executes the command as if you were inside that directory. This can be useful when you want to run a Git command on a different repository or when you want to execute a Git command from a different location.

```
git -C /path/to/repository status

```

In the above command, the -C option specifies the path /path/to/repository as the working directory for the status command. Git will act as if you are inside that repository and display the status of the files within it.

This option is particularly helpful when you want to run Git commands on repositories located in different directories, without having to navigate to each repository's location individually. It provides a convenient way to operate on different repositories without changing your current working directory.

Here's another example to illustrate its usage:

```
git --git-dir=a.git --work-tree=b -C c status
git --git-dir=c/a.git --work-tree=c/b status
```

---

```
-c <name>=<value>
```

The -c <name>=<value> option in Git is used to set configuration variables for a specific Git command. It allows you to override or set temporary configurations just for that particular command without permanently modifying the global or local Git configurations.

With the -c option, you can specify a configuration variable by providing its name and value. Here's an example:

```
git -c user.name="John Doe" commit -m "Initial commit"

```

In the above command, the -c option sets the temporary value of the user.name configuration variable to "John Doe" only for the duration of the commit command. This allows you to specify a custom name for the author of the commit without permanently changing your global or local Git configurations.

You can use the -c option multiple times to set multiple configuration variables:

```
git -c user.name="John Doe" -c user.email="john.doe@example.com" commit -m "Fix typo"

```

In this example, both the user.name and user.email configuration variables are set temporarily for the commit command.

The -c option is particularly useful when you want to override specific configuration variables for a single command without affecting the rest of your Git environment. It allows you to customize certain aspects of a command without permanently modifying your Git settings.

---

```
--config-env=<name>=<envvar>
```

### More:

- [--config-env](https://git-scm.com/docs/git#Documentation/git.txt---config-envltnamegtltenvvargt)

---

```
--exec-path[=<path>]
```

Path to wherever your core Git programs are installed. This can also be controlled by setting the GIT_EXEC_PATH environment variable. If no path is given, git will print the current setting and then exit.

```
/usr/lib/git-core
```

---

```
--html-path
# /usr/share/doc/git/html
```

Print the path, without trailing slash, where Git’s HTML documentation is installed and exit.

---

```
--man-path
# /usr/share/man
```

Print the manpath (see man(1)) for the man pages for this version of Git and exit.

---

```
--info-path
# /usr/share/info
```

Print the path where the Info files documenting this version of Git are installed and exit.

---

```
-p
--paginate
```

### More:

- [-p](https://git-scm.com/docs/git#Documentation/git.txt---paginate)

---

```
-P
--no-pager
```

Do not pipe Git output into a pager.

---

```
--git-dir=<path>
git --git-dir=/path/to/repository/.git log

```

The --git-dir=<path> option in Git is used to specify the path to the Git directory for a particular operation. By default, Git assumes the current working directory is the Git directory (.git) or a parent directory of it. However, the --git-dir option allows you to explicitly specify a different directory as the Git directory.

Using --git-dir is particularly useful when you want to run Git commands on a repository that is not in the current working directory. It allows you to explicitly point Git to the desired repository location.

It's worth noting that when you specify --git-dir, Git will not change your current working directory. If the command you execute requires a working directory (such as git status), it will still use the current working directory as the working directory for that command.

Remember that specifying the --git-dir option should be done with caution, as it bypasses the normal behavior of Git and assumes a different Git directory location for the operation.

---

```
--work-tree=<path>

git --work-tree=/path/to/repository/ status

```

Set the path to the working tree. It can be an absolute path or a path relative to the current working directory. This can also be controlled by setting the GIT_WORK_TREE environment variable and the core.worktree configuration variable

The working tree refers to the directory where you have checked out or cloned a Git repository.

By default, Git assumes that the current working directory is the working tree. However, the --work-tree option allows you to explicitly specify a different directory as the working tree.

Similar to the --git-dir option, specifying --work-tree does not change your current working directory. If the command you execute requires a working directory (such as git add), it will still use the current working directory as the working directory for that command.

---

```
--namespace=<path>

git branch projectA/new-feature


```

Set the Git namespace. Equivalent to setting the GIT_NAMESPACE environment variable.

In Git, a namespace refers to a way of organizing and categorizing Git references, such as branches, tags, and remote references. It allows you to group related references under a specific namespace, making it easier to manage and differentiate between different sets of references.

Namespaces are primarily used in large-scale Git repositories where multiple teams or projects coexist within the same repository. By using namespaces, you can isolate and organize the references associated with each project or team, reducing the potential for conflicts and providing better clarity in the repository's structure.

Namespaces in Git are created by prefixing references with a namespace string followed by a slash (/). For example, if you have a namespace called "projectA", you would prefix branches, tags, and remote references associated with that project with "projectA/". The actual reference names would look like "projectA/branch-name" or "projectA/tag-name".

Namespaces help provide a logical separation and structure to your Git repository, making it easier to manage large codebases, multiple projects, or collaborative environments.

### More

[Git namespace](https://git-scm.com/docs/gitnamespaces)

---

```
--bare
```

Treat the repository as a bare repository. If GIT_DIR environment is not set, it is set to the current working directory.

A bare repository is a repository that does not have a working tree. It contains only the version history, branches, tags, and other Git-related metadata, without the actual files of the project. In other words, a bare repository does not have a checked-out or editable version of the project's files like a typical working directory does.

The primary purpose of a bare repository is to serve as a central shared repository in a collaborative Git workflow. It is commonly used when setting up a remote repository that multiple developers can push their changes to or pull changes from.

When you don't have a working tree:

- You cannot directly view or modify the files: Without a working tree, you don't have a local copy of the project's files. You cannot directly view or edit the contents of the files within the repository.
- You cannot perform typical file operations: Since the files are not present in the repository, you cannot perform common file operations such as editing, adding, deleting, or organizing files through Git commands.
- You can still perform version control operations: Although you don't have a working tree, you can still perform version control operations in a bare repository. You can create branches, tags, and commits, push and pull changes, merge branches, view the commit history, and perform other Git-related actions.
- It is suitable for collaboration and server-side use: Bare repositories are commonly used in scenarios where multiple developers need to collaborate on a project or where the repository is set up as a server-side deployment. In these cases, developers interact with the repository through Git commands without directly modifying the files within the repository.

### More:

[Git Repo Bare](https://www.youtube.com/watch?v=8aZW9mYOxhc)

---
