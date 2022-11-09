# Github cheat sheet

## Git issues

| No.        | Topics           | 
| ------------- |:-------------|
| 1. |[*Create-a-new-branch-with-git-and-manage-branches*](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)|
| 2. |[*Git - getting started*](https://www.atlassian.com/git/tutorials/setting-up-a-repository)|
| 3. |[*Git - tagging*](https://git-scm.com/docs/git-tag)|
| 4. |[*Change unpushed commit message*](https://stackoverflow.com/a/179147)|
| 5. |[*How do i fix a git detached head*](https://stackoverflow.com/questions/10228760/how-do-i-fix-a-git-detached-head)|

## Git branching
| No.        | Topics           | 
| ------------- |:-------------|
| 1. | [*Create new local branch*](#create-new-local-branch)|
| 2. | [*Create and manage branches*](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)|
| 2. | [*Push local branch on remote*](https://stackoverflow.com/questions/2765421/how-do-i-push-a-new-local-branch-to-a-remote-git-repository-and-track-it-too)|


## Git tagging
| No.        | Topics           | 
| ------------- |:-------------|
| 1. | [*Create tags*](#create-tags)|
| 2. | [*List tags*](#list-tags)|
| 3. | [*Pushing tags to remote servers*](#pushing-tags-to-remote-servers)|

## Git stashing
| No.        | Topics           | 
| ------------- |:-------------|
| 1. | [*Stash changes*](#stash-changes)|

## Git stageing
| No.        | Topics           | 
| ------------- |:-------------|
| 1. | [*Remove file from stage area*](#remove-file-from-stage-area)|

## Showing git actions
| No.        | Topics           | 
| ------------- |:-------------|
| 1. | [*Show changes in local commit*](#show-changes-in-local-commit)|
| 2. | [*Change message*](#change-message)|
| 3. | [*Viewing commit history*](#viewing-commit-history)|
| 3. | [*Undo pushed commits*](#undo-pushed-commits)|

# Git branching

### Create new local branch
- [git checkout -b <name_of_your_new_branch>]() - create the branch on your local machine and switch in this branch

**[⬆ Back to Top](#git-branching)**

### List branches
- [git branch -a]() - list all branches
- [git branch -r]() - list only remote branches
- [git branch -l]() - git branch -l

**[⬆ Back to Top](#git-branching)**

# Git tagging

### Create tags
You can create two types of tags: lightweight and annotated.
- [git tag <name_of_tag> <hashcode>]() - a lightweight tag is similar to a branch; it’s just a pointer to a specific commit. You don’t need to include any of the flags
- [git tag -a <name_of_tag> <hashcode>]() - an annotated tag, is stored as a full object in the Git database. These tags are checksummed; they contain the name of the person who created the tag, email, and date. Annotated tags include a message and can be verified with a GNU Privacy Guard (GPG). (-a make an unsigned, annotated tag object, flag with metadata)

- [git tag -a <name_of_tag> -m "<short_message>"]() - an annotated tag, (-m - use the given tag message (instead of prompting). If you don’t include this flag, Git will launch your code editor for you to include it.

**[⬆ Back to Top](#git-tagging)**

### List tags
- [git tag]() - list tag
- [git tag -l]() - list tag with optional -l or --list parameter
- [git tag -l "<specific_part_of_name>*"]() - alist tags by wildcard must include -l or --list parameter (begin or ending specific part of name)

**[⬆ Back to Top](#git-tagging)**

### Pushing tags to remote servers
- [git push origin <name_of_tag>]() - push command you must explicitly push each tag after they’ve been created
- [git push origin --tags]() - to push multiple tags

**[⬆ Back to Top](#git-tagging)**

# Git stashing

### Stash changes
- [git stash --include-untracked]() - stash untracked (new created files)
- [git stash save --include-untracked "New message"]() - create new stash index with untracked files and message (git puts stash on the top of stack) - command DEPRECATED in 2.15.x/2.16:
- [git stash save -u "New message"]() - create new stash index with message (git puts stash on the top of stack) - command DEPRECATED in 2.15.x/2.16:

- [git stash push --include-untracked -m "New stash name"]() - create new stash index with untracked files and message (git puts stash on the top of stack)
- [git stash push -u -m "New stash name"]() - create new stash index with message (git puts stash on the top of stack):
 
### Listing stashes
- [git stash list]() - list stashed index
- [git stash list --stat]() - listing all stash changes in index with a files that was added or modified without pointing which of these added or modified
- [git stash list --name-status]() - listing all stash changes in index with a files that was added or modified 
- [git stash show]() - show summary of stash with number of changes rows (from top of stack)
- [git stash show stash@{1}]() - show summary of stash with number of changes rows (specific by stash index)
- [git stash show -p stash@{0}]() - showing changes inside files in specific stash
- [git stash show stash@{0} --name-status]() - showing/listing which files was changed in a specific stash with info about what was added or modified: 
 
### Applying stash
- [git stash apply stash@{0}/<nuber_of_indexed_stash>]() - get specific stash and applies it to the repo (without deleting it from stack)
- [git stash pop stash@{1}]() - get specific stash and applies it to the repo (deleting it from stack)
- [git stash branch <branch_name> stash@{1}]() - command creates and checks out a new branch named <branchname> starting from the commit at which the <stash> was originally created, applies the changes recorded in <stash> to the new working tree and index, then drops the <stash> if that completes successfully. When no <stash> is given, applies the latest one.
 
### Clear stash
- [git stash clear]() - remove all stashes made in repo
- [git stash drop stash{1}]() - remove specific stash made in repo:

[How To Git Stash Changes](https://devconnected.com/how-to-git-stash-changes/)
 
**[⬆ Back to top](#git-stashing)**
 
# Git stageing
 
### Remove file from stage area
- [git reset HEAD -- path/to/file]() - remove file from stage area
- [  git reset HEAD -- .]() - remove all files from current directory from stage area
 
**[⬆ Back to Top](#git-stashing)**

# Git committing

### Show changes in local commit
- [git log]() - show all commits with data like hash, author, date etc
- [git show <commit_hash>]() - show commited files

### Change message
- [git commit --amend -m "New commit message"]() - change commit message
 
**[⬆ Back to Top](#showing-git-actions)** 

### Viewing commit history 
- [git log --oneline]() - showing commit in oneline

**[⬆ Back to Top](#showing-git-actions)** 
 
[Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

**[⬆ Back to Top](#showing-git-actions)** 
 
### Undo pushed commits 
[Git - Undo pushed commits](https://stackoverflow.com/a/56970242) 
```
git reset <sha1 poprzedniego>
git commit -m 'revert'
git push -f ~
 ```
 or
 ```
git reset --hard 'xxxxx'
git clean -f -d
git push -f
 ```
 **[⬆ Back to Top](#showing-git-actions)** 

