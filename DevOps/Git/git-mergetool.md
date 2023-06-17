# Git mergetool

Run merge conflict resolution tools to resolve merge conflicts.

Use git mergetool to run one of several merge utilities to resolve merge conflicts. It is typically run after git merge.

If one or more <file> parameters are given, the merge tool program will be run to resolve differences on each file (skipping those without conflicts). Specifying a directory will include all unresolved files in that path. If no <file> names are specified, git mergetool will run the merge tool program on every file with merge conflicts.

## Options

```
-t <tool>
--tool=<tool>
```

Use the merge resolution program specified by <tool>. Valid values include emerge, gvimdiff, kdiff3, meld, vimdiff, and tortoisemerge. Run git mergetool --tool-help for the list of valid <tool> settings.

If a merge resolution program is not specified, git mergetool will use the configuration variable merge.tool. If the configuration variable merge.tool is not set, git mergetool will pick a suitable default.

You can explicitly provide a full path to the tool by setting the configuration variable mergetool.<tool>.path. For example, you can configure the absolute path to kdiff3 by setting mergetool.kdiff3.path. Otherwise, git mergetool assumes the tool is available in PATH.

Instead of running one of the known merge tool programs, git mergetool can be customized to run an alternative program by specifying the command line to invoke in a configuration variable mergetool.<tool>.cmd.

When git mergetool is invoked with this tool (either through the -t or --tool option or the merge.tool configuration variable) the configured command line will be invoked with $BASE set to the name of a temporary file containing the common base for the merge, if available; $LOCAL set to the name of a temporary file containing the contents of the file on the current branch; $REMOTE set to the name of a temporary file containing the contents of the file to be merged, and $MERGED set to the name of the file to which the merge tool should write the result of the merge resolution.

If the custom merge tool correctly indicates the success of a merge resolution with its exit code, then the configuration variable mergetool.<tool>.trustExitCode can be set to true. Otherwise, git mergetool will prompt the user to indicate the success of the resolution after the custom tool has exited.

## Configuration

[Configuration](https://git-scm.com/docs/git-mergetool#_configuration)
