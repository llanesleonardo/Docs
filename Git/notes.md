# Git - Version control system

These docs were gathered from various sources, such as:

[Git Software](https://git-scm.com/)

## Setup Git

- [setup Git](https://docs.github.com/en/get-started/quickstart/set-up-git)
- [Git software](https://git-scm.com/downloads)

### set your Git username fro every repository on your computer

    $ git config --global user.name "Mona Lisa"
    $ git config --global user.name

### Authenticating with Github from Git

There are two way of doing this:

- HTTPS
- SSH (best practice)

### About version control and Git

A version control system, or VCS, tracks the history of changes as people and teams collaborate on projects together. As developers make changes to the project, any earlier version of the project can be recovered at any time.

Developers can review project history to find out

- Which changes were made?
- Who made the changes?
- When were the changes made?
- Why were changes needed?

VCSs give each contributor a unified and consistent view of a project, surfacing work that's already in progress. Seeing a transparent history of changes, who made them, and how they contribute to the development of a project helps team members stay aligned while working independently.

Git is the most popular distributed version control system. Git is commonly used for both open source and commercial software development, with significant benefits for individuals, teams and businesses.

- Git lets developers see the entire timeline of their changes, decisions, and progression of any project in one place. From the moment they access the history of a project, the developer has all the context they need to understand it and start contributing.
- Developers work in every time zone. With a DVCS like Git, collaboration can happen any time while maintaining source code integrity. Using branches, developers can safely propose changes to production code.
- Businesses using Git can break down communication barriers between teams and keep them focused on doing their best work. Plus, Git makes it possible to align experts across a business to collaborate on major projects.

### About repositories

A repository, or Git project, encompasses the entire collection of files and folders associated with a project, along with each file's revision history. The file history appears as snapshots in time called commits. The commits can be organized into multiple lines of development called branches. Because Git is a DVCS, repositories are self-contained units and anyone who has a copy of the repository can access the entire codebase and its history. Using the command line or other ease-of-use interfaces, a Git repository also allows for: interaction with the history, cloning the repository, creating branches, committing, merging, comparing changes across versions of code, and more.

Through platforms like GitHub, Git also provides more opportunities for project transparency and collaboration. Public repositories help teams work together to build the best possible final product.

### Basic git commands

To use Git, developers use specific commands to copy, create, change, and combine code. These commands can be executed directly from the command line or by using an application like GitHub Desktop. Here are some common commands for using Git:

- git init initializes a brand new Git repository and begins tracking an existing directory. It adds a hidden subfolder within the existing directory that houses the internal data structure required for version control.
- git clone creates a local copy of a project that already exists remotely. The clone includes all the project's files, history, and branches.
- git add stages a change. Git tracks changes to a developer's codebase, but it's necessary to stage and take a snapshot of the changes to include them in the project's history. This command performs staging, the first part of that two-step process. Any changes that are staged will become a part of the next snapshot and a part of the project's history. Staging and committing separately gives developers complete control over the history of their project without changing how they code and work.
- git commit saves the snapshot to the project history and completes the change-tracking process. In short, a commit functions like taking a photo. Anything that's been staged with git add will become a part of the snapshot with git commit.
- git status shows the status of changes as untracked, modified, or staged.
- git branch shows the branches being worked on locally.
- git merge merges lines of development together. This command is typically used to combine changes made on two distinct branches. For example, a developer would merge when they want to combine changes from a feature branch into the main branch for deployment.
- git pull updates the local line of development with updates from its remote counterpart. Developers use this command if a teammate has made commits to a branch on a remote, and they would like to reflect those changes in their local environment.
- git push updates the remote repository with any commits made locally to a branch. [Push commits to a remote](https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository)

More about:

- [Contribute to an existing repository or an existing branch](https://docs.github.com/en/get-started/using-git/about-git)

### Splitting a subfolder out into a new repository

If you create a new clone of the repository, you won't lose any of your Git history or changes when you split a folder into a separate repository.

1. Terminal
2. Change the current working directory to the location where you want to create your new repository
3. Clone the repository that contains the subfolder
   $ git clone https://github.com/USERNAME/REPOSITORY-NAME
4. Change the current working directory to your cloned repository.
   $ cd REPOSITORY-NAME
5. To filter the subfolder from the rest of the files in the repository yo should use: [git-filter-repo5](https://github.com/newren/git-filter-repo)
6. Create a new repository on GitHub
7. At the top of your new repository on GitHub.com's Quick Setup page, click to copy the remote repository URL
8. Add a new remote name with the URL you copied for your repository. For example, origin or upstream are two common choices
9. Verify that the remote URL was added with your new repository name
10. Push your changes to the new repository on GitHub.

### Subtree merges

[More about about-git-subtree-merges](https://docs.github.com/en/get-started/using-git/about-git-subtree-merges)

#### Setting up the empty repository for a subtree merge

1. Terminal
2. Create a new directory and navigate to it
3. Initialize a new Git repository
4. Create and commit a new file

#### Adding a new repository as a subtree

1. Add a new remote URL pointing to the separate project that we're interested in
2. Merge the Spoon-Knife project into the local Git project. This doesn't change any of your files locally, but it does prepare Git for the next step
   $ git merge -s ours --no-commit --allow-unrelated-histories spoon-knife/main
   Automatic merge went well; stopped before committing as requested
3. Create a new directory called spoon-knife, and copy the Git history of the Spoon-Knife project into it
   git read-tree --prefix=spoon-knife/ -u spoon-knife/main
4. Commit the changes to keep them safe
   $ git commit -m "Subtree merged in spoon-knife"
   [main fe0ca25] Subtree merged in spoon-knife

Although we've only added one subproject, any number of subprojects can be incorporated into a Git repository.

#### Synchronizing with updates and changes

When a subproject is added, it is not automatically kept in sync with the upstream changes. You will need to update the subproject with the following command:

    $ git pull -s subtree REMOTE-NAME BRANCH-NAME

For the example above, this would be:

    $ git pull -s subtree spoon-knife main

### Git rebase

The git rebase command allows you to easily change a series of commits, modifying the history of your repository. You can reorder, edit, or squash commits together.

Typically, you would use git rebase to:

- Edit previous commit messages
- Combine multiple commits into one
- Delete or revert commits that are no longer necessary

#### Rebasing commits against a branch

To rebase all the commits between another branch and the current branch state, you can enter the following command in your shell (either the command prompt for Windows, or the terminal for Mac and Linux):

    $ git rebase --interactive OTHER-BRANCH-NAME

#### Rebasing commits against a point in time

## Common errors

- [The SSH agent is not running](https://stackoverflow.com/questions/17846529/could-not-open-a-connection-to-your-authentication-agent)
- [The SSH Agent has not entities](https://stackoverflow.com/questions/26505980/github-permission-denied-ssh-add-agent-has-no-identities)
- [Working with SSH key passphrases](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)
- [Find if your private keys were added to SSH Agent](https://www.freecodecamp.org/news/how-to-manage-multiple-ssh-keys/)
- [Unprotected private key file](https://www.howtogeek.com/168119/fixing-warning-unprotected-private-key-file-on-linux/)
- [Non fast forward Errors](https://docs.github.com/en/get-started/using-git/dealing-with-non-fast-forward-errors)
- [Merge conflict](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)
- [About pull request merges](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges)
