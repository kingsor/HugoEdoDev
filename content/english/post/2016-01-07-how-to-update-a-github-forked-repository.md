---
date: "2016-01-07T00:00:00Z"
description: I was looking for updating a forked repository and I found the answer
  on StackOverflow.
tags:
- developer
- git
- github
title: How to update a GitHub forked repository
---

My question was: how can I update a forked repo in order to view all the latest commits?

I found the answer on [StackOverflow](http://stackoverflow.com/a/7244456).

I quote it as a note to self.

> In your local clone of your forked repository, you can add the original GitHub repository as a "remote". ("Remotes" are like nicknames for the URLs of repositories - `origin` is one, for example.) Then you can fetch all the branches from that upstream repository, and rebase your work to continue working on the upstream version. In terms of commands that might look like:

```bash
# Add the remote, call it "upstream":

git remote add upstream https://github.com/whoever/whatever.git

# Fetch all the branches of that remote into remote-tracking branches,
# such as upstream/master:

git fetch upstream

# Make sure that you're on your master branch:

git checkout master

# Rewrite your master branch so that any commits of yours that
# aren't already in upstream/master are replayed on top of that
# other branch:

git rebase upstream/master
```

> If you don't want to rewrite the history of your master branch, (for example because other people may have cloned it) then you should replace the last command with `git merge upstream/master`. However, for making further pull requests that are as clean as possible, it's probably better to rebase.

> *Update*: If you've rebased your branch onto `upstream/master` you may need to force the push in order to push it to your own forked repository on GitHub. You'd do that with:

```bash
git push -f origin master
```

> You only need to use the `-f` the first time after you've rebased.