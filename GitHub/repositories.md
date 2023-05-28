# Repositories

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

### Cloning a repository

You can clone an existing repository from GitHub to your local computer, making it easier to add or remove files, fix merge conflicts, or make complex commits. Cloning a repository pulls down a full copy of all the repository data that GitHub has at that point in time, including all versions of every file and folder for the project.

1. On GitHub.com, navigate to the main page of the repository
2. Above the list of files, click <> Code
3. Copy the URL for the repository (HTTPS - SSH)
4. Open terminal
5. Change the current working directory to the location where you want the cloned directory
6. Type git clone, and then paste the URL you copied earlier
7. Press Enter to create your local clone

This process also works for an empty repository.

### Forking a repository

A fork is a copy of a repository that you manage, where any changes you make will not affect the original repository unless you submit a pull request to the project owner. Most commonly, forks are used to either propose changes to someone else's project or to use someone else's project as a starting point for your own idea.

### Creating remote repositories

You can use the git remote add command to match a remote URL with a name. For example, you'd type the following in the command line:

    git remote add origin <REMOTE_URL>

This associates the name origin with the REMOTE_URL.

You can use the command git remote set-url to change a remote's URL. [Managing remote repositories](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)

More information: [HTTPS URL'S - SSH URL'S](https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories)

### Adding a file to a repository

You can upload and commit an existing file to a repository on GitHub or by using the command line. Files that you add to a repository via a browser are limited to 25 MB per file. You can add larger files, up to 100 MB each, via the command line.

1. On GitHub.com, navigate to the main page of the repository
2. Above the list of files, select the Add file dropdown menu and click Upload files. Alternatively, you can drag and drop files into your browser
3. To select the files you want to upload, drag and drop the file or folder, or click choose your files
4. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message
5. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request
6. Click Propose changes

### Adding a file to a repository using the command line

    $ git add .
    $ git commit -m "Add existing file"
    $ git push origin YOUR_BRANCH

### Verify new remote repository

    $ git remote -v
    # Verify new remote
    origin  https://github.com/OWNER/REPOSITORY.git (fetch)
    origin  https://github.com/OWNER/REPOSITORY.git (push)

### Switching remote URL's from SSH to HTTPS

List your existing remotes in order to get the name of the remote you want to change.

    $ git remote -v
    origin  git@github.com:OWNER/REPOSITORY.git (fetch)
    origin  git@github.com:OWNER/REPOSITORY.git (push)

Change your remote's URL from SSH to HTTPS with the git remote set-url command.

    $ git remote set-url origin https://github.com/OWNER/REPOSITORY.git

Verify that the remote URL has changed.

    $ git remote -v # Verify new remote URL
    origin https://github.com/OWNER/REPOSITORY.git (fetch)
    origin https://github.com/OWNER/REPOSITORY.git (push)

Same process the other way around.

### Renaming a remote repository

    $ git remote rename origin destination
    Change remote name from 'origin' to 'destination'

### Remove a repository

    $ git remote rm destination
    Remove remote

### Fetching changes from a remote repository

Use git fetch to retrieve new work done by other people. Fetching from a repository grabs all the new remote-tracking branches and tags without merging those changes into your own branches.

If you already have a local repository with a remote URL set up for the desired project, you can grab all the new information by using git fetch _remotename_ in the terminal:

    $ git fetch REMOTE-NAME
    # Fetches updates made to a remote repository

### Merging changes into your local branch

Merging combines your local changes with changes made by others.

Typically, you'd merge a remote-tracking branch (i.e., a branch fetched from a remote repository) with your local branch:

    $ git merge REMOTE-NAME/BRANCH-NAME
    # Merges updates made online with your local work

### Pulling changes from a remote repository

git pull is a convenient shortcut for completing both git fetch and git merge in the same command:

    $ git pull REMOTE-NAME BRANCH-NAME
    # Grabs online updates and merges them with your local work

Because pull performs a merge on the retrieved changes, you should ensure that your local work is committed before running the pull command. If you run into a merge conflict you cannot resolve, or if you decide to quit the merge, you can use git merge --abort to take the branch back to where it was in before you pulled.

## Ignoring files

### Configuring ignored files for a single repository

You can create a .gitignore file in your repository's root directory to tell Git which files and directories to ignore when you make a commit.

To share the ignore rules with other users who clone the repository, commit the .gitignore file in to your repository.

GitHub maintains an official list of recommended .gitignore files for many popular operating systems, environments, and languages in the github/gitignore public repository. You can also use gitignore.io to create a .gitignore file for your operating system, programming language, or IDE.

## Restoring a deleted repository

You can restore some deleted repositories to recover their contents.

It can take up to an hour after a repository is deleted before that repository is available for restoration.

Restoring a repository will not restore release attachments or team permissions. Issues that are restored will not be labeled.

### Restoring a deleted repository that was owned by a personal account

1. In the upper-right corner of any page, click your profile photo, then click Settings
2. In the "Code planning, and automation" section of the sidebar, click Repositories
3. Under "Repositories", click Deleted repositories
4. Next to the repository you want to restore, click Restore
5. Read the warning, then click I understand, restore this repository
