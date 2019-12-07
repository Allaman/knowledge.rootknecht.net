---
title: Git
taxonomy:
    category:
        - Application
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
! Use it with care! Interactive rebase is almost almighty

Start the rebase at the last "good" commit

```bash
git rebase -i -p COMMITHASH
```
or start from the initial commit with

```bash
git rebase -i --root $tip
```

After this command a text editor will open. Edit the keywords at the beginning of the line, in this case `edit` allows us to modify the commits. After saving the file the first commit to be edited will be selected. Now you can run e.g.
```bash
git commit --amend --author="Michael <allaman@rootknecht.net>"
```
to modify the author. Then run
```bash
git rebase --continue
```
to go to the next marked commit. After rebasing run
```bash
git push --force-with-lease
```
to push your modifications.

## Proxy settings
```bash
git config --global http.proxy http://proxy.company.com:3128
```
or in .git/config
```ini
[http]
	proxy = http://proxy.company.com:3128
```
or temporarly as command line argument
```bash
-c http.proxy http://proxy.company.com:3128
````

## Disable certificate validation
```bash
git config --global http.sslVerify=false
```
or in .git/config
```ini
[http]
sslVerify = false
```
or temporarly as command line argument
```bash
-c http.sslVerify=false
```

## Show the current branch

```bash
git rev-parse --abbrev-ref HEAD
```

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

## Edit git config with editor

```bash
git config [--global] --edit
```

## Set git file endings to LF (msysgit)

```sh
git config --global core.autocrlf false
git config --global core.eol lf
```

## Debug git command

```sh
GIT_CURL_VERBOSE=1 GIT_TRACE=1 git pull
```

even more output:

```sh
set -x; GIT_TRACE=2 GIT_CURL_VERBOSE=2 GIT_TRACE_PERFORMANCE=2 GIT_TRACE_PACK_ACCESS=2 GIT_TRACE_PACKET=2 GIT_TRACE_PACKFILE=2 GIT_TRACE_SETUP=2 GIT_TRACE_SHALLOW=2 git pull origin master -v -v; set +x
```
## List all repos a Github user is allowed to access

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Small CLI script to list basic overview of our Github repositories

- Access and repositories are based upon the user's permissions
- Default ouput is a SingleTable (fancier) but ASCII Table is supported as well
- Show last commit only since a defined period of time to limit required API calls

Install dependencies with 'pip3 install --user PyGithub, terminaltables' or appropriate command
"""
__version__ = "1.0.0"

from datetime import datetime, timedelta
import argparse
from github import Github
from terminaltables import AsciiTable, SingleTable

def main(args):
    """ entry point """
    g = Github(args.token)

    data = [['Name', 'URL', 'Tags', 'Branches', 'Last Commit']]

    since = datetime.now() - timedelta(days=args.days)

    for repo in g.get_user().get_repos():
        # to see all the available attributes and methods
        # print(dir(repo))
        commits = repo.get_commits(since=since)
        date = 'unknown'
        author = 'unknown'
        try:
            if commits.totalCount > 0:
                last_commit = commits[0]
                date = last_commit.last_modified
                author = last_commit.author.login
        except:
            pass # empty repo found ^^
        name = repo.name
        url = repo.clone_url
        tags = []
        for tag in repo.get_tags():
            tags.append(tag.name)
        branches = []
        for branch in repo.get_branches():
            branches.append(branch.name)
        data.append([name, url, '\n'.join(tags), '\n'.join(branches), f"{date} by {author}"])

    if (args.a):
        table = AsciiTable(data)
    else:
        table = SingleTable(data)
    table.inner_row_border = True
    print(table.table)

if __name__ == "__main__":
    """ Executed from the commandline"""
    parser = argparse.ArgumentParser(description='Terminal Github Overview for Innio')
    parser.add_argument('-t', '--token', action='store', required=True, help='your Github API token')
    parser.add_argument('-d', '--days', action='store', type=int, default=1, help='list commits since x days')
    parser.add_argument('-a', action='store_true', default=False, help='use simple ASCII table as output')
    parser.add_argument('-v', action='version',version='%(prog)s (version {version})'.format(version=__version__))
    args = parser.parse_args()
    main(args)

```
