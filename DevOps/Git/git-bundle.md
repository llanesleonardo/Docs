# Git bundle

Move objects and refs by archive.

Create, unpack, and manipulate "bundle" files. Bundles are used for the "offline" transfer of Git objects without an active "server" sitting on the other side of the network connection.

They can be used to create both incremental and full backups of a repository, and to relay the state of the references in one repository to another.

Git commands that fetch or otherwise "read" via protocols such as ssh:// and https:// can also operate on bundle files. It is possible git-clone[1] a new repository from a bundle, to use git-fetch[1] to fetch from one, and to list the references contained within it with git-ls-remote[1]. There’s no corresponding "write" support, i.e.a git push into a bundle is not supported.

Bundles are .pack files (see git-pack-objects[1]) with a header indicating what references are contained within the bundle.

## Options

```
create [options] <file> <git-rev-list-args>
```

Used to create a bundle named file. This requires the <git-rev-list-args> arguments to define the bundle contents. options contains the options specific to the git bundle create subcommand. If file is -, the bundle is written to stdout.

---

```
verify <file>
```

Used to check that a bundle file is valid and will apply cleanly to the current repository. This includes checks on the bundle format itself as well as checking that the prerequisite commits exist and are fully linked in the current repository.

Then, git bundle prints a list of missing commits, if any. Finally, information about additional capabilities, such as "object filter", is printed. See "Capabilities" in gitformat-bundle[5] for more information. The exit code is zero for success, but will be nonzero if the bundle file is invalid. If file is -, the bundle is read from stdin.

---

```
list-heads <file>

```

Lists the references defined in the bundle. If followed by a list of references, only references matching those given are printed out. If file is -, the bundle is read from stdin.

---

```
unbundle <file>
```

Passes the objects in the bundle to git index-pack for storage in the repository, then prints the names of all defined references. If a list of references is given, only references matching those in the list are printed. This command is really plumbing, intended to be called only by git fetch. If file is -, the bundle is read from stdin.

---

```
--progress

```

Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

---

```
--version=<version>

```

Specify the bundle version. Version 2 is the older format and can only be used with SHA-1 repositories; the newer version 3 contains capabilities that permit extensions. The default is the oldest supported format, based on the hash algorithm in use.

---

```
-q
--quiet

```

This flag makes the command not to report its progress on the standard error stream.

---

Revisions must be accompanied by reference names to be packaged in a bundle.

More than one reference may be packaged, and more than one set of prerequisite objects can be specified. The objects packaged are those not contained in the union of the prerequisites.

The git bundle create command resolves the reference names for you using the same rules as git rev-parse --abbrev-ref=loose.

All of these simple cases are OK (assuming we have a "master" and "next" branch):

```
$ git bundle create master.bundle master
$ echo master | git bundle create master.bundle --stdin
$ git bundle create master-and-next.bundle master next
$ (echo master; echo next) | git bundle create master-and-next.bundle --stdin

$ git bundle create recent-master.bundle master~10..master
$ git bundle create recent-updates.bundle master~10..master next~5..next
```

## Examples

Assume you want to transfer the history from a repository R1 on machine A to another repository R2 on machine B. For whatever reason, direct connection between A and B is not allowed, but we can move data from A to B via some mechanism (CD, email, etc.). We want to update R2 with development made on the branch master in R1.

To bootstrap the process, you can first create a bundle that does not have any prerequisites. You can use a tag to remember up to what commit you last processed, in order to make it easy to later update the other repository with an incremental bundle:

```
machineA$ cd R1
machineA$ git bundle create file.bundle master
machineA$ git tag -f lastR2bundle master
```

Then you transfer file.bundle to the target machine B. Because this bundle does not require any existing object to be extracted, you can create a new repository on machine B by cloning from it:

```
machineB$ git clone -b master /home/me/tmp/file.bundle R2

```

This will define a remote called "origin" in the resulting repository that lets you fetch and pull from the bundle. The $GIT_DIR/config file in R2 will have an entry like this:

```
[remote "origin"]
    url = /home/me/tmp/file.bundle
    fetch = refs/heads/*:refs/remotes/origin/*
```

To update the resulting mine.git repository, you can fetch or pull after replacing the bundle stored at /home/me/tmp/file.bundle with incremental updates.

After working some more in the original repository, you can create an incremental bundle to update the other repository:

```
machineA$ cd R1
machineA$ git bundle create file.bundle lastR2bundle..master
machineA$ git tag -f lastR2bundle master
```

You then transfer the bundle to the other machine to replace /home/me/tmp/file.bundle, and pull from it.

```
machineB$ cd R2
machineB$ git pull
```

If you know up to what commit the intended recipient repository should have the necessary objects, you can use that knowledge to specify the prerequisites, giving a cut-off point to limit the revisions and objects that go in the resulting bundle. The previous example used the lastR2bundle tag for this purpose, but you can use any other options that you would give to the git-log[1] command. Here are more examples:

You can use a tag that is present in both:

```
$ git bundle create mybundle v1.0.0..master

```

You can use a prerequisite based on time:

```
$ git bundle create mybundle --since=10.days master

```

You can use the number of commits:

```
$ git bundle create mybundle -10 master
```

You can run git-bundle verify to see if you can extract from a bundle that was created with a prerequisite:

```
$ git bundle verify mybundle

```

This will list what commits you must have in order to extract from the bundle and will error out if you do not have them.

A bundle from a recipient repository’s point of view is just like a regular repository which it fetches or pulls from. You can, for example, map references when fetching:

```
$ git fetch mybundle master:localRef
```

You can also see what references it offers:

```
$ git ls-remote mybundle
```
