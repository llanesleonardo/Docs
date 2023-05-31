# Forks

## Working with forks

A fork is a new repository that shares code and visibility settings with the original “upstream” repository.

Forks let you make changes to a project without affecting the original repository, also known as the "upstream" repository. After you fork a repository, you can fetch updates from the upstream repository to keep your fork up to date, and you can propose changes from your fork to the upstream repository with pull requests. A fork can be owned by either a personal account or an organization.

When you view a forked repository on GitHub, the upstream repository is indicated below the name of the fork.

In open source projects, forks are often used to iterate on ideas or changes before incorporating the changes into the upstream repository. If you fork a public repository to your personal account, make changes, then open a pull request to propose your changes to the upstream repository, you can give anyone with push access to the upstream repository permission to push changes to your pull request branch (including deleting the branch). This speeds up collaboration by allowing repository maintainers to make commits or run tests locally to your pull request branch from a user-owned fork before merging.

You can view, sort, and filter the forks of a repository on the repository's forks page.

You can fork any public repository to your personal account, or to an organization where you have permission to create repositories. If you have access to a private repository and the owner permits forking, you can fork the repository to your personal account, or to an organization on GitHub Team where you have permission to create repositories. You cannot fork a private repository to an organization using GitHub Free.

### Forking a repository versus duplicating a repository

If you want to create a new repository from the contents of an existing repository but don't want to merge your changes to the upstream in the future, you can duplicate the repository or, if the repository is a template, you can use the repository as a template.

[Duplicating a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository)

Forking a repository is similar to duplicating a repository, with the following differences.

1. You can use a pull request to suggest changes from your fork to the upstream repository.
2. You can bring changes from the upstream repository to your fork by synchronizing your fork with the upstream repository.
3. Forks have their own members, branches, tags, labels, policies, issues, pull requests, discussions, actions, projects, and wikis.
4. Forks inherit the restrictions of their upstream repositories. For example, branch protection rules cannot be passed down if the upstream repository belongs to an organization on a GitHub Free plan.

### permissions and visibility of forks

The permissions and visibility of forks depend on whether the upstream repository is public or private, and whether it is owned by an organization.

A fork is a new repository that shares code and visibility settings with the upstream repository. All forks of public repositories are public. You cannot change the visibility of a fork.

All repositories belong to a repository network. A repository network contains the upstream repository, the upstream repository's direct forks, and all forks of those forks. All forks in the repository network have the same visibility setting.

If you delete a repository or change the repository's visibility settings, you will affect the repository's forks.

Private forks inherit the permissions structure of the upstream repository. This helps owners of private repositories maintain control over their code. For example, if the upstream repository is private and gives read/write access to a team, then the same team will have read/write access to any forks of the private upstream repository. Only team permissions (not individual permissions) are inherited by private forks.

Public forks do not inherit the permissions structure of the upstream repository. If you fork a public repository to your personal account, make changes, then open a pull request to propose your changes to the upstream repository, you can give anyone with push access to the upstream repository permission to push changes to your pull request branch (including deleting the branch). This speeds up collaboration by allowing repository maintainers to make commits or run tests locally to your pull request branch from a user-owned fork before merging. You cannot give push permissions to a fork owned by an organization.

### Important security considerations

If you work with forks, or if you're the owner of a repository or organization that allows forking, it's important to be aware of the following security considerations.

- Forks have their own permissions separate from the upstream repository.
- The owners of a repository that has been forked have read permission to all forks in the repository's fork network.
- Organization owners of a repository that has been forked have admin permission to forks created in personal user namespaces, including the ability to delete the fork and its branches.
- Organization owners of a repository that has been forked have read permission to forks created in organizations, but do not have the ability to delete the fork or its branches.
- Forks created in another organization will not be deleted when individual access is removed from the upstream repository.
- Commits to any repository in a fork network can be accessed from any repository in the same fork network, including the upstream repository.

### About forks within an organization

Forks within the same organization copy the collaborators and team settings of their upstream repositories. If a repository is owned by an organization:

- That organization controls the permissions of its forks.
- Any teams from the upstream permission structure that exist and are visible in the target organization or user namespace will have their permissions copied.
- Admin permissions remain with the upstream owner, except when a user forks into a different organization.
- If that repository is forked to a user namespace, the organization maintains admin permissions and any teams with access maintain access.

## Configure a remote repository for a fork

You must configure a remote that points to the upstream repository in Git to sync changes you make in a fork with the original repository. This also allows you to sync changes made in the original repository with the fork.

1. Open Git Bash.
2. List the current configured remote repository for your fork.

```
   $ git remote -v
   > origin https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
   > origin https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
```

3. Specify a new remote upstream repository that will be synced with the fork.

```
   $ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```

4. Verify the new upstream repository you've specified for your fork.

```
   $ git remote -v
   > origin https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
   > origin https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
   > upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
   > upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
```

## Syncing a fork

Sync a fork of a repository to keep it up-to-date with the upstream repository.

1. On GitHub, navigate to the main page of the forked repository that you want to sync with the upstream repository.
2. Above the list of files, select the Sync fork dropdown menu.
3. Review the details about the commits from the upstream repository, then click Update branch.

If the changes from the upstream repository cause conflicts, GitHub will prompt you to create a pull request to resolve the conflicts.

### Syncing a fork branch from the command line

Before you can sync your fork with an upstream repository, you must configure a remote that points to the upstream repository in Git.

1. Open Git Bash.
2. Change the current working directory to your local project.
3. Fetch the branches and their respective commits from the upstream repository. Commits to BRANCHNAME will be stored in the local branch upstream/BRANCHNAME.

```
    $ git fetch upstream
    > remote: Counting objects: 75, done.
    > remote: Compressing objects: 100% (53/53), done.
    > remote: Total 62 (delta 27), reused 44 (delta 9)
    > Unpacking objects: 100% (62/62), done.
    > From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
    >  * [new branch]      main     -> upstream/main
```

4. Check out your fork's local default branch - in this case, we use main.

```
    $ git checkout main
    > Switched to branch 'main'
```

5. Merge the changes from the upstream default branch - in this case, upstream/main - into your local default branch. This brings your fork's default branch into sync with the upstream repository, without losing your local changes.

```
$ git merge upstream/main
> Updating a422352..5fdff0f
> Fast-forward
>  README                    |    9 -------
>  README.md                 |    7 ++++++
>  2 files changed, 7 insertions(+), 9 deletions(-)
>  delete mode 100644 README
>  create mode 100644 README.md
```

If your local branch didn't have any unique commits, Git will perform a fast-forward.

```
$ git merge upstream/main
> Updating 34e91da..16c56ad
> Fast-forward
>  README.md                 |    5 +++--
>  1 file changed, 3 insertions(+), 2 deletions(-)
```

If your local branch had unique commits, you may need to resolve conflicts.

## Allowing changes to a pull request branch created from a fork

[Allowing changes to a pull request branch created from a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/allowing-changes-to-a-pull-request-branch-created-from-a-fork)

## What happens to forks when a repository is deleted or changes visibility?

Deleting your repository or changing its visibility affects that repository's forks.

### Deleting a private repository

When you delete a private repository, all of its private forks are also deleted.

### Deleting a public repository

When you delete a public repository, one of the existing public forks is chosen to be the new upstream repository. All other repositories are forked off of this new upstream and subsequent pull requests go to this new upstream repository.

### Private forks and permissions

Private forks inherit the permissions structure of the upstream repository. This helps owners of private repositories maintain control over their code. For example, if the upstream repository is private and gives read/write access to a team, then the same team will have read/write access to any forks of the private upstream repository. Only team permissions (not individual permissions) are inherited by private forks.

[Changing a public repo to a private repository](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/what-happens-to-forks-when-a-repository-is-deleted-or-changes-visibility#changing-a-public-repository-to-a-private-repository)

[Changing a private repo to a public repository](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/what-happens-to-forks-when-a-repository-is-deleted-or-changes-visibility#changing-a-private-repository-to-a-public-repository)
