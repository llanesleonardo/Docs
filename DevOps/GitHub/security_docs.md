# Github Security

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

## Managing security and analysis settings for your repository

You can control features that secure and analyze the code in your project on GitHub.

You can manage a subset of security and analysis features for public repositories. Other features are permanently enabled, including dependency graph and secret scanning alerts for partners.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Security" section of the sidebar, click Code security and analysis
4. Under "Code security and analysis", to the right of the feature, click Disable or Enable

## Granting access to security alerts

Security alerts for a repository are visible to people with admin access to the repository and, when the repository is owned by an organization, organization owners. You can give additional teams and people access to the alerts.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Security" section of the sidebar, click Code security and analysis
4. Under "Access to alerts", in the search field, start typing the name of the person or team you'd like to find, then click a name in the list of matches
5. Click Save changes

This process also works for disabiling access to security alerts.

## Access permissions on github

## Important security considerations using forks

[Important security considerations using forks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-permissions-and-visibility-of-forks#important-security-considerations)
