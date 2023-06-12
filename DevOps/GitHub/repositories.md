Back: [Table contents](./1-tablecontent.md)

# Repositories

## Create a repository

---

To start a project on Github, you will ned to create a repository (main object on github).

Every repository needs a license:

- [Licenses](https://choosealicense.com/)

Then you have to click the plus icon on the right corner of the main page on Github.

### Process' checklist

1. Plus sign icon (on the left corner of the page)
2. New repository
3. Repository name (Unique)
4. Add description
5. add README file (optional)
6. Review and finalize the repository creation

## Creating a repository from a template

---

You can generate a new repository with the same directory structure and files as an existing repository. Anyone with read permissions to a template repository can create a repository from that template.

You can choose to include the directory structure and files from only the default branch of the template repository or to include all branches. Branches created from a template have unrelated histories, which means you cannot create pull requests or merge between the branches.

Creating a repository from a template is similar to forking a repository, but there are important differences:

- A new fork includes the entire commit history of the parent repository, while a repository created from a template starts with a single commit.
- Commits to a fork don't appear in your contributions graph, while commits to a repository created from a template do appear in your contribution graph.
- A fork can be a temporary way to contribute code to an existing project, while creating a repository from a template starts a new project quickly.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Above the file list, click Use this template
3. Select Create a new repository
4. Use the Owner dropdown menu to select the account you want to own the repository
5. Choose a repository visibility
6. Optionally, to include the directory structure and files from all branches in the template, and not just the default branch, select Include all branches
7. Optionally, if the personal account or organization in which you're creating uses any GitHub Apps from GitHub Marketplace, select any apps you'd like to use in the repository
8. Click Create repository from template

## Creating a template repository

---

You can make an existing repository a template, so you and others can generate new repositories with the same directory structure, branches, and files.
To create a template repository, you must create a repository, then make the repository a template.

After you make your repository a template, anyone with access to the repository can generate a new repository with the same directory structure and files as your default branch. They can also choose to include all the other branches in your repository. Branches created from a template have unrelated histories, so you cannot create pull requests or merge between the branches.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. Select Template repository

## Creating an issues-only repository

---

GitHub does not provide issues-only access permissions, but you can accomplish this using a second repository which contains only the issues.

### Process' checklist

1. Create a private repository to host the source code from your project
2. reate a second repository with the permissions you desire to host the issue tracker
3. Add a README file to the issues repository explaining the purpose of this repository and linking to the issues section
4. Set your collaborators or teams to give access to the repositories as you desire

Users with write access to both can reference and close issues back and forth across the repositories, but those without the required permissions will see references that contain a minimum of information.

## Create a commit on the terminal

A commit is like a snapshot of all the files in your project at a particular point in time.

```
    git add .
    git commit -m "first commit"
    git push origin main
```

these commands are making a "commit" to the default branch, if you want to create a branch you should go here:

- [branches](./branches.md)

After a commit you should create a "Pull Request":

- [Pull Request](./pullrequest.md)

## Create a commit on the graphic interface

---

### Process checklist

1. Edit README file
2. Make some changes to the file
3. Preview the changes you made to the file
4. Commit changes
5. Create a Pull Request

## About README's

---

You can add a README file to your repository to tell other people why your project is useful, what they can do with your project, and how they can use it.

A README is often the first item a visitor will see when visiting your repository. README files typically include information on:

- What the project does
- Why the project is useful
- How users can get started with the project
- Where users can get help with your project
- Who maintains and contributes to the project

If you put your README file in your repository's hidden .github, root, or docs directory, GitHub will recognize and automatically surface your README to repository visitors.

## Cloning a repository

---

You can clone an existing repository from GitHub to your local computer, making it easier to add or remove files, fix merge conflicts, or make complex commits. Cloning a repository pulls down a full copy of all the repository data that GitHub has at that point in time, including all versions of every file and folder for the project.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Above the list of files, click <> Code
3. Copy the URL for the repository (HTTPS - SSH)
4. Open terminal
5. Change the current working directory to the location where you want the cloned directory
6. Type git clone, and then paste the URL you copied earlier
7. Press Enter to create your local clone

This process also works for an empty repository.

## Forking a repository

---

### More information:

- [Fork a repository](./forks.md)

## Creating remote repositories

You can use the git remote add command to match a remote URL with a name. For example, you'd type the following in the command line:

```
    git remote add origin <REMOTE_URL>
```

This associates the name origin with the REMOTE_URL.

You can use the command git remote set-url to change a remote's URL.

### More information:

- [Managing remote repositories](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)
- [HTTPS URL'S - SSH URL'S](https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories)

## Adding a file to a repository

---

### More information:

[Managing files](./workingfiles.md)

## Verify new remote repository

---

```
    $ git remote -v
    # Verify new remote
    origin  https://github.com/OWNER/REPOSITORY.git (fetch)
    origin  https://github.com/OWNER/REPOSITORY.git (push)
```

## Switching remote URL's from SSH to HTTPS

---

List your existing remotes in order to get the name of the remote you want to change.

```
    $ git remote -v
    origin  git@github.com:OWNER/REPOSITORY.git (fetch)
    origin  git@github.com:OWNER/REPOSITORY.git (push)
```

Change your remote's URL from SSH to HTTPS with the git remote set-url command.

```
    $ git remote set-url origin https://github.com/OWNER/REPOSITORY.git
```

Verify that the remote URL has changed.

```
    $ git remote -v # Verify new remote URL
    origin https://github.com/OWNER/REPOSITORY.git (fetch)
    origin https://github.com/OWNER/REPOSITORY.git (push)
```

Same process the other way around.

## Renaming a remote repository

---

```
    $ git remote rename origin destination
```

    Change remote name from 'origin' to 'destination'

## Remove a repository

---

```
    $ git remote rm destination
    # Remove remote
```

## Fetching changes from a remote repository

---

Use git fetch to retrieve new work done by other people. Fetching from a repository grabs all the new remote-tracking branches and tags without merging those changes into your own branches.

If you already have a local repository with a remote URL set up for the desired project, you can grab all the new information by using git fetch _remotename_ in the terminal:

```
    $ git fetch REMOTE-NAME
    # Fetches updates made to a remote repository
```

## Merging changes into your local branch

---

Merging combines your local changes with changes made by others.

Typically, you'd merge a remote-tracking branch (i.e., a branch fetched from a remote repository) with your local branch:

```
    $ git merge REMOTE-NAME/BRANCH-NAME
    # Merges updates made online with your local work
```

## Pulling changes from a remote repository

---

git pull is a convenient shortcut for completing both git fetch and git merge in the same command:

```
    $ git pull REMOTE-NAME BRANCH-NAME
    # Grabs online updates and merges them with your local work
```

Because pull performs a merge on the retrieved changes, you should ensure that your local work is committed before running the pull command. If you run into a merge conflict you cannot resolve, or if you decide to quit the merge, you can use git merge --abort to take the branch back to where it was in before you pulled.

# Repository settings

---

### More information:

- [Repository settings](./repositoriesettings.md)

## Classifying your repository with topics

---

To help other people find and contribute to your project, you can add topics to your repository related to your project's intended purpose, subject area, affinity groups, or other important qualities.

Topics appear on the main page of a repository. You can click a topic name to see related topics and a list of other repositories classified with that topic.

To browse the most used topics, go to:

- [Github Topics](https://github.com/topics/).

Repository admins can add any topics they'd like to a repository. Helpful topics to classify a repository include the repository's intended purpose, subject area, community, or language.

Public and private repositories can have topics, although you will only see private repositories that you have access to in topic search results.

When creating a topic:

- use lowercase letters, numbers, and hyphens.
- use 50 characters or less.
- add no more than 20 topics.

## Adding topics to your repository

---

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. In the top right corner of the page, to the right of "About", click
3. Under "Topics", start to type the topic you want to add to your repository to display a dropdown menu of any matching topics. Click the topic you want to add or continue typing to create a new topic
4. Optional, if there are "Suggested" topics displayed under the "Topics" field, click to add or to decline the suggested topic
5. After you've finished adding topics, click Save changes

## Configuring tag protection rules

---

You can configure tag protection rules for your repository to prevent contributors from creating or deleting tags.

When you add a tag protection rule, all tags that match the pattern provided will be protected. Only users with admin or maintain permissions, or custom roles with the "edit repository rules" permission in the repository will be able to create protected tags, and only users with admin permissions or custom roles with the "edit repository rules" permission in the repository will be able to delete protected tags. GitHub Apps require the Repository administration: write permission to modify a protected tag.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings.
3. In the "Code and automation" section of the sidebar, click Tags
4. Click New rule
5. Under "Tag name pattern", type the pattern of the tags you want to protect. In this example, typing "\*" protects all tags
6. Click Add rule

## Managing GitHub Actions settings for a repository

---

You can disable or configure GitHub Actions for a specific repository.
By default, GitHub Actions is enabled on all repositories and organizations.

You can enable GitHub Actions for your repository. When you enable GitHub Actions, workflows are able to run actions and reusable workflows located within your repository and any other public repository. When you disable GitHub Actions, no workflows run in your repository.

Alternatively, you can enable GitHub Actions in your repository but limit the actions and reusable workflows a workflow can run.

You can disable GitHub Actions for a repository, or set a policy that configures which actions and reusable workflows can be used in the repository.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the left sidebar, click Actions, then click General
4. Under "Actions permissions", select an option
5. Click Save

### More information:

- [Specific selection of workflows](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#allowing-select-actions-and-reusable-workflows-to-run)
- [GitHub Token](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#setting-the-permissions-of-the-github_token-for-your-repository)
- [Retention period for artifacts](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#configuring-the-retention-period-for-github-actions-artifacts-and-logs-in-your-repository)

## Customizing your repository's social media preview

---

You can customize the image displayed on social media platforms when someone links to your repository.

Until you add an image, repository links expand to show basic information about the repository and the owner's avatar. Adding an image to your repository can help identify your project across various social platforms.

You can upload an image to a public repository, or to a private repository to which you have previously uploaded an image. Your image can only be shared from a public repository.

Your image should be a PNG, JPG, or GIF file under 1 MB in size. For the best quality rendering, we recommend keeping the image at 640 by 320 pixels.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. Under "Social preview," click Edit
   1. To add a new image, click Upload an image....
   2. To remove an image, click Remove image

## About code owners

---

You can use a CODEOWNERS file to define individuals or teams that are responsible for code in a repository.

People with admin or owner permissions can set up a CODEOWNERS file in a repository.

The people you choose as code owners must have write permissions for the repository. When the code owner is a team, that team must be visible and it must have write permissions, even if all the individual members of the team already have write permissions directly, through organization membership, or through another team membership.

Code owners are automatically requested for review when someone opens a pull request that modifies code that they own. Code owners are not automatically requested to review draft pull requests.
When you mark a draft pull request as ready for review, code owners are automatically notified. If you convert a pull request to a draft, people who are already subscribed to notifications are not automatically unsubscribed.

When someone with admin or owner permissions has enabled required reviews, they also can optionally require approval from a code owner before the author can merge a pull request in the repository.

If a file has a code owner, you can see who the code owner is before you open a pull request. In the repository, you can browse to the file and hover over to see a tool tip with codeownership details.

### More information:

- [Specify more than one codeowner](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#codeowners-file-location)
- [codeowner syntax](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#codeowners-syntax)

A CODEOWNERS file uses a pattern that follows most of the same rules used in gitignore files. The pattern is followed by one or more GitHub usernames or team names using the standard @username or @org/team-name format. Users and teams must have explicit write access to the repository, even if the team's members already have access.

If you want to match two or more code owners with the same pattern, all the code owners must be on the same line. If the code owners are not on the same line, the pattern matches only the last mentioned code owner.

### More information:

- [Example of codeowner file](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#example-of-a-codeowners-file)
