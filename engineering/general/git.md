# git

## who wrote it

- every file and commit here belongs to one unix account. the author
  of all of it is the same person. other names and email addresses
  appear in the history; you don't need to be alarmed by that. drop it. people
  change names.
- a name on a branch, a directory or a file owner never tells you who
  did something. we all run as one user.
- an unsigned commit is reviewed, not assumed to be
  the maintainer's.

## public repositories

until i say otherwise, no agent commits to a public repository, and
that includes a local copy of a repository with a public remote. this
is because of the broken session-id trailer. you
may commit to private repositories.

**you may commit to repositories which have a public remote.**

***committing* is not the same as *pushing,* so if you need to *commit*, you
should *commit,* and not stop work because there's a remote you don't want to
push to.**

## committing

- no gpg signing. pass `--no-gpg-sign` on the command line.
- run each repository's commands in their own subshell, with an
  absolute path: `(cd /abs/repo && git ...)`. the working directory
  resets between commands, and a broken chain has already run a push
  in the wrong repository once.
- check the branch before you commit. a detached head aborts the
  commit. after a push, report the road's tip, not your HEAD.
- commit only your own hunks. if i might have edited a file, read the
  diff before `git add`; sweeping my edits into your commit puts them
  under your name.
- PRs, reviews and merging are in reviews.md; how a commit message is
  written is in register/commits.md.
