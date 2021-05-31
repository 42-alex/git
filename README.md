# This is Git Basics

## Sources for learning
* https://git-scm.com/docs
* https://git-scm.com/book/ru/v2
* https://ru.hexlet.io/courses/intro_to_git
* https://learngitbranching.js.org/?demo=&locale=ru_RU


## Git setup

### Config setup
```
git config --global user.name "Ivan Ivanov"
git config --global user.email "ivan.ivanov@gmail.com"
```
These settings are necessary for the Git to work properly. This data is inserted into the change history. This is the only way to find out who did what in the project


### Add SSH-keys
```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# There will be several questions further. All questions need to press Enter

# Launching an ssh agent that monitors keys
$ eval "$(ssh-agent -s)"

# Adding a private ssh key to the agent
$ ssh-add ~/.ssh/id_rsa

# At the last step, you need to add the public key ~/.ssh/id_rsa.pub
# to the remote repository (to your Github account)
```
This is in order not to be entered each time a login and password when you synchronize local and remote repository

### Add .gitignore
Create a file .gitignore in the project root and describe all folders and files which you want to exclude from your commits.
Example:
```
.idea/
.gitignore
```

### Show current branch in terminal ([source](https://ru.hexlet.io/blog/posts/kak-prisoedinitsya-k-rabote-nad-opensorsom-chto-takoe-ps1-i-drugie-voprosy-otvechaet-razrabotchik-heksleta-andrey-moshkov))
```
export PS1="💻 \[\e[1;34m\]\W\[\e[m\]\[\033[32m\]\$(__git_ps1)\[\033[00m\] $ "
```


## Create a new repository

1. Go to the folder with the project and execute the command
```
git init
```
2. Add files to the project and make a commit
```
git add .  # add all files
git commit -m "Initial commit"
```
3. Create an empty remote repository (for example, on Github.com)
4. Perform local and remote repository integration
```
git branch -M main
git remote add origin git@github.com:ivan/myproject.git 
git push -u origin main
```


## Clone a repository

```
git clone git@github.com:ivan/myproject.git
```


## Commands 

```
git status
```
Shows the status of the repository, changed files, files that are not being tracked and files prepared for commit.

```
git diff
```
Shows changes in all changed files. To show diff in index add flag `--staged`.
If the pager application opens, you need to press **f** to move down, **u** to move up and **q** to exit the view mode.

```
git log
```
Shows list of all commits sorted by date. `git log --oneline` shows compact version. `git log -p` shows diff for each commit.

```
git show 32f2
```
Shows diff only for specified commit. You can use only first four symbols from commit hash as it is always unique.

```
git blame README.md
```
Shows who, when and in which commit made changes.

```
git add file1 file2  # add file1 and file2
git add .            # add all untracked and changed files
git add -i           # manually specify which part of file should be commited
```
Adds files to index. After this command files are ready to be commited.
If you chose the third option the next info will be helpful for you

| Letter | Description |
| ------ | ----------- |
| y | stage this hunk |
| n | do not stage this hunk |
| q | quit; do not stage this hunk or any of the remaining ones |
| a | stage this hunk and all later hunks in the file |
| d | do not stage this hunk or any of the later hunks in the file |
| g | select a hunk to go to |
| / | search for a hunk matching the given regex |
| j | leave this hunk undecided, see next undecided hunk |
| J | leave this hunk undecided, see next hunk |
| k | leave this hunk undecided, see previous undecided hunk |
| K | leave this hunk undecided, see previous hunk |
| s | split the current hunk into smaller hunks |
| e | manually edit the current hunk |
| ? | print help |

```
git commit -m "(message that describes your commit)"
```
Commit files which were added to index with description message.

```
git commit --amend
```
Fix your last commit. You can either add new files to your last commit or just edit commit message of your last commit. Under the hood it makes `git reset` and creates a new commit with new data.

```
git push
```
Send commits from your current branch to remote repository.

```
git pull --rebase
```
Before starting work, you should always run this command, which downloads new commits from the external repository and adds them to the local repository.
`--rebase` flag is necessary to avoid unnecessary merge commits that worsen the change history

```
git rm file1
```
Remove file "file1" from working directory and add it to index (so it is ready to be commited)

```
git restore file1
```
Restore changed or removed file "file1". After this command "file1" will appear again in your working directory. You can also use flag `--staged` here. It will remove your file from index only and file will appear in your working directory. 

```
git revert 0cb9
```
Revert any commit. This command creates opposite changes to specified commit. It is enough to specify four first symbols of commit hash which you need to revert.

```
git reset --hard HEAD~
```
Remove last commit. `git reset --hard HEAD~2` will remove last two commits. `git reset HEAD~` will remove last commit but keeps changed files from commit which is removed in working directory.

```
git grep -i search_term
```
Searches all project files for a match with the specified string. `-i` flag means case insensitive. `git grep search_term 5120bea3` search in a specific commit. `git grep hexlet $(git rev-list --all)` search in all history.

```
git clean -fd
```
Remove all untracked files and folders in working directory. Flags `-f` - force, `-d` - directory.

```
git checkout 0cb9
```
Switch between branches or commits

```
git branch
```
Look what branch or commit loaded in working directory currently

```
git stash
```
Hide current changes from index to special stash folder.

```
git stash pop
```
Get hidden changes from stash and place it to index.
