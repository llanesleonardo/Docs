# Git clone

Clone a repository into a new directory.

Clones a repository into a newly created directory, creates remote-tracking branches for each branch in the cloned repository (visible using git branch --remotes), and creates and checks out an initial branch that is forked from the cloned repository’s currently active branch.

After the clone, a plain git fetch without arguments will update all the remote-tracking branches, and a git pull without arguments will in addition merge the remote master branch into the current master branch, if any (this is untrue when "--single-branch" is given; see below).

This default configuration is achieved by creating references to the remote branch heads under refs/remotes/origin and by initializing remote.origin.url and remote.origin.fetch configuration variables.

## Options

```
--bare
```

Make a bare Git repository. That is, instead of creating <directory> and placing the administrative files in <directory>/.git, make the <directory> itself the $GIT_DIR. This obviously implies the --no-checkout because there is nowhere to check out the working tree. Also the branch heads at the remote are copied directly to corresponding local branch heads, without mapping them to refs/remotes/origin/. When this option is used, neither remote-tracking branches nor the related configuration variables are created.

```
--sparse
```

Employ a sparse-checkout, with only files in the toplevel directory initially being present.

```
--also-filter-submodules
```

Also apply the partial clone filter to any submodules in the repository. Requires --filter and --recurse-submodules. This can be turned on by default by setting the clone.filterSubmodules config option.

```
--mirror
```

Set up a mirror of the source repository. This implies --bare. Compared to --bare, --mirror not only maps local branches of the source to local branches of the target, it maps all refs (including remote-tracking branches, notes etc.) and sets up a refspec configuration such that all these refs are overwritten by a git remote update in the target repository.

```
-o <name>
--origin <name>
```

Instead of using the remote name origin to keep track of the upstream repository, use <name>. Overrides clone.defaultRemoteName from the config.

```
--template=<template-directory>
```

Specify the directory from which templates will be used;

```
-c <key>=<value>
--config <key>=<value>
```

Set a configuration variable in the newly-created repository; this takes effect immediately after the repository is initialized, but before the remote history is fetched or any files checked out. The key is in the same format as expected by git-config[1] (e.g., core.eol=true). If multiple values are given for the same key, each value will be written to the config file. This makes it safe, for example, to add additional fetch refspecs to the origin remote.

Due to limitations of the current implementation, some configuration variables do not take effect until after the initial fetch and checkout. Configuration variables known to not take effect are: remote.<name>.mirror and remote.<name>.tagOpt. Use the corresponding --mirror and --no-tags options instead.

```
--no-tags
```

Don’t clone any tags, and set remote.<remote>.tagOpt=--no-tags in the config, ensuring that future git pull and git fetch operations won’t follow any tags. Subsequent explicit tag fetches will still work, (see git-fetch[1]).

Can be used in conjunction with --single-branch to clone and maintain a branch with no references other than a single cloned branch. This is useful e.g. to maintain minimal clones of the default branch of some repository for search indexing.

```
<repository>

```

The (possibly remote) repository to clone from. See the GIT URLS section below for more information on specifying repositories.

```
<directory>
```

The name of a new directory to clone into. The "humanish" part of the source repository is used if no directory is explicitly given (repo for /path/to/repo.git and foo for host.xz:foo/.git). Cloning into an existing directory is only allowed if the directory is empty.

```
--bundle-uri=<uri>
```

Before fetching from the remote, fetch a bundle from the given <uri> and unbundle the data into the local repository. The refs in the bundle will be stored under the hidden refs/bundle/\* namespace. This option is incompatible with --depth, --shallow-since, and --shallow-exclude.

## Git urls

In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching, but this is inefficient and deprecated; do not use it).

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

ssh://[user@]host.xz[:port]/path/to/repo.git/

git://host.xz[:port]/path/to/repo.git/

http[s]://host.xz[:port]/path/to/repo.git/

ftp[s]://host.xz[:port]/path/to/repo.git/

An alternative scp-like syntax may also be used with the ssh protocol:

[user@]host.xz:path/to/repo.git/

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path foo:bar could be specified as an absolute path or ./foo:bar to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support ~username expansion:

ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/

git://host.xz[:port]/~[user]/path/to/repo.git/

[user@]host.xz:/~[user]/path/to/repo.git/

For local repositories, also supported by Git natively, the following syntaxes may be used:

/path/to/repo.git/

file:///path/to/repo.git/

These two syntaxes are mostly equivalent, except the former implies --local option.

git clone, git fetch and git pull, but not git push, will also accept a suitable bundle file.

## Examples

Clone from upstream:

```
$ git clone git://git.kernel.org/pub/scm/.../linux.git my-linux
$ cd my-linux
$ make
```

Make a local clone that borrows from the current directory, without checking things out:

```
$ git clone -l -s -n . ../copy
$ cd ../copy
$ git show-branch
```

Clone from upstream while borrowing from an existing local directory:

```
$ git clone --reference /git/linux.git \
	git://git.kernel.org/pub/scm/.../linux.git \
	my-linux
$ cd my-linux
```

Create a bare repository to publish your changes to the public:

```
$ git clone --bare -l /home/proj/.git /pub/scm/proj.git
```
