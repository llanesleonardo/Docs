# Projects

Projects is an adaptable, flexible tool for planning and tracking work on GitHub.

A project is an adaptable spreadsheet that integrates with your issues and pull requests on GitHub to help you plan and track your work effectively. You can create and customize multiple views by filtering, sorting, grouping your issues and pull requests, visualize work with configurable charts, and add custom fields to track metadata specific to your team. Rather than enforcing a specific methodology, a project provides flexible features you can customize to your team’s needs and processes.

Your projects are built from the issues and pull requests you add, creating direct references between your project and your work. Information is synced automatically to your project as you make changes, updating your views and charts. This integration works both ways, so that when you change information about a pull request or issue in your project, the pull request or issue reflects that information. For example, change an assignee in your project and that change is shown in your issue. You can take this integration even further, group your project by assignee, and make changes to issue assignment by dragging issues into the different groups.

[Quickstart for Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects)

[Planning and tracking for developers](https://www.youtube.com/watch?v=DuAyYsWbt5o)

## Adding metadata to your items

You can use custom fields to add metadata to your issues, pull requests, and draft issues and build a richer view of item attributes. You’re not limited to the built-in metadata (assignee, milestone, labels, etc.) that currently exists for issues and pull requests. For example, you can add the following metadata as custom fields:

- A date field to track target ship dates.
- A number field to track the complexity of a task.
- A single select field to track whether a task is Low, Medium, or High priority.
- A text field to add a quick note.
- An iteration field to plan work week-by-week, including support for breaks.

## Automating your projects

There are a number of ways you can add automation to your project. Built-in workflows allow you to automatically set fields when items are added or changed, and you can also configure your project to automatically archive items when they meet certain criteria and automatically add items from a repository when they match set criteria.

You can also use the GraphQL API and GitHub Actions to take even greater control of your project.

## Exploring the relationships between issues

You can use tasklists to build hierarchies of issues, dividing your issues into smaller subtasks, and creating new relationships between your issues.

These relationships are displayed on the issue, as well as the Tracked by and Tracks fields in your projects. You can filter by issues which are tracked by another issue, and you can also group your table views by the Tracked by field to show all parent issues with a list of their subtasks.

## Viewing your project from different perspectives

Quickly answer your most pressing questions by tailoring your project view to give you the information you need. You can save these views, allowing you to quickly return to them as needed and make them available to your team. Views not only let you scope down the items listed but also offer two different layout options.

You can view your project as a high-density table layout, as a kanban board, or a timeline-style roadmap.

## Best practices for Projects

Learn tips for managing your projects.
You can use Projects to manage your work on GitHub, where your issues and pull requests live. Read on for tips to manage your projects efficiently and effectively.

Break down large issues into smaller issues
Breaking a large issue into smaller issues makes the work more manageable and enables team members to work in parallel. It also leads to smaller pull requests, which are easier to review.

To track how smaller issues fit into the larger goal, use task lists, milestones, or labels.

## Communicate

Issues and pull requests include built-in features to let you easily communicate with your collaborators. Use @mentions to alert a person or entire team about a comment. Assign collaborators to issues to communicate responsibility. Link to related issues or pull requests to communicate how they are connected.

## Make use of the description and README

Use your project's description and README to share information about the project.

For example:

- Explaining the purpose of the project.
- Describing the project views and how to use them.
- Including relevant links and people to contact for more information.

Project READMEs support Markdown which allows you to use images and advanced formatting such as links, lists, and headers.

## Use views

Use project views to look at your project from different angles.

For example:

- Filter by status to view all un-started items
- Group by a custom priority field to monitor the volume of high priority items
- Sort by a custom date field to view the items with the earliest target ship date

## Have a single source of truth

To prevent information from getting out of sync, maintain a single source of truth. For example, track a target ship date in a single location instead of spread across multiple fields. Then, if the target ship date shifts, you only need to update the date in one location.

Projects automatically stay up to date with GitHub data, such as assignees, milestones, and labels. When one of these fields changes in an issue or pull request, the change is automatically reflected in your project.

## Use automation

You can automate tasks to spend less time on busy work and more time on the project itself. The less you need to remember to do manually, the more likely your project will stay up to date.

Projects offers built-in workflows. For example, when an issue is closed, you can automatically set the status to "Done." You can also configure built-in workflows to automatically archive items when they meet certain criteria and to automatically add items from a repository when they match a filter.

Additionally, GitHub Actions and the GraphQL API enable you to automate routine project management tasks. For example, to keep track of pull requests awaiting review, you can create a workflow that adds a pull request to a project and sets the status to "needs review"; this process can be automatically triggered when a pull request is marked as "ready for review."

## Use different field types

Take advantage of the various field types to meet your needs.

Use an iteration field to schedule work or create a timeline. You can group by iteration to see if items are balanced between iterations, or you can filter to focus on a single iteration. Iteration fields also let you view work that you completed in past iterations, which can help with velocity planning and reflecting on your team's accomplishments. Iteration fields also support breaks to show when you and your team are taking time away from their iterations.

Use a single select field to track information about a task based on a preset list of values. For example, track priority or project phase. Since the values are selected from a preset list, you can easily group or filter to focus on items with a specific value.

## Creating a project

Learn how to create an organization or user project.

Projects are an adaptable collection of items that stay up-to-date with GitHub data. Your projects can track issues, pull requests, and ideas that you note down. You can add custom fields and create views for specific purposes.

You can also choose to use an existing project as a template and copy the views and custom fields to a new project.

### Creating an organization project

Organization projects can track issues and pull requests from the organization's repositories. You can also set projects in your organization as templates that other organization members can then use as the base for the projects they create.

1. In the top right corner of GitHub.com, click your profile photo, then click Your organizations.
2. Click the name of your organization.
3. Under your organization name, click Projects.
4. Click New project.
5. Optionally, in the text box under "Project name", type a name for your new project.
6. Click a built-in template, a template from your organization or, to start with an empty project, click Table or Board.
7. Click Create.

### Creating a user project

User projects can track issues and pull requests from the repositories owned by your personal account.

1. In the top right corner of GitHub.com, click your profile photo, then click Your profile.
2. On your profile, click Projects.
3. Click New project.
4. Optionally, in the text box under "Project name", type a name for your new project.
5. Click a template or, to start with an empty project, click Table or Board.
6. Click Create.

## Updating your project description and README

You can set your project's description and README to share the purpose of your project, provide instructions on how to use the project, and include any relevant links.

1. Navigate to your project.
2. In the top-right, click to open the menu.
3. In the menu, click Settings to access the project settings.
4. To add a short description to your project, under "Add a description", type your description in the text box and click Save.
5. To update your project's README, under "README", type your content in the text box.
   1. You can format your README using Markdown. For more information, see "Basic writing and formatting syntax."
   2. To toggle between the text box and a preview of your changes, click or .
6. To save changes to your README, click Save.

You can view and make quick changes to your project description and README by navigating to your project and clicking in the top right.

## Copying an existing project

You can use an existing project as a template by copying it.

You can copy an existing project and use it as a template to save time configuring your views and custom fields.

When you copy a project, the new project will contain the same views and custom fields. You also have the option to copy existing draft issues. The new project will not contain the original project's items, workflows, insights, collaborators, or team and repository links.

You can also set projects in your organization as templates that other organization members can then use as the base for the projects they create.

1. Navigate to the project you want to copy.
2. In the top-right, click to open the menu.
3. In the menu, click Make a copy.
4. Optionally, if you want all draft issues to be copied with the project, in the "Make a copy" dialog, select Draft issues will be copied if selected.
5. Under "Owner", select either the organization that will own the new project or your personal account.
6. Under "New project name", type the name of the new project.
7. Click Copy project.

## Migrating from projects (classic)

[Migrating from projects (classic)](https://docs.github.com/en/issues/planning-and-tracking-with-projects/creating-projects/migrating-from-projects-classic)
