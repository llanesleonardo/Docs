Back: [Table contents](./1-tablecontent.md)

# Releases

You can create a release to package software, along with release notes and links to binary files, for other people to use.

Releases are based on Git tags, which mark a specific point in your repository's history. A tag date may be different than a release date since they can be created at different times.

You can receive notifications when new releases are published in a repository without receiving notifications about other updates to the repository. Anyone with read access to a repository can view and compare releases, but only people with write permissions to a repository can manage releases.

You can manually create release notes while managing a release. Alternatively, you can automatically generate release notes from a default template, or customize your own release notes template.

When viewing the details for a release, the creation date for each release asset is shown next to the release asset.

People with admin permissions to a repository can choose whether Git Large File Storage (Git LFS) objects are included in the ZIP files and tarballs that GitHub creates for each release.

### More information:

- [GitHub Large files](https://docs.github.com/en/repositories/working-with-files/managing-large-files)

If a release fixes a security vulnerability, you should publish a security advisory in your repository. GitHub reviews each published security advisory and may use it to send Dependabot alerts to affected repositories.

You can view the Dependents tab of the dependency graph to see which repositories and packages depend on code in your repository, and may therefore be affected by a new release.

### More information:

- [Video about releases](https://www.youtube.com/watch?v=Ob9llA_QhQY)

ChatPGT definition:

    On GitHub, "Dependents" refers to a feature that shows you which other repositories depend on a specific repository. It allows you to explore the reverse dependencies of a repository and understand its impact on other projects.

    When viewing a repository on GitHub, you can navigate to the "Dependents" tab to see a list of other repositories that have declared a dependency on the current repository. This feature is particularly useful when you maintain a library, package, or framework, as it helps you identify projects that rely on your code.

    Here's what you can typically find in the "Dependents" tab:

    List of Repositories: The "Dependents" tab displays a list of repositories that depend on the current repository. These repositories have explicitly declared a dependency, such as by listing it in their package manifest file (e.g., package.json, requirements.txt, etc.) or using dependency management tools.

    Usage Statistics: Depending on the platform or ecosystem, the "Dependents" tab might provide additional information, such as the number of dependents or usage statistics. This can give you an idea of the popularity and adoption of your code in other projects.

    Explore Dependencies: By exploring the dependents, you can discover projects that rely on your code and explore how your repository fits into the larger ecosystem. It allows you to understand the impact of your work, track downstream users, and potentially collaborate with other developers or projects.

    The "Dependents" feature provides valuable insights for both maintainers and users of libraries or packages. For maintainers, it helps understand the reach and usage of their code, making it easier to prioritize improvements, handle breaking changes, or communicate with the community. For users, it aids in discovering related projects and evaluating the maturity and popularity of a repository before incorporating it into their own projects.

    Note that the "Dependents" feature relies on the dependency information provided by the dependent repositories themselves. It may not capture all dependencies if some projects don't explicitly declare them or use alternative mechanisms for managing dependencies.

You can also use the Releases API to gather information, such as the number of times people download a release asset.

Each file included in a release must be under 2 GB. There is no limit on the total size of a release, nor bandwidth usage.

## Managing releases in a repository

---

### More information:

- [View releases](https://docs.github.com/en/repositories/releasing-projects-on-github/viewing-your-repositorys-releases-and-tags)

You can create releases to bundle and deliver iterations of a project to users.

You can create new releases with release notes, @mentions of contributors, and links to binary files, as well as edit or delete existing releases. You can also create, modify, and delete releases by using the Releases API.

You can also publish an action from a specific release in GitHub Marketplace.

You can choose whether Git Large File Storage (Git LFS) objects are included in the ZIP files and tarballs that GitHub creates for each release.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. To the right of the list of files, click Releases.
3. At the top of the page, click Draft a new release.
4. To choose a tag for the release, select the Choose a tag dropdown menu.
   1. To use an existing tag, click the tag.
   2. To create a new tag, type a version number for your release, then click Create new tag.
5. If you created a new tag, select the Target dropdown menu, then click the branch that contains the project you want to release.
6. Optionally, above the description field, select the Previous tag dropdown menu, then click the tag that identifies the previous release.
7. In the "Release title" field, type a title for your release.
8. In the "Describe this release" field, type a description for your release. If you @mention anyone in the description, the published release will include a Contributors section with an avatar list of all the mentioned users. Alternatively, you can automatically generate your release notes by clicking Generate release notes.
9. Optionally, to include binary files such as compiled programs in your release, drag and drop or manually select files in the binaries box.
10. Optionally, to notify users that the release is not ready for production and may be unstable, select This is a pre-release.
11. Optionally, select Set as latest release. If you do not select this option, the latest release label will automatically be assigned based on semantic versioning.
12. Optionally, if GitHub Discussions is enabled for the repository, create a discussion for the release.
    - Select Create a discussion for this release.
    - Select the Category dropdown menu, then click a category for the release discussion.
13. If you're ready to publicize your release, click Publish release. To work on the release later, click Save draft. You can then view your published or draft releases in the releases feed for your repository. For more information, see "Viewing your repository's releases and tags."

## Create an automated release with github actions

---

### More information:

- [Create an automated release with github actions](https://github.com/marketplace/actions/create-release)

## Edit and Delete a Release

---

### More information:

- [Edit and Delete a Release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository#editing-a-release)

## Searching a repository's releases

---

You can use keywords, tags, and other qualifiers to search for particular releases in a repository.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. To the right of the list of files, click Releases.
3. At the top of the page, in the "Find a release" field, type your query and press Enter.

### More information:

- [Search syntax](https://docs.github.com/en/repositories/releasing-projects-on-github/searching-a-repositorys-releases#search-syntax-for-searching-releases-in-a-repository)

## Linking to releases

---

You can share a link to the latest release for a repository by adding releases/latest to the end of a repository's URL. For example, the URL for the latest release of octo-org/octo-repo on GitHub.com is https://github.com/octo-org/octo-repo/releases/latest.

To link directly to a download of your latest release asset that was manually uploaded, the suffix is /releases/latest/download/asset-name.zip.

## Comparing releases

---

### More information:

- [Comparing releases](https://docs.github.com/en/repositories/releasing-projects-on-github/comparing-releases)
