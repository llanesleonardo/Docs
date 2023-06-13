# Hunk

In Git, a "hunk" refers to a distinct portion of a file's changes that is selected for inclusion in a commit or a patch. It represents a section of modified or added content within a file.

When you make changes to a file, Git analyzes the differences between the previous version of the file and the modified version. It breaks down these differences into smaller chunks called "hunks" for easier management and selective inclusion in commits.

A hunk represents a coherent block of changes within a file. It typically consists of several lines of added, modified, or deleted content. Each hunk is identified by the line range where the changes occur in the file.

Here's an example of a hunk:

```
@@ -5,6 +5,6 @@
 This is the original content of the file.

-This line has been removed.
+This line has been modified.

 This line has been added.

```

In this example, the hunk starts with the @@ -5,6 +5,6 @@ line, which indicates the line range where the changes occur. The - symbol indicates that the line(s) have been removed, the + symbol indicates that the line(s) have been added, and the @@ symbol separates the line range of the original content and the modified content.

Hunks are commonly used in various Git commands and tools, such as git add -p (or git add --patch) and git diff. These commands allow you to interactively review and select specific hunks to include or exclude from a commit or patch. This fine-grained control over hunks helps in managing changes and creating clean and meaningful commits.

By working with hunks, you can selectively stage or discard specific changes within a file, allowing for more granular control over the content that is committed or included in patches.
