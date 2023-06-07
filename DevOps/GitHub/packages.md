# Github Packages

GitHub Packages is a software package hosting service that allows you to host your software packages privately or publicly and use packages as dependencies in your projects.

[Quickstart for Github Packages](https://docs.github.com/en/packages/quickstart)

GitHub Packages is a platform for hosting and managing packages, including containers and other dependencies. GitHub Packages combines your source code and packages in one place to provide integrated permissions management and billing, so you can centralize your software development on GitHub.

You can integrate GitHub Packages with GitHub APIs, GitHub Actions, and webhooks to create an end-to-end DevOps workflow that includes your code, CI, and deployment solutions.

GitHub Packages offers different package registries for commonly used package managers, such as npm, RubyGems, Apache Maven, Gradle, Docker, and NuGet. GitHub's Container registry is optimized for containers and supports Docker and OCI images.

You can view a package's README, as well as metadata such as licensing, download statistics, version history, and more on GitHub.

## Overview of package permissions

The permissions for a package are either inherited from the repository where the package is hosted, or can be defined for specific users or organizations. Some registries only support permissions inherited from a repository.

## Overview of package visibility

You can publish packages in a public repository (public packages) to share with all of GitHub, or in a private repository (private packages) to share with collaborators or an organization.

## About billing

GitHub Packages usage is free for public packages. For private packages, each account on GitHub.com receives a certain amount of free storage and data transfer, depending on the product used with the account. Any usage beyond the included amounts is controlled by spending limits. If you are a monthly-billed customer, your account will have a default spending limit of 0 US dollars (USD), which prevents additional usage of storage or data transfer after you reach the included amounts. If you pay your account by invoice, your account will have an unlimited default spending limit.

## Supported clients and formats

[Supported clients and formats](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages#supported-clients-and-formats)

## Authenticating to GitHub Packages

You need an access token to publish, install, and delete private, internal, and public packages.

You can use a personal access token (classic) to authenticate to GitHub Packages or the GitHub API. When you create a personal access token (classic), you can assign the token different scopes depending on your needs.

To authenticate to a GitHub Packages registry within a GitHub Actions workflow, you can use:

- GITHUB_TOKEN to publish packages associated with the workflow repository.
- a personal access token (classic) with at least read:packages scope to install packages associated with other private repositories (which GITHUB_TOKEN can't access).

## Managing packages

You can delete a package in the GitHub user interface or using the REST API.

You cannot use the GitHub Packages GraphQL API with registries that support granular permissions.

When you use the GraphQL API to query and delete private packages, you must use the same personal access token (classic) you use to authenticate to GitHub Packages.

You can configure webhooks to subscribe to package-related events, such as when a package is published or updated.

## About permissions for Github Packages

Learn about how to manage permissions for your packages.

[About permissions for Github Packages](https://docs.github.com/en/packages/learn-github-packages/about-permissions-for-github-packages)

## Access control & visibility

[Access control & visibility](https://docs.github.com/en/packages/learn-github-packages/configuring-a-packages-access-control-and-visibility)

## Connecting a repository to a package

You can connect a repository to a package on GitHub.com.

When you publish a package that is scoped to a personal account or an organization, the package is not linked to a repository by default. If you connect a package to a repository, the package's landing page will show information and links from the repository, such as the README. You can also choose to have the package inherit its access permissions from the linked repository.

## Connecting a repository to a user-scoped package on GitHub

1. On GitHub, navigate to the main page of your personal account.
2. In the top right corner of GitHub.com, click your profile photo, then click Your profile.
3. On your profile page, in the header, click the Packages tab.
4. Search for and then click the name of the package that you want to manage.
5. Under your package versions, click Connect repository.
6. Select a repository to link to the package, then click Connect repository.

[organization-scoped package](https://docs.github.com/en/packages/learn-github-packages/connecting-a-repository-to-a-package#connecting-a-repository-to-an-organization-scoped-package-on-github)

[Connecting a repository to a container image using the command line](https://docs.github.com/en/packages/learn-github-packages/connecting-a-repository-to-a-package#connecting-a-repository-to-a-container-image-using-the-command-line)

## Publishing a package

You can publish a package to GitHub Packages to make the package available for others to download and re-use.

You can help people understand and use your package by providing a description and other details like installation and usage instructions on the package page. GitHub provides metadata for each version, such as the publication date, download activity, and recent versions.

You can publish packages in a public repository (public packages) to share with all of GitHub, or in a private repository (private packages) to share with collaborators or an organization. A repository can be connected to more than one package. To prevent confusion, make sure the README and description clearly provide information about each package.

If a new version of a package fixes a security vulnerability, you should publish a security advisory in your repository. GitHub reviews each published security advisory and may use it to send Dependabot alerts to affected repositories.

You can publish a package to GitHub Packages using any supported package client by following the same general guidelines.

1. Create or use an existing personal access token (classic) with the appropriate scopes for the task you want to accomplish. For more information, see "About permissions for GitHub Packages."
2. Authenticate to GitHub Packages using your personal access token (classic) and the instructions for your package client.
3. Publish the package using the instructions for your package client.
   For instructions specific to your package client, see "Working with a GitHub Packages registry."

After you publish a package, you can view the package on GitHub.

## Viewing packages

[Viewing packages](https://docs.github.com/en/packages/learn-github-packages/viewing-packages)

## Installing a package

You can install a package from GitHub Packages and use the package as a dependency in your own project.

You can search on GitHub.com to find packages in GitHub Packages that you can install in your own project.

After you find a package, you can read the package's description and installation and usage instructions on the package page.

## Installing a package

You can install a package from GitHub Packages using any supported package client by following the same general guidelines.

1. Authenticate to GitHub Packages using the instructions for your package client.
2. Install the package using the instructions for your package client.

## Delete and restoring a package

[Delete and restoring a package](https://docs.github.com/en/packages/learn-github-packages/deleting-and-restoring-a-package)

## Container registery

[Container registery](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)

## Working with the npm registry

[Working with the npm registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry)

## Publish & install with actions

[Publish & install with actions](https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/publishing-and-installing-a-package-with-github-actions)

## Packages & Actions

[Packages & Actions](https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/about-github-packages-and-github-actions)
