Back: [Github Pages](./ghpages.md)

# Github Pages and Jekyll

Jekyll is a static site generator with built-in support for GitHub Pages.

Jekyll is a static site generator with built-in support for GitHub Pages and a simplified build process. Jekyll takes Markdown and HTML files and creates a complete static website based on your choice of layouts. Jekyll supports Markdown and Liquid, a templating language that loads dynamic content on your site.

Jekyll is not officially supported for Windows.

We recommend using Jekyll with GitHub Pages. If you prefer, you can use other static site generators or customize your own build process locally or on another server.

## Configuring Jekyll in your GitHub Pages site

---

You can configure most Jekyll settings, such as your site's theme and plugins, by editing your \_config.yml file.

Some configuration settings cannot be changed for GitHub Pages sites.

```
lsi: false
safe: true
source: [your repo's top level directory]
incremental: false
highlighter: rouge
gist:
  noscript: false
kramdown:
  math_engine: mathjax
  syntax_highlighter: rouge
```

By default, Jekyll doesn't build files or folders that:

- are located in a folder called /node_modules or /vendor
- start with \_, ., or #
- end with ~
- are excluded by the exclude setting in your configuration file

If you want Jekyll to process any of these files, you can use the include setting in your configuration file.

## Front matter

---

To set variables and metadata, such as a title and layout, for a page or post on your site, you can add YAML front matter to the top of any Markdown or HTML file.

### More information

- [Front Matter](https://jekyllrb.com/docs/front-matter/)

## Themes

---

You can add a Jekyll theme to your GitHub Pages site to customize the look and feel of your site.

You can add a supported theme to your site on GitHub.

To use any other open source Jekyll theme hosted on GitHub, you can add the theme manually.

You can override any of your theme's defaults by editing the theme's files.

## Plugins

---

You can download or create Jekyll plugins to extend the functionality of Jekyll for your site. For example, the jemoji plugin lets you use GitHub-flavored emoji in any page on your site the same way you would on GitHub. For more information, see "Plugins" in the Jekyll documentation.

GitHub Pages uses plugins that are enabled by default and cannot be disabled:

- jekyll-coffeescript
- jekyll-default-layout
- jekyll-gist
- jekyll-github-metadata
- jekyll-optional-front-matter
- jekyll-paginate
- jekyll-readme-index
- jekyll-titles-from-headings
- jekyll-relative-links

You can enable additional plugins by adding the plugin's gem to the plugins setting in your \_config.yml file.

For a list of supported plugins, see "Dependency versions" on the GitHub Pages site.

### More information

- [Dependency versions](https://pages.github.com/versions/)

GitHub Pages cannot build sites using unsupported plugins. If you want to use unsupported plugins, generate your site locally and then push your site's static files to GitHub.

## Syntax highlighting

---

To make your site easier to read, code snippets are highlighted on GitHub Pages sites the same way they're highlighted on GitHub.

By default, code blocks on your site will be highlighted by Jekyll. Jekyll uses the Rouge highlighter, which is compatible with Pygments. Pygments has been deprecated and not supported in Jekyll 4. If you specify Pygments in your \_config.yml file, Rouge will be used as the fallback instead. Jekyll cannot use any other syntax highlighter, and you'll get a page build warning if you specify another syntax highlighter in your \_config.yml file.

If you want to use another highlighter, such as highlight.js, you must disable Jekyll's syntax highlighting by updating your project's \_config.yml file.

```
kramdown:
  syntax_highlighter_opts:
    disable : true
```

If your theme doesn't include CSS for syntax highlighting, you can generate GitHub's syntax highlighting CSS and add it to your project's style.css file.

```
$ rougify style github > style.css

```

## Building your site locally

---

If you are publishing from a branch, changes to your site are published automatically when the changes are merged into your site's publishing source. If you are publishing from a custom GitHub Actions workflow, changes are published whenever your workflow is triggered (typically by a push to the default branch). If you want to preview your changes first, you can make the changes locally instead of on GitHub. Then, test your site locally.

## Creating a GitHub Pages site with Jekyll

---

You can use Jekyll to create a GitHub Pages site in a new or existing repository.

## Prerequisites

---

Before you can use Jekyll to create a GitHub Pages site, you must install Jekyll and Git.

We recommend using Bundler to install and run Jekyll. Bundler manages Ruby gem dependencies, reduces Jekyll build errors, and prevents environment-related bugs. To install [Bundler](https://bundler.io/):

### Process' checklist

1. Install Ruby. For more information, see "Installing Ruby" in the Ruby documentation.
2. Install Bundler.

## Creating a repository for your site

---

You can either create a repository or choose an existing repository for your site.

If you want to create a GitHub Pages site for a repository where not all of the files in the repository are related to the site, you will be able to configure a publishing source for your site. For example, you can have a dedicated branch and folder to hold your site source files, or you can use a custom GitHub Actions workflow to build and deploy your site source files.

If the account that owns the repository uses GitHub Free or GitHub Free for organizations, the repository must be public.

If you want to create a site in an existing repository, skip to the "Creating your site" section.

### Process' checklist

1. In the upper-right corner of any page, use the drop-down menu, and select New repository.
2. Use the Owner dropdown menu to select the account you want to own the repository.
3. Type a name for your repository and an optional description. If you're creating a user or organization site, your repository must be named <user>.github.io or <organization>.github.io. If your user or organization name contains uppercase letters, you must lowercase the letters.
4. Choose a repository visibility.

## Creating your site

---

Before you can create your site, you must have a repository for your site on GitHub.

### Process' checklist

1. Open Git Bash.
2. If you don't already have a local copy of your repository, navigate to the location where you want to store your site's source files, replacing PARENT-FOLDER with the folder you want to contain the folder for your repository.

```
$ cd PARENT-FOLDER

```

3. If you haven't already, initialize a local Git repository, replacing REPOSITORY-NAME with the name of your repository.

```
$ git init REPOSITORY-NAME
> Initialized empty Git repository in /Users/octocat/my-site/.git/
# Creates a new folder on your computer, initialized as a Git repository
```

4. Change directories to the repository.

```
$ cd REPOSITORY-NAME
# Changes the working directory
```

5. Decide which publishing source you want to use.
6. Navigate to the publishing source for your site. For example, if you chose to publish your site from the docs folder on the default branch, create and change directories to the docs folder.

```
$ mkdir docs
# Creates a new folder called docs
$ cd docs
```

If you chose to publish your site from the gh-pages branch, create and checkout the gh-pages branch.

```
$ git checkout --orphan gh-pages
# Creates a new branch, with no history or contents, called gh-pages, and switches to the gh-pages branch
$ git rm -rf .
# Removes the contents from your default branch from the working directory
```

7. To create a new Jekyll site, use the jekyll new command:

```
$ jekyll new --skip-bundle .
```

8. Open the Gemfile that Jekyll created.
9. Add "#" to the beginning of the line that starts with gem "jekyll" to comment out this line.
10. Add the github-pages gem by editing the line starting with # gem "github-pages". Change this line to:

```
gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
```

Replace GITHUB-PAGES-VERSION with the latest supported version of the github-pages gem. You can find this version here: "Dependency versions."

The correct version Jekyll will be installed as a dependency of the github-pages gem.

11. Save and close the Gemfile.
12. From the command line, run bundle install.
13. Optionally, make any necessary edits to the \_config.yml file. This is required for relative paths when the repository is hosted in a subdirectory.
14. Optionally, test your site locally.
15. Add and commit your work.

```
git add .
git commit -m 'Initial GitHub pages site with Jekyll'
```

16. Add your repository on GitHub.com as a remote, replacing USER with the account that owns the repository and REPOSITORY with the name of the repository.

```
$ git remote add origin https://github.com/USER/REPOSITORY.git

```

17. Push the repository to GitHub, replacing BRANCH with the name of the branch you're working on.

```
$ git push -u origin BRANCH

```

18. Configure your publishing source.
19. On GitHub, navigate to your site's repository.
20. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings.
21. In the "Code and automation" section of the sidebar, click Pages.
22. To see your published site, under "GitHub Pages", click Visit site.
23. Your GitHub Pages site is built and deployed with a GitHub Actions workflow.

You can add a Jekyll theme to your GitHub Pages site to customize the look and feel of your site.

## Testing your GitHub Pages site locally with Jekyll

---

You can build your GitHub Pages site locally to preview and test changes to your site.

Anyone with read permissions for a repository can test a GitHub Pages site locally.

## Prerequisites

---

Before you can use Jekyll to test a site, you must:

- Install Jekyll.
- Create a Jekyll site.

We recommend using Bundler to install and run Jekyll. Bundler manages Ruby gem dependencies, reduces Jekyll build errors, and prevents environment-related bugs. To install Bundler:

- Install Ruby.
- Install Bundler.

## Building your site locally

---

### Process' checklist

1. Open Git Bash.
2. Navigate to the publishing source for your site.
3. Run bundle install.
4. Run your Jekyll site locally.

```
$ bundle exec jekyll serve
> Configuration file: /Users/octocat/my-site/_config.yml
>            Source: /Users/octocat/my-site
>       Destination: /Users/octocat/my-site/_site
> Incremental build: disabled. Enable with --incremental
>      Generating...
>                    done in 0.309 seconds.
> Auto-regeneration: enabled for '/Users/octocat/my-site'
> Configuration file: /Users/octocat/my-site/_config.yml
>    Server address: http://127.0.0.1:4000/
>  Server running... press ctrl-c to stop.
```

5. To preview your site, in your web browser, navigate to http://localhost:4000.

## Updating the GitHub Pages gem

---

Jekyll is an active open source project that is updated frequently. If the github-pages gem on your computer is out of date with the github-pages gem on the GitHub Pages server, your site may look different when built locally than when published on GitHub. To avoid this, regularly update the github-pages gem on your computer.

### Process' checklist

1. Open Git Bash.
2. Update the github-pages gem.
   - If you installed Bundler, run bundle update github-pages.
   - If you don't have Bundler installed, run gem update github-pages.

## Adding content to your GitHub Pages site using Jekyll

---

You can add a new page or post to your Jekyll site on GitHub Pages.

Before you can add content to a Jekyll site on GitHub Pages, you must create a Jekyll site.

The main types of content for Jekyll sites are pages and posts. A page is for standalone content that isn't associated with a specific date, such as an "About" page. The default Jekyll site contains a file called about.md, which renders as a page on your site at YOUR-SITE-URL/about. You can edit the contents of that file to personalize your "About" page, and you can use the "About" page as a template to create new pages.

A post is a blog post. The default Jekyll site contains a directory named \_posts that contains a default post file. You can edit the contents of that post, and you can use the default post as a template to create new posts.

Your theme includes default layouts, includes, and stylesheets that will automatically be applied to new pages and posts on your site, but you can override any of these defaults.

To set variables and metadata, such as a title and layout, for a page or post on your site, you can add YAML front matter to the top of any Markdown or HTML file. F

If you are publishing from a branch, changes to your site are published automatically when the changes are merged into your site's publishing source. If you are publishing from a custom GitHub Actions workflow, changes are published whenever your workflow is triggered (typically by a push to the default branch). If you want to preview your changes first, you can make the changes locally instead of on GitHub. T

## Adding a new page to your site

---

### Process' checklist

1. On GitHub, navigate to your site's repository.
2. Navigate to the publishing source for your site.
3. In the root of your publishing source, create a new file for your page called PAGE-NAME.md, replacing PAGE-NAME with a meaningful filename for the page.
4. Add the following YAML frontmatter to the top of the file, replacing PAGE-TITLE with the page's title and URL-PATH with a path you want for the page's URL. For example, if the base URL of your site is https://octocat.github.io and your URL-PATH is /about/contact/, your page will be located at https://octocat.github.io/about/contact.

```
layout: page
title: "PAGE-TITLE"
permalink: /URL-PATH
```

5. Below the frontmatter, add content for your page.
6. Click Commit changes...
7. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message.
8. If you have more than one email address associated with your account on GitHub.com, click the email address drop-down menu and select the email address to use as the Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then <username>@users.noreply.github.com is the default commit author email address.
9. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request.
10. Click Commit changes or Propose changes.
11. Create a pull request for your proposed changes.
12. In the "Pull Requests" list, click the pull request you would like to merge.
13. Click Merge pull request.
14. If prompted, type a commit message, or accept the default message.
15. Click Confirm merge.
16. Optionally, delete the branch.

## Adding a new post to your site

---

### Process' checklist

1. On GitHub, navigate to your site's repository.
2. Navigate to the publishing source for your site.
3. Navigate to the \_posts directory.
4. Create a new file called YYYY-MM-DD-NAME-OF-POST.md, replacing YYYY-MM-DD with the date of your post and NAME-OF-POST with the name of your post.
5. Add the following YAML frontmatter to the top of the file, including the post's title enclosed in quotation marks, the date and time for the post in YYYY-MM-DD hh:mm:ss -0000 format, and as many categories as you want for your post.

```
layout: post
title: "POST-TITLE"
date: YYYY-MM-DD hh:mm:ss -0000
categories: CATEGORY-1 CATEGORY-2
```

6. Below the frontmatter, add content for your post.
7. Click Commit changes...
8. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message.
9. If you have more than one email address associated with your account on GitHub.com, click the email address drop-down menu and select the email address to use as the Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then <username>@users.noreply.github.com is the default commit author email address.
10. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request.
11. Click Commit changes or Propose changes.
12. Create a pull request for your proposed changes.
13. In the "Pull Requests" list, click the pull request you would like to merge.
14. Click Merge pull request.
15. If prompted, type a commit message, or accept the default message.
16. Click Confirm merge.
17. Optionally, delete the branch.

Your post should now be up on your site! If the base URL of your site is https://octocat.github.io, then your new post will be located at https://octocat.github.io/YYYY/MM/DD/TITLE.html.

## Setting a Markdown processor for your GitHub Pages site using Jekyll

---

You can choose a Markdown processor to determine how Markdown is rendered on your GitHub Pages site.

People with write permissions for a repository can set the Markdown processor for a GitHub Pages site.

GitHub Pages supports two Markdown processors: kramdown and GitHub's own Markdown processor, which is used to render GitHub Flavored Markdown (GFM) throughout GitHub.

You can use GitHub Flavored Markdown with either processor, but only our GFM processor will always match the results you see on GitHub.

### Process' checklist

1. On GitHub, navigate to your site's repository.
2. In your repository, browse to the \_config.yml file.
3. In the upper right corner of the file view, click (edit icon) to open the file editor.
4. Find the line that starts with markdown: and change the value to kramdown or GFM. The full line should read markdown: kramdown or markdown: GFM.
5. Click Commit changes...
6. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message.
7. If you have more than one email address associated with your account on GitHub.com, click the email address drop-down menu and select the email address to use as the Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then <username>@users.noreply.github.com is the default commit author email address.
8. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request.
9. Click Commit changes or Propose changes.

## Adding a theme to your GitHub Pages site using Jekyll

---

You can personalize your Jekyll site by adding and customizing a theme.

## Adding a theme

### Process' checklist

1. On GitHub, navigate to your site's repository.
2. Navigate to the publishing source for your site.
3. Navigate to \_config.yml.
4. In the upper right corner of the file view, click (edit icon) to open the file editor.
5. Add a new line to the file for the theme name.

- To use a supported theme, type theme: THEME-NAME, replacing THEME-NAME with the name of the theme as shown in the README of the theme's repository. For a list of supported themes, see "Supported themes" on the GitHub Pages site. For example, to select the Minima theme, type theme: minima.
- To use any other Jekyll theme hosted on GitHub, type remote_theme: THEME-NAME, replacing THEME-NAME with the name of the theme as shown in the README of the theme's repository. [Supported themes](https://pages.github.com/themes/)

6. Click Commit changes...
7. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message.
8. If you have more than one email address associated with your account on GitHub.com, click the email address drop-down menu and select the email address to use as the Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then <username>@users.noreply.github.com is the default commit author email address.
9. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request.
10. Click Commit changes or Propose changes.

## Customizing your theme's CSS

---

These instructions work best with themes that are officially supported by GitHub Pages. For a complete list of supported themes, see "Supported themes" on the GitHub Pages site.

Your theme's source repository may offer some help in customizing your theme. For example, see Minima's README.

1. On GitHub, navigate to your site's repository.
2. Navigate to the publishing source for your site. For more information, see "Configuring a publishing source for your GitHub Pages site."
3. Create a new file called /assets/css/style.scss.
4. Add the following content to the top of the file:

```
---
---

@import "{{ site.theme }}";
```

5. Add any custom CSS or Sass (including imports) you'd like immediately after the @import line.

## Customizing your theme's HTML layout

---

These instructions work best with themes that are officially supported by GitHub Pages. For a complete list of supported themes, see "Supported themes" on the GitHub Pages site.

Your theme's source repository may offer some help in customizing your theme. For example, see Minima's README.

1. On GitHub, navigate to your theme's source repository. For example, the source repository for Minima is https://github.com/jekyll/minima.
2. In the \_layouts folder, navigate to your theme's default.html file.
3. Copy the contents of the file.
4. On GitHub, navigate to your site's repository.
5. Navigate to the publishing source for your site. For more information, see "Configuring a publishing source for your GitHub Pages site."
6. Create a file called \_layouts/default.html.
7. Paste the default layout content you copied earlier.
8. Customize the layout as you'd like.

## About custom domains and GitHub Pages

---

GitHub Pages supports using custom domains, or changing the root of your site's URL from the default, like octocat.github.io, to any domain you own.

GitHub Pages works with two types of domains: subdomains and apex domains.

You can set up either or both of apex and www subdomain configurations for your site.

We recommend always using a www subdomain, even if you also use an apex domain. When you create a new site with an apex domain, we automatically attempt to secure the www subdomain for use when serving your site's content, but you need to make the DNS changes to use the www subdomain. If you configure a www subdomain, we automatically attempt to secure the associated apex domain.

After you configure a custom domain for a user or organization site, the custom domain will replace the <user>.github.io or <organization>.github.io portion of the URL for any project sites owned by the account that are published publicly and do not have a custom domain configured. For example, if the custom domain for your user site is www.octocat.com, and you have a project site with no custom domain configured that is published from a repository called octo-project, the GitHub Pages site for that repository will be available at www.octocat.com/octo-project.

## Using a subdomain for your GitHub Pages site

---

A subdomain is the part of a URL before the root domain. You can configure your subdomain as www or as a distinct section of your site, like blog.example.com.

Subdomains are configured with a CNAME record through your DNS provider.

## www subdomains

---

A www subdomain is the most commonly used type of subdomain. For example, www.example.com includes a www subdomain.

www subdomains are the most stable type of custom domain because www subdomains are not affected by changes to the IP addresses of GitHub's servers.

## Custom subdomains

---

A custom subdomain is a type of subdomain that doesn't use the standard www variant. Custom subdomains are mostly used when you want two distinct sections of your site. For example, you can create a site called blog.example.com and customize that section independently from www.example.com.

## Using an apex domain for your GitHub Pages site

---

An apex domain is a custom domain that does not contain a subdomain, such as example.com. Apex domains are also known as base, bare, naked, root apex, or zone apex domains.

An apex domain is configured with an A, ALIAS, or ANAME record through your DNS provider.

If you are using an apex domain as your custom domain, we recommend also setting up a www subdomain. If you configure the correct records for each domain type through your DNS provider, GitHub Pages will automatically create redirects between the domains. For example, if you configure www.example.com as the custom domain for your site, and you have GitHub Pages DNS records set up for the apex and www domains, then example.com will redirect to www.example.com. Note that automatic redirects only apply to the www subdomain. Automatic redirects do not apply to any other subdomains, such as blog.

## Securing the custom domain for your GitHub Pages site

---

If your GitHub Pages site is disabled but has a custom domain set up, it is at risk of a domain takeover. Having a custom domain configured with your DNS provider while your site is disabled could result in someone else hosting a site on one of your subdomains.

Verifying your custom domain prevents other GitHub users from using your domain with their repositories. If your domain is not verified, and your GitHub Pages site is disabled, you should immediately update or remove your DNS records with your DNS provider.

There are a couple of reasons your site might be automatically disabled.

- If you downgrade from GitHub Pro to GitHub Free, any GitHub Pages sites that are currently published from private repositories in your account will be unpublished.
- If you transfer a private repository to a personal account that is using GitHub Free, the repository will lose access to the GitHub Pages feature, and the currently published GitHub Pages site will be unpublished.

## Managing a custom domain for your Github pages site

---

### More information

- [Managing a custom domain for your Github pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

## Verifying your custom domain for Github Pages

---

### More information

- [Verifying your custom domain for Github Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)
