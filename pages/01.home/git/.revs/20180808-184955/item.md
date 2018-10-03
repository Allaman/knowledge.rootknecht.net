---
title: Git
taxonomy:
    category:
        - Others
---

[TOC]

## Change remote of an existing repo
Check current urls:
```bash
git remote -v
```
Switch urls:
```bash
git remote set-url origin NEWURL
```
Compare change
```bash
git remote -v
```
Push to new remote
```bash
git push -u origin master
```

## Run git command over all subdirectories

```bash
find . -maxdepth 1 -type d -exec git --git-dir={}/.git --work-tree=$PWD/{} pull \;
```

## Modify past commits
!!! Use it with care! Interactive rebase is almost almighty

Start the rebase at the last "good" commit

```bash
git rebase -i -p COMMITHASH
```

After this command a text editor will open. Edit the keywords at the beginning of the line, in this case `edit` allows us to modify the commits. After saving the file the first commit to be edited will be selected. Now you can run e.g. `git commit --amend --author="Michael <allaman@rootknecht.net>"`to modify the author. Then run `git rebase --continue` to go to the next marked commit. After rebasing run `git push --force-with-lease`.

## Git proxy
```bash
git config --global http.proxy http://proxy.company.com:3128
```
or in .git/config
```
[http]
	proxy = http://proxy.company.com:3128
```
or temporarly as command line argument
```bash
-c http.proxy http://proxy.company.com:3128
````

## Use Github and Gitlab
### Use multiple remotes named differently
```bash
git remote add github https://github.com/USER/repo.git
git push/pull origin
git push/pull github
```
When the origin is at github vice versa.

### Single remote with multiple targets
```bash
git remote set-url –add origin https://github.com/USER/repo.git
git push/pull origin
```
When the origin is at github vice versa. Now, origin will targed the Gitlab as well as Github remotes
