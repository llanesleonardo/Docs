# Managing your projects

Learn about setting your project to private or public visibility.

Projects can be public or private. For public projects, everyone on the internet can view the project. For private projects, only users granted at least read access can see the project.

Only the project visibility is affected; to view an item on the project, someone must have the required permissions for the repository that the item belongs to. If your project includes items from a private repository, people who are not collaborators in the repository will not be able to view items from that repository.

Project admins and organization owners can control project visibility. Organization owners can restrict the ability to change project visibility to just organization owners.

In public and private projects, insights are only visible to users with write permissions for the project.

In private, organization-owned projects, the avatars of users who are current making updates to the project are displayed in the project UI.

Project admins can also manage write and admin access to their project and control read access for individual users.

## Changing project visibility

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click (screw) Settings to access the project settings.
4. Next to Visibility in the "Danger zone", select Private or Public.

## Managing access to your projects

Learn how to manage team and individual access to your project.

Admins of organization-level projects can manage access for the entire organization, for teams, for individual organization members, and for outside collaborators.

Admins of user-level projects can invite individual collaborators and manage their access.

Project admins can also control the visibility of their project for everyone on the internet.

## Managing access for organization-level projects

You can control access to your project by setting permissions for particular individuals and teams or you can set a base permission that applies to everyone in your organization.

### Managing access for everyone in your organization

You can manage access for everyone in your organization to a particular project by changing the project's base permission. Changes to the base permission only affect organization members who are not organization owners and who are not granted individual access.

You can also configure the default base permission at the organization-level for new projects and projects that haven't yet had a base permission configured.

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click (screw) Settings to access the project settings.
4. Click Manage access.
5. Under Base role, select the default role.
   1. No access: Only organization owners and users granted individual access can see the project. Organization owners are also admins for the project.
   2. Read: Everyone in the organization can see the project. Organization owners are also admins for the project.
   3. Write: Everyone in the organization can see and edit the project. Organization owners are also admins for the project.
   4. Admin: Everyone in the organization is an admin for the project.

## Managing access for teams and individual members of your organization

You can also add teams, external collaborators, and individual organization members as collaborators for an organization-level project.

If you grant a team read permissions or greater for a project, the project is also displayed on the team's projects page. You can also add projects to a team on the team's projects page.

You can only invite an individual user to collaborate on your organization-level project if they are already a member of the organization or an outside collaborator on at least one repository in the organization.

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click (screw) Settings to access the project settings.
4. Click Manage access.
5. Under Invite collaborators, search for the team or individual user that you want to invite.
6. Select the role for the collaborator.
   1. Read: The team or individual can view the project.
   2. Write: The team or individual can view and edit the project.
   3. Admin: The team or individual can view, edit, and add new collaborators to the project.
7. Click Invite.

## Managing access of an existing collaborator on your project

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click (screw icon) Settings to access the project settings.
4. Click Manage access.
5. Under Manage access, find the collaborator(s) whose permissions you want to modify.
6. You can use the Type and Role drop-down menus to filter the access list.
7. Edit the role for the collaborator(s).
8. Optionally, click Remove to remove the collaborator(s).

[Managing access for user level projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/managing-your-project/managing-access-to-your-projects#managing-access-for-user-level-projects)

## Managing project templates in your organization

You can set projects in your organization as templates, allowing other people to select your template as the base for projects they create.

You can set a project as a template to share a pre-configured project with other people in your organization which they can then use as the base for their projects.

The projects you have marked as templates are made available in the "Select a template" pop-up window when other people create projects in your organization.

When someone creates a project from a template, the views, custom fields, and draft issues are copied from the template to the new project.

## Setting a project as a template

If you have admin permissions for a project in your organization, you can set the project as a template and make it available for others in your organization to use.

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click (screw icon) Settings to access the project settings.
4. In the "Templates" section, next to "Make template", select the switch to toggle it to On.

## Finding templates in your organization

You can filter the list of projects in your organization to only show projects set as templates.

1. In the top right corner of GitHub.com, click your profile photo, then click Your organizations.
2. Click the name of your organization.
3. At the top of the screen, click Projects.
4. In the text box above the list of projects, type is:template, and press Enter.

## Copying a project as a template

If you have write or admin permissions for a project in your organization, you can choose to copy the project as a template. This will make a duplicate of the current project, copying the views, custom fields, and draft issues, and set that copied project as a template for your organization.

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click (screw icon) Settings to access the project settings.
4. In the "Templates" section, click Copy as template.

## Closing and deleting your projects

[Closing and deleting your projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/managing-your-project/closing-and-deleting-your-projects)

## Adding your project to a repository

You can add your project to a repository to make it accessible from that repository.

You can list relevant projects in a repository. You can only list projects that are owned by the same user or organization that owns the repository.

In order for repository members to see a project listed in a repository, they must have visibility for the project.

1. On GitHub, navigate to the main page of your repository.
2. Click Projects.
3. Click Add project.
4. In the search bar that appears, search for projects that are owned by the same user or organization that owns the repository.
5. Click on a project to list it in your repository.

## Adding your project to a team

[Adding your project to a team](https://docs.github.com/en/issues/planning-and-tracking-with-projects/managing-your-project/adding-your-project-to-a-team)
