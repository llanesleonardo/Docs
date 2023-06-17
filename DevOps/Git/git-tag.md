# Git tag

Create, list, delete or verify a tag object signed with GPG.

Add a tag reference in refs/tags/, unless -d/-l/-v is given to delete, list or verify tags.

Unless -f is given, the named tag must not yet exist.

If one of -a, -s, or -u <key-id> is passed, the command creates a tag object, and requires a tag message. Unless -m <msg> or -F <file> is given, an editor is started for the user to type in the tag message.

If -m <msg> or -F <file> is given and -a, -s, and -u <key-id> are absent, -a is implied.

Otherwise, a tag reference that points directly at the given object (i.e., a lightweight tag) is created.

A GnuPG signed tag object will be created when -s or -u <key-id> is used. When -u <key-id> is not used, the committer identity for the current user is used to find the GnuPG key for signing. The configuration variable gpg.program is used to specify custom GnuPG binary.

Tag objects (created with -a, -s, or -u) are called "annotated" tags; they contain a creation date, the tagger name and e-mail, a tagging message, and an optional GnuPG signature. Whereas a "lightweight" tag is simply a name for an object (usually a commit object).

Annotated tags are meant for release while lightweight tags are meant for private or temporary object labels. For this reason, some git commands for naming objects (like git describe) will ignore lightweight tags by default.

## Options

[Options](https://git-scm.com/docs/git-tag#_options)

## Examples

[Git tag](https://www.youtube.com/watch?v=vSsypsDRiMU)
[Git types of tags example](youtube.com/watch?v=Zyk3S0q_W30)
