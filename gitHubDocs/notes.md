# Github - Web-based version control system (Use git)

These docs were gathered from various sources, such as:

- [connecting to github with ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

## SSH Keys

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

## Profile & Users

## Projects

## Repositories

## Pull request

## Actions

## Issues

## GitHub Pages

## CoPilot
