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
These settings are necessary for the Gir to work properly. This data is inserted into the change history. This is the only way to find out who did what in the project

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
