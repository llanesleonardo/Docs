# Git cherry pick

Apply the changes introduced by some existing commits.

Given one or more existing commits, apply the change each one introduces, recording a new commit for each. This requires your working tree to be clean (no modifications from the HEAD commit).

When it is not obvious how to apply a change, the following happens:

1. The current branch and HEAD pointer stay at the last commit successfully made.
2. The CHERRY_PICK_HEAD ref is set to point at the commit that introduced the change that is difficult to apply.
3. Paths in which the change applied cleanly are updated both in the index file and in your working tree.
4. For conflicting paths, the index file records up to three versions, as described in the "TRUE MERGE" section of git-merge[1]. The working tree files will include a description of the conflict bracketed by the usual conflict markers <<<<<<< and >>>>>>>.
5. No other modifications are made.

The purpose of git cherry-pick is to apply specific commits from one branch onto another branch. It allows you to select individual commits and incorporate them into a different branch, essentially
replaying those commits on top of the current branch.

The benefits of using git cherry-pick include:

- Selective commit application: You have granular control over which commits to apply, allowing you to cherry-pick only the desired changes.
- Avoiding unnecessary merge conflicts: Since git cherry-pick applies individual commits, it can help avoid conflicts that might arise from merging larger branches.
- Maintaining a clean commit history: By cherry-picking specific commits, you can keep your commit history focused and organized, incorporating only the relevant changes.

## Options

<commit>…​
Commits to cherry-pick. For a more complete list of ways to spell commits, see gitrevisions[7]. Sets of commits can be passed but no traversal is done by default, as if the --no-walk option was specified, see git-rev-list[1]. Note that specifying a range will feed all <commit>…​ arguments to a single revision walk (see a later example that uses maint master..next).

TODO: FIND MORE INFO.

---

```
-e
--edit

```

With this option, git cherry-pick will let you edit the commit message prior to committing.

```
-x
```

When recording the commit, append a line that says "(cherry picked from commit …​)" to the original commit message in order to indicate which commit this change was cherry-picked from. This is done only for cherry picks without conflicts.

TODO: FIND MORE INFO.

---

```
-m <parent-number>
--mainline <parent-number>

```

Usually you cannot cherry-pick a merge because you do not know which side of the merge should be considered the mainline. This option specifies the parent number (starting from 1) of the mainline and allows cherry-pick to replay the change relative to the specified parent.

---

```
-n
--no-commit
```

The -n option in git cherry-pick is used to perform a "no-commit" cherry-pick. When you use git cherry-pick -n <commit>, Git applies the changes from the specified commit onto the current branch, but it does not automatically create a new commit with those changes.

The purpose of using -n with git cherry-pick is to give you the opportunity to make additional modifications or adjustments to the changes before committing them. It allows you to further refine or tailor the cherry-picked changes to better suit your needs.

Here's how the -n option affects the cherry-pick process:

- You identify the commit you want to cherry-pick and run git cherry-pick -n <commit>.
- Git applies the changes from the specified commit onto the current branch, but it does not automatically create a new commit.
- After the cherry-pick is complete, the changes from the cherry-picked commit are staged but not committed. Git leaves the changes in the working directory and the staging area.
- You can now make additional modifications to the changes if needed. This could involve adjusting the code, resolving conflicts, or making any necessary tweaks.
- Once you're satisfied with the modifications, you manually stage the changes using git add.
- Finally, you create a new commit to capture the modified changes using git commit. Git will prompt you to provide a commit message for the new commit.

By using git cherry-pick -n, you have more control over the cherry-picked changes and the ability to fine-tune them before committing. It allows you to review and modify the changes as needed, ensuring that they fit well within the context of your current branch.

```
-s
--signoff
```

Add a Signed-off-by trailer at the end of the commit message.

The --signoff option in git cherry-pick is used to automatically add a "Signed-off-by" line to the commit message of the cherry-picked commit. The "Signed-off-by" line is a convention commonly used in Git commit messages to indicate that the author of the commit has agreed to the project's Contributor License Agreement (CLA) or Developer Certificate of Origin (DCO).

The purpose of using --signoff with git cherry-pick is to acknowledge and record the origin of the commit. It helps track the history of the commit and provides a record of the author's agreement to the project's licensing terms.

When you run git cherry-pick --signoff <commit>, Git performs the cherry-pick operation as usual, applying the changes from the specified commit onto the current branch. Additionally, it automatically appends the following line to the commit message:

```
Signed-off-by: Your Name <your.email@example.com>

```

The Signed-off-by line includes the name and email address associated with your Git configuration. This indicates that you, as the cherry-pick author, certify that you have the right to submit the changes and agree to the project's licensing terms.

---

```
-S[<keyid>]
--gpg-sign[=<keyid>]
--no-gpg-sign
```

GPG-sign commits. The keyid argument is optional and defaults to the committer identity; if specified, it must be stuck to the option without a space. --no-gpg-sign is useful to countermand both commit.gpgSign configuration variable, and earlier --gpg-sign.

```
--ff
```

If the current HEAD is the same as the parent of the cherry-pick’ed commit, then a fast forward to this commit will be performed.

```
--strategy=<strategy>
```

Use the given merge strategy.

The --strategy option in git cherry-pick is used to specify the merge strategy to be used when applying the changes from the cherry-picked commit. It allows you to override the default merge strategy and choose a different strategy tailored to your specific needs.

By default, git cherry-pick uses the "recursive" merge strategy, which is the most common and versatile strategy for combining changes. However, you can use --strategy to select a different strategy if necessary.

Some common --strategy options include:

- recursive (default): The default merge strategy that performs a recursive three-way merge.
- resolve: A simpler merge strategy that performs a two-way merge, discarding the common ancestor.
- ours: Resolves conflicts by keeping the version from the current branch, effectively ignoring changes from the cherry-picked commit.
- theirs: Resolves conflicts by keeping the version from the cherry-picked commit, discarding changes from the current branch.

Note that the available merge strategies can vary depending on your Git version.

## Sequencer subcommands

```
--continue
```

Continue the operation in progress using the information in .git/sequencer. Can be used to continue after resolving conflicts in a failed cherry-pick or revert.

```
--skip
```

Skip the current commit and continue with the rest of the sequence.

```
--quit
```

Forget about the current operation in progress. Can be used to clear the sequencer state after a failed cherry-pick or revert.

```
--abort
```

Cancel the operation and return to the pre-sequence state.

## Examples

- Applying specific bug fixes: Suppose you have a branch with various commits, and you identify a specific commit that fixes a bug. Instead of merging the entire branch, you can cherry-pick that commit onto the branch where you want to apply the fix.
- Selectively adding features: If you have a branch with multiple commits introducing different features, you can cherry-pick only the commits related to a specific feature onto another branch.
- Incorporating changes from upstream: If you have a forked repository and want to bring in changes from the original repository, you can cherry-pick the relevant commits onto your forked branch.

```
git cherry-pick master

```

Apply the change introduced by the commit at the tip of the master branch and create a new commit with this change.

---

```
git cherry-pick ..master
git cherry-pick ^HEAD master

```

[cherry-pick](https://www.youtube.com/watch?v=i657Bg_HAWI)
[cherry-pick conflicts](https://www.youtube.com/watch?v=aUeNbpSkY8k)

Apply the changes introduced by all commits that are ancestors of master but not of HEAD to produce new commits.

```
git cherry-pick maint next ^master
git cherry-pick maint master..next
```

Apply the changes introduced by all commits that are ancestors of maint or next, but not master or any of its ancestors. Note that the latter does not mean maint and everything between master and next; specifically, maint will not be used if it is included in master.

```
git cherry-pick -n master~1 next
```

Apply to the working tree and the index the changes introduced by the second last commit pointed to by master and by the last commit pointed to by next, but do not create any commit with these changes.

```
git cherry-pick --ff ..next
```

If history is linear and HEAD is an ancestor of next, update the working tree and advance the HEAD pointer to match next. Otherwise, apply the changes introduced by those commits that are in next but not HEAD to the current branch, creating a new commit for each new change.
