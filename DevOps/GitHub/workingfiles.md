Back: [Repositories](./repositories.md)

# Managing files

## Creating new files

---

You can create new files directly on GitHub in any repository you have write access to.

When creating a file on GitHub, consider the following:

- If you try to create a new file in a repository that you don’t have access to, we will fork the project to your personal account and help you send a pull request to the original repository after you commit your change.
- File names created via the web interface can only contain alphanumeric characters and hyphens (-). To use other characters, create and commit the files locally, then push them to the repository on GitHub.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. In your repository, browse to the folder where you want to create a file
3. Above the list of files, select the Add file dropdown menu, then click Create new file
4. In the file name field, type the name and extension for the file. To create subdirectories, type the / directory separator
5. In the file contents text box, type content for the file
6. To review the new content, above the file contents, click Preview
7. Click Commit changes..
8. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message
9. If you have more than one email address associated with your account on GitHub.com, click the email address drop-down menu and select the email address to use as the Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then <username>@users.noreply.github.com is the default commit author email address. For more information, see "Setting your commit email address."
10. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request
11. Click Commit changes or Propose changes

## Removing sensitive data from a repository

---

Never git add, commit, or push sensitive information to a remote repository. Sensitive information can include, but is not limited to:

- Passwords
- SSH keys
- AWS access keys
- API keys
- Credit card numbers
- PIN numbers

### More information:

- [Removing senstiive data](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

## Adding a file to a repository

---

You can upload and commit an existing file to a repository on GitHub or by using the command line. Files that you add to a repository via a browser are limited to 25 MB per file. You can add larger files, up to 100 MB each, via the command line.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository
2. Above the list of files, select the Add file dropdown menu and click Upload files. Alternatively, you can drag and drop files into your browser
3. To select the files you want to upload, drag and drop the file or folder, or click choose your files
4. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message
5. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request
6. Click Propose changes

## Adding a file to a repository using the command line

---

```
    $ git add .
    $ git commit -m "Add existing file"
    $ git push origin YOUR_BRANCH
```

## Viewing a file

---

You can view raw file content or trace changes to lines in a file and discover how parts of the file evolved over time.

With the raw view, you can view or copy the raw content of a file without any styling.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Click the file that you want to view.
3. In the upper-right corner of the file view, click Raw.
4. Optionally, to copy the raw file content, in the upper-right corner of the file view, click . To download the raw file, click

### More information:

- [Blame View](https://docs.github.com/en/repositories/working-with-files/using-files/viewing-a-file#viewing-the-line-by-line-revision-history-for-a-file)

## Moving a file to a new location

---

You can move a file to a different directory on GitHub or by using the command line.

### Process' checklist

1. In your repository, browse to the file you want to move
2. In the upper right corner of the file view, click to open the file editor
3. In the filename field, change the name of the file using these guidelines:
   1. To move the file into a subfolder, type the name of the folder you want, followed by /. Your new folder name becomes a new item in the navigation breadcrumbs
   2. To move the file into a directory above the file's current location, place your cursor at the beginning of the filename field, then either type ../ to jump up one full directory level, or type the backspace key to edit the parent folder's name
4. Click Commit changes..
5. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file.
6. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch.
7. Click Commit changes or Propose changes

### More information:

- [Use command line to a file to a new location](https://docs.github.com/en/repositories/working-with-files/managing-files/moving-a-file-to-a-new-location)

This process can also be use to rename a file.

## Editing files

---

You can edit files directly on GitHub in any of your repositories using the file editor.

### Process' checklist

1. In your repository, browse to the file you want to edit
2. In the upper right corner of the file view, click to open the file editor
3. In the text box, make any changes you need to the file
4. Above the new content, click Preview
5. Click Commit changes...
6. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file.
7. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch.
8. Click Commit changes or Propose changes

## Deleting files in a repository

---

You can delete an individual file or an entire directory in your repository on GitHub.

You can delete an individual file in your repository or an entire directory, including all the files in the directory.

If you try to delete a file or directory in a repository that you don’t have write permissions to, we'll fork the project to your personal account and help you send a pull request to the original repository after you commit your change.

If the file or directory you deleted contains sensitive data, the data will still be available in the repository's Git history. To completely remove the file from GitHub, you must remove the file from your repository's history.

## Deleting a file

---

### Process' checklist

1. Browse to the file in your repository that you want to delete
2. In the top-right corner, select the dropdown menu, then click Delete file
3. In the "Commit message" field, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message
4. If you have more than one email address associated with your account on GitHub.com, click the email address drop-down menu and select the email address to use as the Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then <username>@users.noreply.github.com is the default commit author email address. For more information, see "Setting your commit email address."
5. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request
6. Click Commit changes or Propose changes

This process will work for deleting a directory, the only change that we have to apply is choose the option "Delete directory" in the dropdown menu.

## Navigating code on GitHub

---

You can understand the relationships within and across repositories by navigating code directly in GitHub.

Code navigation helps you to read, navigate, and understand code by showing and linking definitions of a named entity corresponding to a reference to that entity, as well as references corresponding to an entity's definition.

Code navigation uses the open source tree-sitter library. The following languages and navigation strategies are supported.

You do not need to configure anything in your repository to enable code navigation. We will automatically extract search-based and precise code navigation information for these supported languages in all repositories and you can switch between the two supported code navigation approaches if your programming language is supported by both.

GitHub has developed two code navigation approaches based on the open source tree-sitter and stack-graphs library:

- Search-based - searches all definitions and references across a repository to find entities with a given name
- Precise - resolves definitions and references based on the set of classes, functions, and imported definitions at a given point in your code

### More information:

- [Precise and search-based navigation](https://docs.github.com/en/repositories/working-with-files/using-files/navigating-code-on-github#precise-and-search-based-navigation)
- [Advanced search for code repositories](https://docs.github.com/en/repositories/working-with-files/using-files/navigating-code-on-github#using-the-symbols-pane)

## Permalinks

---

### More information:

- [File's Permalinks](https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files)

## Download source code

---

You can download a snapshot of the code in your repository.

You can download a snapshot of any branch, tag, or specific commit from GitHub.com. These snapshots are generated by the git archive command in one of two formats: tarball or zipball. Snapshots don't contain the entire repository history. If you want the entire history, you can clone the repository.

### More information:

- [Download source code](https://docs.github.com/en/repositories/working-with-files/using-files/downloading-source-code-archives)

## Advanced manipulation of non-code files

---

### More information:

[non-code files](https://docs.github.com/en/repositories/working-with-files/using-files/working-with-non-code-files)

## Managing large files

---

### More information:

[Managing large files](https://docs.github.com/en/repositories/working-with-files/managing-large-files)
