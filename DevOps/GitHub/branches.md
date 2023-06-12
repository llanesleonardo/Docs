[Table contents](./1-tablecontent.md)

# Git Repository Branches

## About branches

---

Use a branch to isolate development work without affecting other branches in the repository. Each repository has one default branch, and can have multiple other branches. You can merge a branch into another branch using a pull request.

Branches allow you to develop features, fix bugs, or safely experiment with new ideas in a contained area of your repository.

You always create a branch from an existing branch. Typically, you might create a new branch from the default branch of your repository.

You can then work on this new branch in isolation from changes that other people are making to the repository. A branch you create to build a feature is commonly referred to as a feature branch or topic branch.

You can also use a branch to publish a GitHub Pages site.

You must have write access to a repository to create a branch, open a pull request, or delete and restore branches in a pull request.

### About the default branch

---

When you create a repository with content on GitHub.com, GitHub creates the repository with a single branch. This first branch in the repository is the default branch. The default branch is the branch that GitHub displays when anyone visits your repository. The default branch is also the initial branch that Git checks out locally when someone clones the repository. Unless you specify a different branch, the default branch in a repository is the base branch for new pull requests and code commits.

By default, GitHub names the default branch main in any new repository.

You can change the default branch for an existing repository.

You can set the name of the default branch for new repositories.

## Viewing branches in your repository

---

Branches are central to collaboration on GitHub, and the best way to view them is the branches page.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. From the file tree view on the left, select the branch dropdown menu, then click View all branches. You can also find the branch dropdown menu at the top of the integrated file editor
3. Use the navigation at the top of the page to view specific lists of branches:
   - Your branches: In repositories that you have push access to, the Yours view shows all branches that you’ve pushed to, excluding the default branch, with the most recent branches first.
   - Active branches: The Active view shows all branches (excluding the default branch) that anyone has committed to within the last three months, ordered by the branches with the most recent commits first.
   - Stale branches: The Stale view shows all branches that no one has committed to in the last three months, ordered by the branches with the oldest commits first. Use this list to determine which branches to delete.
   - All branches: The All view shows the default branch, followed by all other branches ordered by the branches with the most recent commits first.
4. Optionally, use the search field on the top right. It provides a simple, case-insensitive, sub-string search on the branch name. It does not support any additional query syntax.

## Renaming a branch

---

### Process'checklist

1. On GitHub.com, navigate to the main page of the repository
2. From the file tree view on the left, select the branch dropdown menu, then click View all branches. You can also find the branch dropdown menu at the top of the integrated file editor
3. Next to the branch you want to rename, click
4. Type a new name for the branch
5. Review the information about local environments, then click Rename branch

## Updating a local clone after a branch name changes

---

After you rename a branch in a repository on GitHub, any collaborator with a local clone of the repository will need to update the clone.

From the local clone of the repository on a computer, run the following commands to update the name of the default branch.

```
    $ git branch -m OLD-BRANCH-NAME NEW-BRANCH-NAME
    $ git fetch origin
    $ git push origin NEW-BRANCH-NAME
    $ git branch -u origin/NEW-BRANCH-NAME NEW-BRANCH-NAME
    $ git remote set-head origin -a
```

Optionally, run the following command to remove tracking references to the old branch name.

```
    $ git remote prune origin
```

## Create a new remote branches

---

The next code will create a new remote branch after the push command is executed.

```
    git push REMOTE-NAME LOCAL-BRANCH-NAME:REMOTE-BRANCH-NAME
```

This pushes the LOCAL-BRANCH-NAME to your REMOTE-NAME, but it is renamed to REMOTE-BRANCH-NAME.

## Delete a branch

---

The syntax to delete a branch is a bit arcane at first glance:

```
    git push REMOTE-NAME :BRANCH-NAME
```

Note that there is a space before the colon. The command resembles the same steps you'd take to rename a branch. However, here, you're telling Git to push nothing into BRANCH-NAME on REMOTE-NAME. Because of this, git push deletes the branch on the remote repository.

## Changing the default branch

---

If you have more than one branch in your repository, you can configure any branch as the default branch.
You can choose the default branch for a repository. The default branch is the base branch for pull requests and code commits.

To change the default branch, your repository must have more than one branch.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings.
3. Under "Default branch", to the right of the default branch name, click
4. Select the branch dropdown menu and click a branch name
5. Click Update
6. Read the warning, then click I understand, update the default branch

## Deleting and restoring branches in a pull request

---

If you have write access in a repository, you can delete branches that are associated with closed or merged pull requests. You cannot delete branches that are associated with open pull requests.
You can delete a branch that is associated with a pull request if the pull request has been merged or closed and there are no other open pull requests referencing the branch.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Pull requests
3. To see a list of closed pull requests, click Closed
4. In the list of pull requests, click the pull request that's associated with the branch that you want to delete
5. Near the bottom of the pull request, click Delete branch
   1. This button isn't displayed if there's currently an open pull request for this branch.

## Restoring a deleted branch

---

You can restore the head branch of a closed pull request.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Pull requests
3. To see a list of closed pull requests, click Closed
4. In the list of pull requests, click the pull request that's associated with the branch that you want to restore
5. Near the bottom of the pull request, click Restore branch
