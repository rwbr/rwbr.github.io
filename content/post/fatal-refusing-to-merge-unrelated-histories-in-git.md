---
title: "'fatal: refusing to merge unrelated histories' in git"
date: 2020-08-24T14:47:25+02:00
tags: [git]
---

This nasty error in git happens, when you try to merge wo repositories, that are not aware of the existence of the other repository. This means, these repositories have a mismatching commit history. 

<!--more-->

![Unrelated histories](/img/fatal-git-unrelated-history.png)

This error can happen in the following situations:

1. After you created a new repository and added some commits locally, you try to pull from a remote repository, which already has some commits on its own. In this case git has no clue, these twi repositories might be related, so it throws the error.
2. If the `.git` folder inside a cloned repository git deleted or corrupted, git becomes unaware of the local history and will complain with this error message, when you try to `push` to or `pull` from the remote repository.

## Solution

The commands `git pull` and the `git push` offer a command line option named **allow-unrelated-histories**. 

```
git pull origin master --allow-unrelated-histories
```