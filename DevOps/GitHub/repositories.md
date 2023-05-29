# Repositories

## Create a repository

To start a project on Github, you will ned to create a repository (main object on github).

Every repository needs a license, I am currently studying this topics and you can find them here: [Licenses](https://choosealicense.com/)

Then you have to click the plus icon on the right corner of the main page on Github.

1. Plus sign icon (on the left corner of the page)
2. New repository
3. Repository name (Unique)
4. Add description
5. add README file (optional)
6. Review and finalize the repository creation

## Creating a repository from a template

You can generate a new repository with the same directory structure and files as an existing repository.
Anyone with read permissions to a template repository can create a repository from that template.

You can choose to include the directory structure and files from only the default branch of the template repository or to include all branches. Branches created from a template have unrelated histories, which means you cannot create pull requests or merge between the branches.

Creating a repository from a template is similar to forking a repository, but there are important differences:

- A new fork includes the entire commit history of the parent repository, while a repository created from a template starts with a single commit.
- Commits to a fork don't appear in your contributions graph, while commits to a repository created from a template do appear in your contribution graph.
- A fork can be a temporary way to contribute code to an existing project, while creating a repository from a template starts a new project quickly.

1. On GitHub.com, navigate to the main page of the repository
2. Above the file list, click Use this template
3. Select Create a new repository
4. Use the Owner dropdown menu to select the account you want to own the repository
5. Choose a repository visibility
6. Optionally, to include the directory structure and files from all branches in the template, and not just the default branch, select Include all branches
7. Optionally, if the personal account or organization in which you're creating uses any GitHub Apps from GitHub Marketplace, select any apps you'd like to use in the repository
8. Click Create repository from template

## Creating a template repository

You can make an existing repository a template, so you and others can generate new repositories with the same directory structure, branches, and files.
To create a template repository, you must create a repository, then make the repository a template.

After you make your repository a template, anyone with access to the repository can generate a new repository with the same directory structure and files as your default branch. They can also choose to include all the other branches in your repository. Branches created from a template have unrelated histories, so you cannot create pull requests or merge between the branches.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. Select Template repository

## Creating an issues-only repository

GitHub does not provide issues-only access permissions, but you can accomplish this using a second repository which contains only the issues.

1. Create a private repository to host the source code from your project
2. reate a second repository with the permissions you desire to host the issue tracker
3. Add a README file to the issues repository explaining the purpose of this repository and linking to the issues section
4. Set your collaborators or teams to give access to the repositories as you desire

Users with write access to both can reference and close issues back and forth across the repositories, but those without the required permissions will see references that contain a minimum of information.

For example, if you pushed a commit to the private repository's default branch with a message that read Fixes organization/public-repo#12, the issue would be closed, but only users with the proper permissions would see the cross-repository reference indicating the commit that closed the issue. Without the permissions, a reference still appears, but the details are omitted.

## First Commit

A commit is like a snapshot of all the files in your project at a particular point in time.

### **Terminal**

    git add .
    git commit -m "first commit"
    git push origin main

these commands are making a "commit" to the default branch, if you want to create a branch you should go here: [branches](branches)

After a commit you should create a "Pull Request". [Pull Request](pull_request)

### Graphic interface

1. Edit README file
2. Make some changes to the file
3. Preview the changes you made to the file
4. Commit changes
5. Create a Pull Request

### About README's

You can add a README file to your repository to tell other people why your project is useful, what they can do with your project, and how they can use it.

A README is often the first item a visitor will see when visiting your repository. README files typically include information on:

- What the project does
- Why the project is useful
- How users can get started with the project
- Where users can get help with your project
- Who maintains and contributes to the project

If you put your README file in your repository's hidden .github, root, or docs directory, GitHub will recognize and automatically surface your README to repository visitors.

For the rendered view of any Markdown file in a repository, including README files, GitHub will automatically generate a table of contents based on section headings. You can view the table of contents for a README file by clicking the menu icon at the top left of the rendered page.

You can link directly to a section in a rendered file by hovering over the section heading to expose .

You can define relative links and image paths in your rendered files to help readers navigate to other files in your repository.

A relative link is a link that is relative to the current file. For example, if you have a README file in root of your repository, and you have another file in docs/CONTRIBUTING.md, the relative link to CONTRIBUTING.md in your README might look like this:

    [Contribution guidelines for this project](docs/CONTRIBUTING.md)

GitHub will automatically transform your relative link or image path based on whatever branch you're currently on, so that the link or path always works. The path of the link will be relative to the current file. Links starting with / will be relative to the repository root. You can use all relative link operands, such as ./ and ../

Relative links are easier for users who clone your repository. Absolute links may not work in clones of your repository - we recommend using relative links to refer to other files within your repository.

## Cloning a repository

You can clone an existing repository from GitHub to your local computer, making it easier to add or remove files, fix merge conflicts, or make complex commits. Cloning a repository pulls down a full copy of all the repository data that GitHub has at that point in time, including all versions of every file and folder for the project.

1. On GitHub.com, navigate to the main page of the repository
2. Above the list of files, click <> Code
3. Copy the URL for the repository (HTTPS - SSH)
4. Open terminal
5. Change the current working directory to the location where you want the cloned directory
6. Type git clone, and then paste the URL you copied earlier
7. Press Enter to create your local clone

This process also works for an empty repository.

## Forking a repository

A fork is a copy of a repository that you manage, where any changes you make will not affect the original repository unless you submit a pull request to the project owner. Most commonly, forks are used to either propose changes to someone else's project or to use someone else's project as a starting point for your own idea.

## Creating remote repositories

You can use the git remote add command to match a remote URL with a name. For example, you'd type the following in the command line:

    git remote add origin <REMOTE_URL>

This associates the name origin with the REMOTE_URL.

You can use the command git remote set-url to change a remote's URL. [Managing remote repositories](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)

More information: [HTTPS URL'S - SSH URL'S](https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories)

## Adding a file to a repository

[Managing files](./workingfiles.md)

## Verify new remote repository

    $ git remote -v
    # Verify new remote
    origin  https://github.com/OWNER/REPOSITORY.git (fetch)
    origin  https://github.com/OWNER/REPOSITORY.git (push)

## Switching remote URL's from SSH to HTTPS

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

## Renaming a remote repository

    $ git remote rename origin destination
    Change remote name from 'origin' to 'destination'

## Remove a repository

    $ git remote rm destination
    Remove remote

## Fetching changes from a remote repository

Use git fetch to retrieve new work done by other people. Fetching from a repository grabs all the new remote-tracking branches and tags without merging those changes into your own branches.

If you already have a local repository with a remote URL set up for the desired project, you can grab all the new information by using git fetch _remotename_ in the terminal:

    $ git fetch REMOTE-NAME
    # Fetches updates made to a remote repository

## Merging changes into your local branch

Merging combines your local changes with changes made by others.

Typically, you'd merge a remote-tracking branch (i.e., a branch fetched from a remote repository) with your local branch:

    $ git merge REMOTE-NAME/BRANCH-NAME
    # Merges updates made online with your local work

## Pulling changes from a remote repository

git pull is a convenient shortcut for completing both git fetch and git merge in the same command:

    $ git pull REMOTE-NAME BRANCH-NAME
    # Grabs online updates and merges them with your local work

Because pull performs a merge on the retrieved changes, you should ensure that your local work is committed before running the pull command. If you run into a merge conflict you cannot resolve, or if you decide to quit the merge, you can use git merge --abort to take the branch back to where it was in before you pulled.

## Managing repository settings

You can choose the way your repository functions by managing repository settings.

### Setting repository visibility

Organization owners can restrict the ability to change repository visibility to organization owners only.

#### Changing a repository's visibility

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Danger Zone" section, to the right of to "Change repository visibility", click Change visibility
4. Select a visibility
5. To verify that you're changing the correct repository's visibility, type the name of the repository you want to change the visibility of
6. Click I understand, change repository visibility

## Managing teams and people with access to your repository

You can see everyone who has access to your repository and adjust permissions.

### About access management for repositories

For each repository that you administer on GitHub, you can see an overview of every team or person with access to the repository. From the overview, you can also invite new teams or people, change each team or person's role for the repository, or remove access to the repository.

This overview can help you audit access to your repository, onboard or off-board contractors or employees, and effectively respond to security incidents.

If a person has been given conflicting access, you'll see a warning on the repository access page. The warning appears with " Mixed roles" next to the person with the conflicting access. To see the source of the conflicting access, hover over the warning icon or click Mixed roles.

### Filtering the list of teams and people

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Access" section of the sidebar, click Collaborators & teams
4. Under "Manage access", in the search field, start typing the name of the team or person you'd like to find. Optionally, use the dropdown menus to filter your search

### Changing permissions for a team or person

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Access" section of the sidebar, click Collaborators & teams
4. Under "Manage access", next to the team or person whose role you'd like to change, select the Role dropdown menu, and click a new role

### Inviting a team or person

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Access" section of the sidebar, click Collaborators & teams
4. To the right of "Manage access", click Add people or Add teams
5. In the search field, start typing the name of the team or person to invite, then click a name in the list of matches
6. Under "Choose a role", select the repository role to grant to the team or person, then click Add NAME to REPOSITORY

To remove acces for a team or person use the same process.

## Managing pull request reviews in your repository

You can limit which users can approve or request changes to a pull requests in a public repository.

By default, in public repositories, any user can submit reviews that approve or request changes to a pull request.

You can limit which users are able to submit reviews that approve or request changes to pull requests in your public repository. When you enable code review limits, anyone can comment on pull requests in your public repository, but only people with read access or higher can approve pull requests or request changes.

You can also enable code review limits for an organization. If you enable limits for an organization, you will override any limits for individual repositories owned by the organization.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. Under Access, click Moderation options
4. Under Moderation options, click Code review limits
5. Select or deselect Limit to users explicitly granted read or higher access

## signoff policy

[signoff policy](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/managing-the-commit-signoff-policy-for-your-repository)

## Managing the push policy for your repository

You can limit how many branches and tags can be updated in a single push.
By default, there is no limit to the number of branches and tags that can be updated in a single push.

You can limit the number of branches and tags that can be updated in a single push to block potentially destructive pushes. This can prevent or limit the loss of data.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. Under "Pushes", select Limit how many branches and tags can be updated in a single push
4. After "Up to", type the number of branches and tags you want to limit in a single push. Lower numbers are more restrictive of which pushes are allowed, and higher numbers are less restrictive but have more potential for being destructive

We recommend the default maximum of 5 branch or tag updates allowed in one push. The minimum value is 2, because Git requires two branch updates to rename a branch in a single push: delete branch and create branch

## Enabling or disabling GitHub Discussions for a repository

You can use GitHub Discussions in a repository as a place for your community to have conversations, ask questions, and post answers without scoping work in an issue.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings
3. Scroll down to the "Features" section and select Discussions
4. To disable discussions, under "Features", unselect Discussions

You can also use organization discussions to facilitate conversations that span multiple repositories in your organization.

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

## About email notifications for pushes to your repository

You can choose to automatically send email notifications to a specific email address when anyone pushes to the repository.

Each email notification for a push to a repository lists the new commits and links to a diff containing just those commits. In the email notification you'll see:

- The name of the repository where the commit was made
- The branch a commit was made in
- The SHA1 of the commit, including a link to the diff in GitHub
- The author of the commit
- The date when the commit was made
- The files that were changed as part of the commit
- The commit message

You can filter email notifications you receive for pushes to a repository.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Integrations" section of the sidebar, click Email notifications
4. In the "Address" field, type up to two email addresses, separated by whitespace, where you'd like notifications to be sent. If you'd like to send emails to more than two accounts, set one of the email addresses to a group email address
5. If you operate your own server, you can verify the integrity of emails via the "Approved header." The "Approved header" is a token or secret that you type in this field, and that is sent with the email. If the Approved header of an email matches the token, you can trust that the email is from GitHub
6. Click Setup notifications

## Classifying your repository with topics

To help other people find and contribute to your project, you can add topics to your repository related to your project's intended purpose, subject area, affinity groups, or other important qualities.

With topics, you can explore repositories in a particular subject area, find projects to contribute to, and discover new solutions to a specific problem. Topics appear on the main page of a repository. You can click a topic name to see related topics and a list of other repositories classified with that topic.

To browse the most used topics, go to https://github.com/topics/.

You can contribute to GitHub's set of featured topics in the github/explore repository.

Repository admins can add any topics they'd like to a repository. Helpful topics to classify a repository include the repository's intended purpose, subject area, community, or language. Additionally, GitHub analyzes public repository content and generates suggested topics that repository admins can accept or reject. Private repository content is not analyzed and does not receive topic suggestions.

Public and private repositories can have topics, although you will only see private repositories that you have access to in topic search results.

When creating a topic:

- use lowercase letters, numbers, and hyphens.
- use 50 characters or less.
- add no more than 20 topics.

### Adding topics to your repository

1. On GitHub.com, navigate to the main page of the repository
2. In the top right corner of the page, to the right of "About", click
3. Under "Topics", start to type the topic you want to add to your repository to display a dropdown menu of any matching topics. Click the topic you want to add or continue typing to create a new topic
4. Optional, if there are "Suggested" topics displayed under the "Topics" field, click to add or to decline the suggested topic
5. After you've finished adding topics, click Save changes

## Configuring tag protection rules

You can configure tag protection rules for your repository to prevent contributors from creating or deleting tags.

When you add a tag protection rule, all tags that match the pattern provided will be protected. Only users with admin or maintain permissions, or custom roles with the "edit repository rules" permission in the repository will be able to create protected tags, and only users with admin permissions or custom roles with the "edit repository rules" permission in the repository will be able to delete protected tags. GitHub Apps require the Repository administration: write permission to modify a protected tag.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings.
3. In the "Code and automation" section of the sidebar, click Tags
4. Click New rule
5. Under "Tag name pattern", type the pattern of the tags you want to protect. In this example, typing "\*" protects all tags
6. Click Add rule

## Managing GitHub Actions settings for a repository

You can disable or configure GitHub Actions for a specific repository.
By default, GitHub Actions is enabled on all repositories and organizations. You can choose to disable GitHub Actions or limit it to actions and reusable workflows in your organization.

You can enable GitHub Actions for your repository. When you enable GitHub Actions, workflows are able to run actions and reusable workflows located within your repository and any other public repository. You can disable GitHub Actions for your repository altogether. When you disable GitHub Actions, no workflows run in your repository.

Alternatively, you can enable GitHub Actions in your repository but limit the actions and reusable workflows a workflow can run.

You can disable GitHub Actions for a repository, or set a policy that configures which actions and reusable workflows can be used in the repository.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the left sidebar, click Actions, then click General
4. Under "Actions permissions", select an option
5. Click Save

[Specific selection of workflows](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#allowing-select-actions-and-reusable-workflows-to-run)

[GitHub Token](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#setting-the-permissions-of-the-github_token-for-your-repository)

[Retention period for artifacts](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#configuring-the-retention-period-for-github-actions-artifacts-and-logs-in-your-repository)

## Customizing your repository's social media preview

You can customize the image displayed on social media platforms when someone links to your repository.

Until you add an image, repository links expand to show basic information about the repository and the owner's avatar. Adding an image to your repository can help identify your project across various social platforms.

You can upload an image to a public repository, or to a private repository to which you have previously uploaded an image. Your image can only be shared from a public repository.
Tip: Your image should be a PNG, JPG, or GIF file under 1 MB in size. For the best quality rendering, we recommend keeping the image at 640 by 320 pixels.

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. Under "Social preview," click Edit
   1. To add a new image, click Upload an image....
   2. To remove an image, click Remove image

## About code owners

You can use a CODEOWNERS file to define individuals or teams that are responsible for code in a repository.

People with admin or owner permissions can set up a CODEOWNERS file in a repository.

The people you choose as code owners must have write permissions for the repository. When the code owner is a team, that team must be visible and it must have write permissions, even if all the individual members of the team already have write permissions directly, through organization membership, or through another team membership.

Code owners are automatically requested for review when someone opens a pull request that modifies code that they own. Code owners are not automatically requested to review draft pull requests.
When you mark a draft pull request as ready for review, code owners are automatically notified. If you convert a pull request to a draft, people who are already subscribed to notifications are not automatically unsubscribed.

When someone with admin or owner permissions has enabled required reviews, they also can optionally require approval from a code owner before the author can merge a pull request in the repository.

If a file has a code owner, you can see who the code owner is before you open a pull request. In the repository, you can browse to the file and hover over to see a tool tip with codeownership details.

[Specify more than one codeowner](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#codeowners-file-location)

[codeowner syntax](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#codeowners-syntax)

A CODEOWNERS file uses a pattern that follows most of the same rules used in gitignore files. The pattern is followed by one or more GitHub usernames or team names using the standard @username or @org/team-name format. Users and teams must have explicit write access to the repository, even if the team's members already have access.

If you want to match two or more code owners with the same pattern, all the code owners must be on the same line. If the code owners are not on the same line, the pattern matches only the last mentioned code owner.

[Example of codeowner file](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#example-of-a-codeowners-file)
