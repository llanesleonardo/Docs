# Github - Web-based version control system (Use git)

These docs were gathered from various sources, such as:

- [Connecting to github with ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Github users](https://docs.github.com/en/enterprise-cloud@latest/admin/user-management)
- [Github Glossary](https://docs.github.com/en/get-started/quickstart/github-glossary)
- [Free courses](https://docs.github.com/en/get-started/quickstart/git-and-github-learning-resources)

if you need a quick reference you should go here:

[Cheatsheet](https://training.github.com/downloads/es_ES/github-git-cheat-sheet.pdf)

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

## Profile & Managing users

### Collaborators

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

### Following people

You can follow people on GitHub to receive notifications about their activity and discover projects in their communities.

When you follow people, you'll see their public activity on your personal dashboard. If someone you follow stars a public repository, GitHub may recommend the repository to you.

1. Navigate to the user's profile page
2. Under the user's profile picture, click Follow

## Projects

## Repositories

[Repositories](./repositories.md)

## Branches

[Branches](#branches)

### renaming branches

The next code will create a new remote branch after the push command is executed.

    git push REMOTE-NAME LOCAL-BRANCH-NAME:REMOTE-BRANCH-NAME

This pushes the LOCAL-BRANCH-NAME to your REMOTE-NAME, but it is renamed to REMOTE-BRANCH-NAME.

### Delete a branch

The syntax to delete a branch is a bit arcane at first glance:

    git push REMOTE-NAME :BRANCH-NAME

Note that there is a space before the colon. The command resembles the same steps you'd take to rename a branch. However, here, you're telling Git to push nothing into BRANCH-NAME on REMOTE-NAME. Because of this, git push deletes the branch on the remote repository.

## Tags

### Pushing tags

By default, and without additional parameters, git push sends all matching branches that have the same names as remote branches.

To push a single tag, you can issue the same command as pushing a branch:

    git push REMOTE-NAME TAG-NAME

To push all your tags, you can type the command:

    git push REMOTE-NAME --tags

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

### Config Visual Studio for Github

[Associating text editors with git](https://docs.github.com/en/get-started/getting-started-with-git/associating-text-editors-with-git)

### Extensions & integrations

[Exntesions & integrations](https://docs.github.com/en/get-started/exploring-integrations/github-extensions-and-integrations)

### Common errors

- [The SSH agent is not running](https://stackoverflow.com/questions/17846529/could-not-open-a-connection-to-your-authentication-agent)
- [The SSH Agent has not entities](https://stackoverflow.com/questions/26505980/github-permission-denied-ssh-add-agent-has-no-identities)
- [Working with SSH key passphrases](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)
- [Find if your private keys were added to SSH Agent](https://www.freecodecamp.org/news/how-to-manage-multiple-ssh-keys/)
- [Unprotected private key file](https://www.howtogeek.com/168119/fixing-warning-unprotected-private-key-file-on-linux/)
- [Non fast forward Errors](https://docs.github.com/en/get-started/using-git/dealing-with-non-fast-forward-errors)
- [Merge conflict](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)
- [About pull request merges](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges)
- [Cloning repositories](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository#troubleshooting-cloning-errors)
