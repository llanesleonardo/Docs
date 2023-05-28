# Github - Web-based version control system (Use git)

These docs were gathered from various sources, such as:

- [Connecting to github with ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Github users](https://docs.github.com/en/enterprise-cloud@latest/admin/user-management)
- [Github Glossary](https://docs.github.com/en/get-started/quickstart/github-glossary)
- [Free courses](https://docs.github.com/en/get-started/quickstart/git-and-github-learning-resources)

if you need a quick reference you should go here:

[Cheatsheet](https://training.github.com/downloads/es_ES/github-git-cheat-sheet.pdf)

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

## Managing SSH Keys

This topic is one of the basic and most important subjects around git and github.

Configure ssh keys the right way will give you some benefits:

- Save time everyday at work
- Connect to Github securely
- Each user can store one or more ssh keys

SSH KEY AGENT is a cryptography service that already come with Linux and MacOS. You can use this service in Windows Operation system installing WSL2 (windows subsystem linux 2).

If you do not want to use WSL, you can download Putty for this purposes.

### Start ssh agent

This way you can ensure the ssh-agent is running.

    start the ssh-agent in the background
    $ eval "$(ssh-agent -s)"
    Agent pid 59566

### Check for existing SSH Keys

You should have checked for existing SSH keys and generated a new SSH key.

if you do not have a ssh key, you have to generate it.

    $ ssh-keygen -t ed25519 -C "your_github_email@ejemplo.com"

You can use many types of algorithm like rsa, ed25519 and others.

    $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

The best practice should always add all your keys to the same path.

### Add your SSH private key to the ssh-agent

Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_ed25519 in the command with the name of your private key file.

    $ ssh-add ~/.ssh/id_rsa_gh

id_rsa_gh is the private key that the ssh agent has to add to its configuration file. This is the second step allow ssh-agent and github to connect and send information with each other.

After adding or during the creation a ssh key the prompt will ask you for a passphrase, this is a password like phrase.

    Enter passphrase (empty for no passphrase): [Type a passphrase]
    Enter same passphrase again: [Type passphrase again]

DO NOT share your passphrase and ssh private keys with anyone.

### Common errors

- [The SSH agent is not running](https://stackoverflow.com/questions/17846529/could-not-open-a-connection-to-your-authentication-agent)
- [The SSH Agent has not entities](https://stackoverflow.com/questions/26505980/github-permission-denied-ssh-add-agent-has-no-identities)
- [Working with SSH key passphrases](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)
- [Find if your private keys were added to SSH Agent](https://www.freecodecamp.org/news/how-to-manage-multiple-ssh-keys/)
- [Unprotected private key file](https://www.howtogeek.com/168119/fixing-warning-unprotected-private-key-file-on-linux/)

## Profile & Managing users

#### Collaborators

You can collaborate on your project with others using your repository's issues, pull requests, and project boards. You can invite other people to your repository as collaborators from the Collaborators tab in the repository settings.

Inviting collaborators to a personal repository

You can send an invitation to collaborate in your repository directly to someone on GitHub.com, or to the person's email address

GitHub limits the number of people who can be invited to a repository within a 24-hour period. If you exceed this limit, either wait 24 hours or create an organization to collaborate with more people.

1. Ask for the username of the person you're inviting as a collaborator
2. On GitHub.com, navigate to the main page of the repository
3. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
4. In the "Access" section of the sidebar, click Collaborators
5. Click Add People
6. In the search field, start typing the name of person you want to invite, then click a name in the list of matches
7. Click Add NAME to REPOSITORY
8. The user will receive an email inviting them to the repository. Once they accept your invitation, they will have collaborator access to your repository

## Projects

## Repositories

### Create a repository

To start a project on Github, you will ned to create a repository (main object on github).

Every repository needs a license, I am currently studying this topics and you can find them here: [Licenses](https://choosealicense.com/)

Then you have to click the plus icon on the right corner of the main page on Github.

1. Plus sign icon (on the left corner of the page)
2. New repository
3. Repository name (Unique)
4. Add description
5. add README file (optional)
6. Review and finalize the repository creation

### First Commit

A commit is like a snapshot of all the files in your project at a particular point in time.

#### **Terminal**

    git add .
    git commit -m "first commit"
    git push origin main

these commands are making a "commit" to the default branch, if you want to create a branch you should go here: [branches](branches)

After a commit you should create a "Pull Request". [Pull Request](pull_request)

#### Graphic interface

1. Edit README file
2. Make some changes to the file
3. Preview the changes you made to the file
4. Commit changes
5. Create a Pull Request

#### Cloning a repository

You can clone an existing repository from GitHub to your local computer, making it easier to add or remove files, fix merge conflicts, or make complex commits. Cloning a repository pulls down a full copy of all the repository data that GitHub has at that point in time, including all versions of every file and folder for the project.

#### Forking a repository

A fork is a copy of a repository that you manage, where any changes you make will not affect the original repository unless you submit a pull request to the project owner. Most commonly, forks are used to either propose changes to someone else's project or to use someone else's project as a starting point for your own idea.

## Branches

[Branches](#branches)

## Pull request

## Actions

## Issues

## Gist

#### What is a gists?

Gists provide a simple way to share code snippets with others. Every gist is a Git repository, which means that it can be forked and cloned.

### Creating a gists

You can create two kinds of gists: public and secret. Create a public gist if you're ready to share your ideas with the world or a secret gist if you're not.

1. Sigin to Github
2. Navigate to your gist home page
3. Optionally, in the "Gist description" field, type a description for your gist
4. In the "Filename including extension" field, type a file name for your gist, including the file extensions
5. In the file contents field, type the text of your gist
6. Optionally, to create a public gist, click , then click Create public gist
7. Click Create secret Gist or Create public gist

After creating a gist, you cannot convert it from public to secret.

You'll receive a notification when:

- You are the author of a gist.
- Someone mentions you in a gist.
- You subscribe to a gist, by clicking Subscribe at the top of any gist.

You can pin gists to your profile so other people can see them easily.

**You can discover public gists others have created by going to the gist home page and clicking All Gists.**

## GitHub Pages

## Github Security

### Access permissions on github

#### Personal accounts

A repository owned by a personal account has two permission levels: the repository owner and collaborators.

More information: [Permission levels](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-personal-account-settings/permission-levels-for-a-personal-account-repository)

## CoPilot

## Github Flow

GitHub flow is a lightweight, branch-based workflow.

1. Create a branch
2. Make changes (Create, Edit, Rename, Move, Delete)
3. Commit your changes including a descriptive message
4. Each commit should include and atomic change in your code base
5. Make a separate branch for each set of unrelated changes.
6. Create a Pull request (basically this is a peer review)
7. Address review comments
8. Merge you pull request (changes will appear on the default branch)
9. If the Pull Request has problems go here: [Addressing merge conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts)
10. Delete your branch

## Github Free for personal account

With GitHub Free for personal accounts, you can work with unlimited collaborators on unlimited public repositories with a full feature set, and on unlimited private repositories with a limited feature set.

With GitHub Free, your personal account includes:

- GitHub Community Support
- Dependabot alerts
- Deployment protection rules for public repositories
- Two-factor authentication enforcement
- 500 MB GitHub Packages storage
- 120 GitHub Codespaces core hours per month
- 15 GB GitHub Codespaces storage per month
- GitHub Actions features:
  - 2,000 minutes per month
  - Deployment protection rules for public repositories
