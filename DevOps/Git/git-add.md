# Git add

Add file contents to the index.

This command updates the index using the current content found in the working tree, to prepare the content staged for the next commit. It typically adds the current content of existing paths as a whole, but with some options it can also be used to add content with only part of the changes made to the working tree files applied, or remove paths that do not exist in the working tree anymore.

The "index" holds a snapshot of the content of the working tree, and it is this snapshot that is taken as the contents of the next commit. Thus after making any changes to the working tree, and before running the commit command, you must use the add command to add any new or modified files to the index.

This command can be performed multiple times before a commit. It only adds the content of the specified file(s) at the time the add command is run; if you want subsequent changes included in the next commit, then you must run git add again to add the new content to the index.

The git status command can be used to obtain a summary of which files have changes that are staged for the next commit.

The git add command will not add ignored files by default. If any ignored files were explicitly specified on the command line, git add will fail with a list of ignored files. Ignored files reached by directory recursion or filename globbing performed by Git (quote your globs before the shell) will be silently ignored. The git add command can be used to add ignored files with the -f (force) option.

Please see git-commit[1] for alternative ways to add content to a commit.

## Options

<pathspec>

Files to add content from. Fileglobs (e.g. \*.c) can be given to add all matching files. Also a leading directory name (e.g. dir to add dir/file1 and dir/file2) can be given to update the index to match the current state of the directory as a whole (e.g. specifying dir will record not just a file dir/file1 modified in the working tree, a file dir/file2 added to the working tree, but also a file dir/file3 removed from the working tree). Note that older versions of Git used to ignore removed files; use --no-all option if you want to add modified or new files but ignore removed ones.

---

```
-n
--dry-run
```

Don’t actually add the file(s), just show if they exist and/or will be ignored.

---

```
-v
--verbose
```

Be verbose.

The --verbose option in Git is used to provide more detailed and verbose output when executing Git commands. By including the --verbose option, Git will display additional information during the command's execution, such as the progress of the operation, the files being processed, and any relevant status messages.

The usage of --verbose varies depending on the Git command. Here is an example:

- git add --verbose <file>: Shows additional information about the files being added to the staging area, such as the path and status of each file.

---

```
-f
--force
```

Allow adding otherwise ignored files.

---

```
--sparse

```

Allow updating index entries outside of the sparse-checkout cone. Normally, git add refuses to update index entries whose paths do not fit within the sparse-checkout cone, since those files might be removed from the working tree without warning.

TODO: FIND MORE INFO.

---

```
-i
--interactive
```

Add modified contents in the working tree interactively to the index. Optional path arguments may be supplied to limit operation to a subset of the working tree.

git add --interactive:
This command opens an interactive session where you can choose which changes to stage (add to the index). It presents you with a list of modified files and allows you to selectively stage them or apply different actions, such as splitting changes into smaller patches.

The --interactive option provides a powerful way to interact with Git, giving you fine-grained control over the operations. It allows you to review changes, make selective modifications, and tailor the behavior of Git commands to suit your specific needs.

Keep in mind that using --interactive can require some familiarity with Git concepts and workflows. It opens an interactive session where you make changes or selections, and then Git carries out the requested actions based on your input.

More: [interactive](https://git-scm.com/docs/git-add#_interactive_mode)

---

```
-p
--patch
```

Interactively choose hunks of patch between the index and the work tree and add them to the index. This gives the user a chance to review the difference before adding modified contents to the index.

---

```
-e
--edit
```

Open the diff vs. the index in an editor and let the user edit it. After the editor was closed, adjust the hunk headers and apply the patch to the index.

The intent of this option is to pick and choose lines of the patch to apply, or even to modify the contents of lines to be staged. This can be quicker and more flexible than using the interactive hunk selector.

TODO: FIND MORE INFO.

---

```
-u
--update
```

Update the index just where it already has an entry matching <pathspec>. This removes as well as modifies index entries to match the working tree, but adds no new files.

---

```
-A
--all
--no-ignore-removal
```

Update the index not only where the working tree has a file matching <pathspec> but also where the index already has an entry. This adds, modifies, and removes index entries to match the working tree.

The git add --all command is used to stage all changes in your working directory, including modified, deleted, and untracked files. It adds all changes to the staging area (also known as the index) in preparation for the next commit.

hen you run git add --all, Git scans your entire working directory and stages all changes it detects. It ensures that all modifications, deletions, and new files are included in the staging area.

---

```
--no-all
--ignore-removal
```

Update the index by adding new files that are unknown to the index and files modified in the working tree, but ignore files that have been removed from the working tree. This option is a no-op when no <pathspec> is used.

---

```
-N
--intent-to-add

```

Record only the fact that the path will be added later. An entry for the path is placed in the index with no content. This is useful for, among other things, showing the unstaged content of such files with git diff and committing them with git commit -a.

TODO: FIND MORE INFO.

--

```
--refresh

```

Don’t add the file(s), but only refresh their stat() information in the index.

---

```
--ignore-errors

```

If some files could not be added because of errors indexing them, do not abort the operation, but continue adding the others. The command shall still exit with non-zero status. The configuration variable add.ignoreErrors can be set to true to make this the default behaviour.

The --ignore-errors option in Git is used to ignore certain errors or warnings that occur during the execution of a Git command. It allows the command to continue executing despite encountering errors, rather than aborting the operation completely.

git add --ignore-errors:
This command ignores any errors that occur while adding files to the staging area. If some files cannot be added due to errors (e.g., permission denied or file not found), Git will skip those files and continue adding the rest of the files that can be processed successfully.

The --ignore-errors option provides a way to proceed with a Git operation even if some files or actions encounter errors. It can be useful in scenarios where you want to perform a bulk operation and handle errors separately or when you want to continue with the operation despite encountering non-critical errors.

---

```
--ignore-missing

```

This option can only be used together with --dry-run. By using this option the user can check if any of the given files would be ignored, no matter if they are already present in the work tree or not.

TODO: FIND MORE INFO.

---

```
--no-warn-embedded-repo

```

By default, git add will warn when adding an embedded repository to the index without using git submodule add to create an entry in .gitmodules.

-[Embedded repository](./embedded-repository.md)

---

```
--renormalize

```

Apply the "clean" process freshly to all tracked files to forcibly add them again to the index. This is useful after changing core.autocrlf configuration or the text attribute in order to correct files added with wrong CRLF/LF line endings. This option implies -u. Lone CR characters are untouched, thus while a CRLF cleans to LF, a CRCRLF sequence is only partially cleaned to CRLF.

The --renormalize option in Git is used with the git add command to reapply text normalization to the changes being staged. It forces Git to normalize line endings and other whitespace-related changes based on the repository's configured text attributes.

When you run git add --renormalize, Git examines the changes being staged and applies text normalization rules to ensure consistent line endings and whitespace handling based on the repository's configuration.

This command applies text normalization to the changes you have made in your working directory before staging them. It can be useful in situations where the repository's text attributes have been updated or modified, and you want to ensure that the staged changes adhere to the updated normalization rules.

Text normalization in Git includes actions such as converting line endings, removing trailing whitespaces, and applying other configured rules to maintain consistency in text files across different platforms and environments.

---

## Examples of git add

```
$ git add Documentation/\*.txt
# Adds content from all *.txt files under Documentation directory and its subdirectories.

$ git add git-*.sh
#Considers adding content from all git-*.sh scripts


```
