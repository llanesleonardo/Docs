# Git difftool

Show changes using common diff tools.

git difftool is a Git command that allows you to compare and edit files between revisions using common diff tools. git difftool is a frontend to git diff and accepts the same options and arguments.

## Options

[Options](https://git-scm.com/docs/git-difftool#_options)

## Configuration

git difftool falls back to git mergetool config variables when the difftool equivalents have not been defined.

The content that follows is the same as what’s found there:

```
diff.tool
```

Controls which diff tool is used by git-difftool[1]. This variable overrides the value configured in merge.tool. The list below shows the valid built-in values. Any other value is treated as a custom diff tool and requires that a corresponding difftool.<tool>.cmd variable is defined.

```
diff.guitool
```

Controls which diff tool is used by git-difftool[1] when the -g/--gui flag is specified. This variable overrides the value configured in merge.guitool. The list below shows the valid built-in values. Any other value is treated as a custom diff tool and requires that a corresponding difftool.<guitool>.cmd variable is defined.

```
difftool.<tool>.cmd
```

Specify the command to invoke the specified diff tool. The specified command is evaluated in shell with the following variables available: LOCAL is set to the name of the temporary file containing the contents of the diff pre-image and REMOTE is set to the name of the temporary file containing the contents of the diff post-image.

```
difftool.<tool>.path
```

Override the path for the given tool. This is useful in case your tool is not in the PATH.

```
difftool.trustExitCode
```

Exit difftool if the invoked diff tool returns a non-zero exit status.
