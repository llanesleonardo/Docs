Back: [Repositories](./repositories.md)

# Repository settings

## Setting repository visibility

---

Organization owners can restrict the ability to change repository visibility to organization owners only.

## Changing a repository's visibility

---

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Danger Zone" section, to the right of to "Change repository visibility", click Change visibility
4. Select a visibility
5. To verify that you're changing the correct repository's visibility, type the name of the repository you want to change the visibility of
6. Click I understand, change repository visibility

## Managing teams and people with access to your repository

---

You can see everyone who has access to your repository and adjust permissions.

## About access management for repositories

---

For each repository that you administer on GitHub, you can see an overview of every team or person with access to the repository. From the overview, you can also invite new teams or people, change each team or person's role for the repository, or remove access to the repository.

This overview can help you audit access to your repository, onboard or off-board contractors or employees, and effectively respond to security incidents.

If a person has been given conflicting access, you'll see a warning on the repository access page. The warning appears with " Mixed roles" next to the person with the conflicting access. To see the source of the conflicting access, hover over the warning icon or click Mixed roles.

## Filtering the list of teams and people

---

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Access" section of the sidebar, click Collaborators & teams
4. Under "Manage access", in the search field, start typing the name of the team or person you'd like to find. Optionally, use the dropdown menus to filter your search

## Changing permissions for a team or person

---

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Access" section of the sidebar, click Collaborators & teams
4. Under "Manage access", next to the team or person whose role you'd like to change, select the Role dropdown menu, and click a new role

## Inviting a team or person

---

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Access" section of the sidebar, click Collaborators & teams
4. To the right of "Manage access", click Add people or Add teams
5. In the search field, start typing the name of the team or person to invite, then click a name in the list of matches
6. Under "Choose a role", select the repository role to grant to the team or person, then click Add NAME to REPOSITORY

To remove acces for a team or person use the same process.

## Managing pull request reviews in your repository

---

You can limit which users can approve or request changes to a pull requests in a public repository.

By default, in public repositories, any user can submit reviews that approve or request changes to a pull request.

You can limit which users are able to submit reviews that approve or request changes to pull requests in your public repository. When you enable code review limits, anyone can comment on pull requests in your public repository, but only people with read access or higher can approve pull requests or request changes.

You can also enable code review limits for an organization. If you enable limits for an organization, you will override any limits for individual repositories owned by the organization.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. Under Access, click Moderation options
4. Under Moderation options, click Code review limits
5. Select or deselect Limit to users explicitly granted read or higher access

## signoff policy

---

### More information:

[signoff policy](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/managing-the-commit-signoff-policy-for-your-repository)

## Managing the push policy for your repository

---

You can limit how many branches and tags can be updated in a single push.
By default, there is no limit to the number of branches and tags that can be updated in a single push.

You can limit the number of branches and tags that can be updated in a single push to block potentially destructive pushes. This can prevent or limit the loss of data.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. Under "Pushes", select Limit how many branches and tags can be updated in a single push
4. After "Up to", type the number of branches and tags you want to limit in a single push. Lower numbers are more restrictive of which pushes are allowed, and higher numbers are less restrictive but have more potential for being destructive

We recommend the default maximum of 5 branch or tag updates allowed in one push. The minimum value is 2, because Git requires two branch updates to rename a branch in a single push: delete branch and create branch

## Enabling or disabling GitHub Discussions for a repository

---

You can use GitHub Discussions in a repository as a place for your community to have conversations, ask questions, and post answers without scoping work in an issue.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings
3. Scroll down to the "Features" section and select Discussions
4. To disable discussions, under "Features", unselect Discussions

You can also use organization discussions to facilitate conversations that span multiple repositories in your organization.

## Configuring ignored files for a single repository

---

You can create a .gitignore file in your repository's root directory to tell Git which files and directories to ignore when you make a commit.

To share the ignore rules with other users who clone the repository, commit the .gitignore file in to your repository.

GitHub maintains an official list of recommended .gitignore files for many popular operating systems, environments, and languages in the github/gitignore public repository. You can also use gitignore.io to create a .gitignore file for your operating system, programming language, or IDE.

## Restoring a deleted repository

---

You can restore some deleted repositories to recover their contents.

It can take up to an hour after a repository is deleted before that repository is available for restoration.

Restoring a repository will not restore release attachments or team permissions. Issues that are restored will not be labeled.

## Restoring a deleted repository that was owned by a personal account

---

### Process' checklist

1. In the upper-right corner of any page, click your profile photo, then click Settings
2. In the "Code planning, and automation" section of the sidebar, click Repositories
3. Under "Repositories", click Deleted repositories
4. Next to the repository you want to restore, click Restore
5. Read the warning, then click I understand, restore this repository

## About email notifications for pushes to your repository

---

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

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings
3. In the "Integrations" section of the sidebar, click Email notifications
4. In the "Address" field, type up to two email addresses, separated by whitespace, where you'd like notifications to be sent. If you'd like to send emails to more than two accounts, set one of the email addresses to a group email address
5. If you operate your own server, you can verify the integrity of emails via the "Approved header." The "Approved header" is a token or secret that you type in this field, and that is sent with the email. If the Approved header of an email matches the token, you can trust that the email is from GitHub
6. Click Setup notifications
