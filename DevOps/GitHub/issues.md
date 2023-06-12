Back: [Table contents](./1-tablecontent.md)

# Github Issues

Use GitHub Issues to track ideas, feedback, tasks, or bugs for work on GitHub.

Issues let you track your work on GitHub, where development happens. When you mention an issue in another issue or pull request, the issue's timeline reflects the cross-reference so that you can keep track of related work. To indicate that work is in progress, you can link an issue to a pull request. When the pull request merges, the linked issue automatically closes.

## Quickly create issues

---

Issues can be created in a variety of ways, so you can choose the most convenient method for your workflow. For example, you can create an issue from a repository, an item in a task list, a note in a project, a comment in an issue or pull request, a specific line of code, or a URL query. You can also create an issue from your platform of choice: through the web UI, GitHub Desktop, GitHub CLI, GraphQL and REST APIs, or GitHub Mobile.

### More information:

- [Quick start for Github issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/quickstart)

## Track work (issues, tasklist, labels, milestones)

---

You can organize and prioritize issues with projects. To track issues as part of a larger issue, you can use task lists. To categorize related issues, you can use labels and milestones.

## Stay up to date

---

To stay updated on the most recent comments in an issue, you can subscribe to an issue to receive notifications about the latest comments. To quickly find links to recently updated issues you're subscribed to, visit your dashboard.

## Community management

---

To help contributors open meaningful issues that provide the information that you need, you can use issue forms and issue templates.

## Efficient communication

---

You can @mention collaborators who have access to your repository in an issue to draw their attention to a comment. To link related issues in the same repository, you can type # followed by part of the issue title and then clicking the issue that you want to link. To communicate responsibility, you can assign issues. If you find yourself frequently typing the same comment, you can use saved replies.

## Comparing issues and discussions

---

Some conversations are more suitable for GitHub Discussions. You can use GitHub Discussions to ask and answer questions, share information, make announcements, and conduct or participate in conversations about a project.

## Create an issue

---

Issues can be created in a variety of ways, so you can choose the most convenient method for your workflow.

Issues can be used to keep track of bugs, enhancements, or other requests.

Repository administrators can disable issues for a repository.

## Creating an issue from a repository

---

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues.
3. Click New issue.
4. If your repository uses issue templates, next to the type of issue you'd like to open, click Get started. If the type of issue you'd like to open isn't included in the available options, click Open a blank issue.
5. In the "Title" field, type a title for your issue.
6. In the comment body field, type a description of your issue.
7. If you're a project maintainer, you can assign the issue to someone, add it to a project board, associate it with a milestone, or apply a label.
8. When you're finished, click Submit new issue.

## Creating an issue from a comment

---

You can open a new issue from a comment in an issue or pull request. When you open an issue from a comment, the issue contains a snippet showing where the comment was originally posted.

### Process' checklist

1. Navigate to the comment that you would like to open an issue from.
2. In that comment, click "..." .
3. Click Reference in new issue.
4. Use the "Repository" dropdown menu, and select the repository you want to open the issue in.
5. Type a descriptive title and body for the issue.
6. Click Create issue.
7. If you're a project maintainer, you can assign the issue to someone, add it to a project board, associate it with a milestone, or apply a label.
8. When you're finished, click Submit new issue.

## Creating an issue from code

---

### More information:

- [Creating an issue from code](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue#creating-an-issue-from-code)
- [Creating an issue from discussions](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue#creating-an-issue-from-discussion)

## Creating an issue from a project

---

You can quickly create issues without leaving your project. When using a view that is grouped by a field, creating an issue in that group will automatically set the new issue's field to the group's value. For example, if you group your view by "Status", when you create an issue in the "Todo" group, the new issue's "Status" will automatically be set to "Todo."

### Process' checklist

1. Navigate to your project.
2. At the bottom of a table, group of items, or a column in board layout, click.
3. Click Create new issue.
4. At the top of the "Create new issue" dialog, select the repository where you want the new issue to be created.
5. Below the repository dropdown, type a title for the new issue.
6. Optionally, use the fields below the title field to set assignees, labels, and milestones, and add the new issue to other projects.
7. Optionally, type a description for your issue.
8. Optionally, if you want to create more issues, select Create more and the dialog will reopen when you create your issue.
9. Click Create.

## Creating an issue from a classic project note

---

If you're using a classic project to track and prioritize your work, you can convert notes to issues.

## Creating an issue from a task list item

---

Within an issue, you can use task lists to break work into smaller tasks and track the full set of work to completion. If a task requires further tracking or discussion, you can convert the task to an issue by hovering over the task and clicking in the upper-right corner of the task.

## Creating an issue from a URL query

---

You can use query parameters to open issues. Query parameters are optional parts of a URL you can customize to share a specific web page view, such as search filter results or an issue template on GitHub. To create your own query parameters, you must match the key and value pair.

Tip: You can also create issue templates that open with default labels, assignees, and an issue title.

You must have the proper permissions for any action to use the equivalent query parameter. For example, you must have permission to add a label to an issue to use the labels query parameter.

If you create an invalid URL using query parameters, or if you don’t have the proper permissions, the URL will return a 404 Not Found error page. If you create a URL that exceeds the server limit, the URL will return a 414 URI Too Long error page.

### More information:

- [Creating an issue from a URL Query](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue#creating-an-issue-from-a-url-query)

## Tasklists

---

You can use tasklists to divide your issues into smaller subtasks.

Tasklists add support for hierarchies of issues on GitHub, helping you to keep track of your issues, divide your issues into smaller subtasks, and create new relationships between your issues.

Tasklists build upon the previous iteration of beta task lists, retaining the ability to convert items into issues, display the progress of a tasklist, and create a "tracks/tracked by" relationship between issues.

The issues you add to your tasklists will be automatically populated to show their assignees and any labels applied.

Your project's side-panel displays an issue's place in the hierarchy on a breadcrumb menu, allowing you to navigate through the issues included in your tasklists. You can also add the Tracks and Tracked by fields to your project views to quickly see the relationships between your issues.

## Creating tasklists with Markdown

---

You can create a tasklist using Markdown in the issue description (the opening comment of an issue). You can include links to issues and pull requests or create draft issues.

### Process' checklist

1. Start creating a new issue or edit the issue description of an existing issue.
2. To begin your tasklist, type ```[tasklist] (triple backticks and tasklist inside square brackets) on a new line in the issue description.
3. Optionally, type ### TITLE on the next line, replacing TITLE with a title for your tasklist.
4. For each item you want to add to your tasklist, type - [ ] on a new line, followed by a space, and either a link to an issue, a link to a pull request, or some text to create a draft issue.
   You must provide a full link to an issue or pull request. For example, https://github.com/octo-org/octo-repo/issues/45.
   Tasks can be formatted with Markdown.
   Tasks must not exceed 256 characters in length.
5. To finish your tasklist, type ` on a new line after the last item.

Your finished tasklist should look like this:

```

[tasklist]
### My tasks
- [ ] https://github.com/octo-org/octo-repo/issues/45
- [ ] Draft issue title
```

Your tasklist will be rendered by GitHub when you save the issue. You can then make changes and add issues and draft issues using the GitHub UI. If you edit the issue description, you will be able to modify the Markdown directly or copy the Markdown to duplicate the tasklist in other issues.

You can also click in the formatting toolbar to insert a tasklist when creating a new issue or editing an issue description.

## Adding issues to a tasklist

---

### Process' checklist

1. At the bottom of your tasklist, click Add item to Tasks.
2. Select the issue to add to your tasklist.

- To add a recently updated issue from the repository, click the issue in the dropdown, or use your arrow keys to select it and then press Enter.
- To search for an issue in the repository, start typing the title of an issue or the issue's number and click on the result, or use your arrow keys to select it and press Enter.
- To add an issue directly using its URL, paste the URL of an issue and press Enter.

## Creating draft issues in a tasklist

---

Draft issues are useful to quickly capture ideas that you can later convert into issues. Unlike issues and pull requests that are referenced from your repositories, draft issues exist only in your tasklist.

### Process' checklist

1. At the bottom of your tasklist, click Add item to Tasks.
2. In the "Type to add an item or paste in an issue URL" field, type your draft issue title and press Enter.

### More information:

- [Converting draft issues to issues in a tasklist](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-tasklists#converting-draft-issues-to-issues-in-a-tasklist)
- [Removing an issue or draft issue from a tasklist](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-tasklists#removing-an-issue-or-draft-issue-from-a-tasklist)

## Changing the title of a tasklist

---

When you create a new tasklist, the default title is "Tasks." You can modify the title by editing the issue's markdown.

### Process' checklist

1. In the top-right of the issue body, select and click Edit.
2. In the fenced code block that starts with ```[tasklist], add a header with your new title, such as ## My new title. [Changing the title of a tasklist](https://docs.github.com/assets/cb-20174/mw-1440/images/help/issues/edit-tasklist-title.webp)
3. Click Update comment.

## Copying a tasklist

---

When you copy your tasklist using the "Copy Markdown" option, GitHub copies Markdown to your clipboard and includes the Issue's name so you can paste the tasklist outside of GitHub without losing context.

### Process' checklist

1. In the top-right of your tasklist, click .
2. In the menu, click Copy markdown.

### More information

- [Slash commands](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-slash-commands)

## Linking a pull request to an issue

---

You can link a pull request or branch to an issue to show that a fix is in progress and to automatically close the issue when the pull request or branch is merged.

You can link an issue to a pull request manually or using a supported keyword in the pull request description.

When you link a pull request to the issue the pull request addresses, collaborators can see that someone is working on the issue.

When you merge a linked pull request into the default branch of a repository, its linked issue is automatically closed.

## Linking a pull request to an issue using a keyword

---

You can link a pull request to an issue by using a supported keyword in the pull request's description or in a commit message. The pull request must be on the default branch.

- close
- closes
- closed
- fix
- fixes
- fixed
- resolve
- resolves
- resolved

If you use a keyword to reference a pull request comment in another pull request, the pull requests will be linked. Merging the referencing pull request also closes the referenced pull request.

The syntax for closing keywords depends on whether the issue is in the same repository as the pull request.

### More information:

- [Linking a pull request to an issue using a keyword](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword)

## Manually linking a pull request to an issue using the pull request sidebar

---

Anyone with write permissions to a repository can manually link a pull request to an issue from the pull request sidebar.

You can manually link up to ten issues to each pull request. The issue and pull request must be in the same repository.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Pull requests.
3. In the list of pull requests, click the pull request that you'd like to link to an issue.
4. In the right sidebar, click Development.
5. Click the issue you want to link to the pull request.

## Manually linking a pull request or branch to an issue using the issue sidebar

---

Anyone with write permissions to a repository can manually link a pull request or branch to an issue from the issue sidebar.

You can manually link up to ten issues to each pull request. The issue can be in a different repository than the linked pull request or branch. Your last selected repository will be remembered.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues.
3. In the list of issues, click the issue that you'd like to link a pull request or branch to.
4. In the right sidebar, click Development.
5. Click the repository containing the pull request or branch you want to link to the issue.
6. Click the pull request or branch you want to link to the issue.
7. Click Apply.

## Creating a branch to work on an issue

---

You can create a branch to work on an issue directly from the issue page and get started right away.

Branches connected to an issue are shown under the "Development" section in the sidebar of an issue. When you create a pull request for one of these branches, it is automatically linked to the issue. The connection with that branch is removed and only the pull request is shown in the "Development" section.

## Creating a branch for an issue

---

Anyone with write permission to a repository can create a branch for an issue. You can link multiple branches for an issue.

By default, the new branch is created in the current repository, and from the default branch.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues.
3. In the list of issues, click the issue that you would like to create a branch for.
4. In the right sidebar under "Development", click Create a branch. If the issue already has a linked branch or pull request, select and click Create a branch.
5. Optionally, in the "Branch name" field, type a branch name.
6. Optionally, select the Repository destination dropdown menu, then choose a repository.
7. Under "What's next", select whether you want to work on the branch locally or to open the branch in GitHub Desktop.
8. Click Create branch.

## Assigning issues and pull requests to other GitHub users

---

Assignees clarify who is working on specific issues and pull requests.

You can assign multiple people to each issue or pull request, including yourself, anyone who has commented on the issue or pull request, anyone with write permissions to the repository, and organization members with read permissions to the repository.

Issues and pull requests in public repositories, and in private repositories for a paid account, can have up to 10 people assigned. Private repositories on the free plan are limited to one person per issue or pull request.

## Assigning an individual issue or pull request

---

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues or Pull requests.
3. Open the issue or pull request that you want to assign to someone.
4. In the right side menu, click Assignees.
5. To assign the issue or pull request to a user, start typing their username, then click their name when it appears. You can select and add up to ten assignees to an issue or pull request.

## Assigning multiple issues or pull requests

---

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues or Pull requests.
3. Select the items you want to assign to someone.
4. In the upper-right corner, click Assign.
5. To assign the items to a user, start typing their username, then click their name when it appears. You can select and add up to ten assignees to an issue or pull request.

### More information:

- [Viewing all of your issues and pull requests](https://docs.github.com/en/issues/tracking-your-work-with-issues/viewing-all-of-your-issues-and-pull-requests)

## Marking issues or pull requests as a duplicate

---

Mark an issue or pull request as a duplicate to track similar issues or pull requests together and remove unnecessary burden for both maintainers and collaborators.

For a "marked as duplicate" timeline event to appear, the user who creates the duplicate reference comment must have write access to the repository where they create the comment.

## Marking duplicates

---

To mark an issue or pull request as a duplicate, type "Duplicate of" followed by an issue or pull request number in the body of a new comment.

You can also use the GitHub-provided saved replies, "Duplicate issue" or "Duplicate pull request."

## Unmarking duplicates

---

You can unmark duplicate issues and pull requests by clicking Undo in the timeline. This will add a new timeline event, indicating that the issue or pull request was unmarked.

## Pinning an issue to your repository

You can pin up to three important issues above the issues list in your repository.

Who can use this feature
People with write access to a repository can pin issue in the repository.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues.
3. In the list of issues, click the issue you'd like to pin
4. In the right sidebar, click Pin issue.

## Transferring an issue to another repository

---

### More information:

- [Transferring an issue to another repository](https://docs.github.com/en/issues/tracking-your-work-with-issues/transferring-an-issue-to-another-repository)

## Closing an issue

---

You can close an issue when bugs are fixed, feedback is acted on, or to show that work is not planned.
Repository owners, collaborators on repositories owned by a personal account, and people with triage permissions or greater on repositories owned by an organization can close issues opened by others.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues.
3. In the list of issues, click the issue you'd like to close.
4. Optionally, to change your reason for closing the issue, next to "Close issue," select , then click a reason.
5. Click Close issue.
