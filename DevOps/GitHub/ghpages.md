Back: [Table contents](./1-tablecontent.md)

# Github Pages

You can use GitHub Pages to showcase some open source projects, host a blog, or even share your résumé. This guide will help get you started on creating your next website.

GitHub Pages are public webpages hosted and published through GitHub. The quickest way to get up and running is by using the Jekyll Theme Chooser to load a pre-made theme. You can then modify your GitHub Pages' content and style.

This guide will lead you through creating a user site at username.github.io.

## Creating your website

---

### Process' checklist

1. In the upper-right corner of any page, use the + drop-down menu, and select New repository.
2. Enter username.github.io as the repository name. Replace username with your GitHub username. For example, if your username is octocat, the repository name should be octocat.github.io.
3. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings.
4. In the "Code and automation" section of the sidebar, click Pages.
5. Under "Build and deployment", under "Source", select Deploy from a branch.
6. Under "Build and deployment", under "Branch", use the branch dropdown menu and select a publishing source.
7. Optionally, open the README.md file of your repository. The README.md file is where you will write the content for your site. You can edit the file or keep the default content for now.
8. Visit username.github.io to view your new website. Note that it can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub.

## Changing the title and description

---

By default, the title of your site is username.github.io. You can change the title by editing the \_config.yml file in your repository. You can also add a description for your site.

### Process' checklist

1. Click the Code tab of your repository.
2. In the file list, click \_config.yml to open the file.
3. Click to edit the file.
4. The \_config.yml file already contains a line that specifies the theme for your site. Add a new line with title: followed by the title you want. Add a new line with description: followed by the description you want. For example:

```
theme: jekyll-theme-minimal
title: Octocat's homepage
description: Bookmark this to keep an eye on my project updates!
```

5. When you are done editing the file, click Commit changes.

## About GitHub Pages

---

GitHub Pages is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub, optionally runs the files through a build process, and publishes a website.

You can host your site on GitHub's github.io domain or your own custom domain.

You can create GitHub Pages sites that are publicly available on the internet. Organizations that use GitHub Enterprise Cloud can also publish sites privately by managing access control for the site.

Organization owners can disable the publication of GitHub Pages sites from the organization's repositories.

## Types of GitHub Pages sites

---

There are three types of GitHub Pages sites: project, user, and organization. Project sites are connected to a specific project hosted on GitHub, such as a JavaScript library or a recipe collection. User and organization sites are connected to a specific account on GitHub.com.

To publish a user site, you must create a repository owned by your personal account that's named <username>.github.io. To publish an organization site, you must create a repository owned by an organization that's named <organization>.github.io. Unless you're using a custom domain, user and organization sites are available at http(s)://<username>.github.io or http(s)://<organization>.github.io.

The source files for a project site are stored in the same repository as their project. Unless you're using a custom domain, project sites are available at http(s)://<username>.github.io/<repository> or http(s)://<organization>.github.io/<repository>.

You can only create one user or organization site for each account on GitHub. Project sites, whether owned by an organization or a personal account, are unlimited.

## Publishing sources for GitHub Pages sites

---

You can publish your site when changes are pushed to a specific branch, or you can write a GitHub Actions workflow to publish your site.

If you do not need any control over the build process for your site, we recommend that you publish your site when changes are pushed to a specific branch. You can specify which branch and folder to use as your publishing source. The source branch can be any branch in your repository, and the source folder can either be the root of the repository (/) on the source branch or a /docs folder on the source branch. Whenever changes are pushed to the source branch, the changes in the source folder will be published to your GitHub Pages site.

If you want to use a build process other than Jekyll or you do not want a dedicated branch to hold your compiled static files, we recommend that you write a GitHub Actions workflow to publish your site. GitHub provides starter workflows for common publishing scenarios to help you write your workflow.

## Static site generators

---

GitHub Pages publishes any static files that you push to your repository. You can create your own static files or use a static site generator to build your site for you. You can also customize your own build process locally or on another server.

If you use a custom build process or a static site generator other than Jekyll, you can write a GitHub Actions to build and publish your site. GitHub provides starter workflows for several static site generators.

If you publish your site from a source branch, GitHub Pages will use Jekyll to build your site by default. If you want to use a static site generator other than Jekyll, we recommend that you write a GitHub Actions to build and publish your site instead. Otherwise, disable the Jekyll build process by creating an empty file called .nojekyll in the root of your publishing source, then follow your static site generator's instructions to build your site locally.

## Limits on use of GitHub Pages

---

GitHub Pages sites created after June 15, 2016, and using github.io domains are served over HTTPS. If you created your site before June 15, 2016, you can enable HTTPS support for traffic to your site.

## Prohibited uses

---

GitHub Pages is not intended for or allowed to be used as a free web-hosting service to run your online business, e-commerce site, or any other website that is primarily directed at either facilitating commercial transactions or providing commercial software as a service (SaaS). GitHub Pages sites shouldn't be used for sensitive transactions like sending passwords or credit card numbers.

In addition, your use of GitHub Pages is subject to the GitHub Terms of Service, including the restrictions on get-rich-quick schemes, sexually obscene content, and violent or threatening content or activity.

## Usage limits

---

GitHub Pages sites are subject to the following usage limits:

### Process' checklist

1. GitHub Pages source repositories have a recommended limit of 1 GB.
2. Published GitHub Pages sites may be no larger than 1 GB.
3. GitHub Pages deployments will timeout if they take longer than 10 minutes.
4. GitHub Pages sites have a soft bandwidth limit of 100 GB per month.
5. GitHub Pages sites have a soft limit of 10 builds per hour. This limit does not apply if you build and publish your site with a custom GitHub Actions workflow
6. In order to provide consistent quality of service for all GitHub Pages sites, rate limits may apply. These rate limits are not intended to interfere with legitimate uses of GitHub Pages. If your request triggers rate limiting, you will receive an appropriate response with an HTTP status code of 429, along with an informative HTML body.

If your site exceeds these usage quotas, we may not be able to serve your site, or you may receive a polite email from GitHub Support suggesting strategies for reducing your site's impact on our servers, including putting a third-party content distribution network (CDN) in front of your site, making use of other GitHub features such as releases, or moving to a different hosting service that might better fit your needs.

## MIME types on GitHub Pages

---

A MIME type is a header that a server sends to a browser, providing information about the nature and format of the files the browser requested. GitHub Pages supports more than 750 MIME types across thousands of file extensions.

While you can't specify custom MIME types on a per-file or per-repository basis, you can add or modify MIME types for use on GitHub Pages.

## Data collection

---

When a GitHub Pages site is visited, the visitor's IP address is logged and stored for security purposes, regardless of whether the visitor has signed into GitHub or not.

## Configuring a publishing source for your GitHub Pages site

---

You can configure your GitHub Pages site to publish when changes are pushed to a specific branch, or you can write a GitHub Actions workflow to publish your site.

## Publishing from a branch

---

### Process' checklist

1. Make sure the branch you want to use as your publishing source already exists in your repository.
2. On GitHub, navigate to your site's repository.
3. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the ... dropdown menu, then click Settings.
4. In the "Code and automation" section of the sidebar, click Pages.
5. Under "Build and deployment", under "Source", select Deploy from a branch.
6. Under "Build and deployment", use the branch dropdown menu and select a publishing source.
7. Optionally, use the folder dropdown menu to select a folder for your publishing source.
8. Click Save.

## Publishing with a custom GitHub Actions workflow

---

To configure your site to publish with GitHub Actions:

### Process' checklist

1. On GitHub, navigate to your site's repository.
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the ... dropdown menu, then click Settings.
3. In the "Code and automation" section of the sidebar, click Pages.
4. Under "Build and deployment", under "Source", select GitHub Actions.
5. GitHub will suggest several starter workflows. If you already have a workflow to publish your site, you can skip this step. Otherwise, choose one of the options to create a GitHub Actions workflow.

## Creating a custom GitHub Actions workflow to publish your site

---

When you configure your site to publish with GitHub Actions, GitHub will suggest starter workflows for common publishing scenarios. The general flow of a workflow is to:

### Process' checklist

1. Trigger whenever there is a push to the default branch of the repository or whenever the workflow is run manually from the Actions tab.
2. Use the actions/checkout action to check out the repository contents.
3. If required by your site, build any static site files.
4. Use the actions/upload-pages-artifact action to upload the static files as an artifact.
5. If the workflow was triggered by a push to the default branch, use the actions/deploy-pages action to deploy the artifact. This step is skipped if the workflow was triggered by a pull request.

The starter workflows use a deployment environment called github-pages. If your repository does not already include an environment called github-pages, the environment will be created automatically. We recommend that you add an environment protection rule so that only the default branch can deploy to this environment.

## Deleting your site by changing the source

---

### More information

- [Deleting your site by changing the source](https://docs.github.com/en/pages/getting-started-with-github-pages/deleting-a-github-pages-site)

### Process' checklist

1. On GitHub, navigate to your site's repository.
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the ... dropdown menu, then click Settings.
3. In the "Code and automation" section of the sidebar, click Pages.
4. Under "Build and deployment", under "Source", select Deploy from a branch even if the site is currently using GitHub Actions.
5. Under "Build and deployment", use the branch dropdown menu and select None as the publishing source.
6. Click Save.

## Unpublishing a GitHub Pages site

---

You can unpublish your GitHub Pages site so that your current deployment is removed and the site is no longer available. This is different from deleting the site.

When you unpublish your site, your current deployment is removed and the site will no longer be available. Any existing repository settings or content will not be affected.

Unpublishing a site does not permanently delete the site.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under GitHub Pages, next to the Your site is live at message, click ... .
3. In the menu that appears, select Unpublish site.

## Re-enabling a site that has been unpublished

---

Unpublishing your GitHub Pages site removes your current deployment. To make your site available again, you can create a new deployment.

## Re-enable using GitHub Actions

---

A successful workflow run in the repository for your site will create a new deployment. Trigger a workflow run to redeploy your site.

## Re-enabling your site when publishing from a branch

---

### Process' checklist

1. Configure your publishing source to publish from a branch of your choosing.
2. Commit to your publishing source to create a new deployment.

## Creating a custom 404 page for your GHA

---

### More information

- [Creating a custom 404 page for your GHA](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-custom-404-page-for-your-github-pages-site)
- [Resolving problems with mixed content](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https#resolving-problems-with-mixed-content)

## Using submodules with GitHub Pages

---

You can use submodules with GitHub Pages to include other projects in your site's code.

If the repository for your GitHub Pages site contains submodules, their contents will automatically be pulled in when your site is built.

You can only use submodules that point to public repositories, because the GitHub Pages server cannot access private repositories.

Use the https:// read-only URL for your submodules, including nested submodules. You can make this change in your .gitmodules file.
