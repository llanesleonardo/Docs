### Splitting a subfolder out into a new repository

If you create a new clone of the repository, you won't lose any of your Git history or changes when you split a folder into a separate repository.

1. Terminal
2. Change the current working directory to the location where you want to create your new repository
3. Clone the repository that contains the subfolder
   $ git clone https://github.com/USERNAME/REPOSITORY-NAME
4. Change the current working directory to your cloned repository.
   $ cd REPOSITORY-NAME
5. To filter the subfolder from the rest of the files in the repository yo should use: [git-filter-repo5](https://github.com/newren/git-filter-repo)
6. Create a new repository on GitHub
7. At the top of your new repository on GitHub.com's Quick Setup page, click to copy the remote repository URL
8. Add a new remote name with the URL you copied for your repository. For example, origin or upstream are two common choices
9. Verify that the remote URL was added with your new repository name
10. Push your changes to the new repository on GitHub.

### Subtree merges

[More about about-git-subtree-merges](https://docs.github.com/en/get-started/using-git/about-git-subtree-merges)

#### Setting up the empty repository for a subtree merge

1. Terminal
2. Create a new directory and navigate to it
3. Initialize a new Git repository
4. Create and commit a new file

#### Adding a new repository as a subtree

1. Add a new remote URL pointing to the separate project that we're interested in
2. Merge the Spoon-Knife project into the local Git project. This doesn't change any of your files locally, but it does prepare Git for the next step
   $ git merge -s ours --no-commit --allow-unrelated-histories spoon-knife/main
   Automatic merge went well; stopped before committing as requested
3. Create a new directory called spoon-knife, and copy the Git history of the Spoon-Knife project into it
   git read-tree --prefix=spoon-knife/ -u spoon-knife/main
4. Commit the changes to keep them safe
   $ git commit -m "Subtree merged in spoon-knife"
   [main fe0ca25] Subtree merged in spoon-knife

Although we've only added one subproject, any number of subprojects can be incorporated into a Git repository.

#### Synchronizing with updates and changes

When a subproject is added, it is not automatically kept in sync with the upstream changes. You will need to update the subproject with the following command:

    $ git pull -s subtree REMOTE-NAME BRANCH-NAME

For the example above, this would be:

    $ git pull -s subtree spoon-knife main
