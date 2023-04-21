# Git Mastery
https://codewithmosh.com/courses/enrolled/1120640

Here we will learn about:
- Fundamental concepts of Git
- Creating Snapshots
- Browsing project history
- Branching and merging
- Collaborating using Github
- Rewriting History

### What is git?
Git is a distributed version control system. We can look at the project history and see what has changed and why.
It is one of the most popular version control systems. Version Control Systems allow us to track our history and work together.
In the past the industry used centralized version control with Subversion and Team Foundation Server.
With a centralized server if the server fails then we lose everything. With a distributed version control system we have a local copy of the repository and we can push our changes to the server.
Git is the most popular because it is:
- Free
- Open Source
- Super Fast
- Scalable
- Cheap branching / merging

Git is a must-have for almost all software companies. Knowing git is a foundational skill.

### Using git
There are different ways to use git:
- Commandline
- Most IDEs have git integration
- Graphical user interfaces
  - the most popular is GitKraken
  - SourceTree is another option but it is only available for Windows and Mac

### Why Command line
- Gui tools have limitations as they are an abstraction on the git fundamentals
- Gui tools are not available on all platforms

In practice developers use the Gui tool with the command line.

### Installing git
For me git version returns:
```bash
tom@tom-ubuntu:~$ git version
git version 2.37.2
```
The latest version is 2.40.0:
https://git-scm.com/downloads

This link is useful for updating git on ubuntu:
https://www.cyberithub.com/how-to-update-git-to-a-newest-version-on-linux-ubuntu-20-04-lts/
First I checked the version above.
Next I removed git:
```bash
sudo apt remove git
```

Next I added the git-core ppa:
```bash
 sudo add-apt-repository ppa:git-core/ppa -y
```
This is to download and install the git package from Git maintainers repository.

Next I updated my system:
```bash
sudo apt-get update
```

I then install the latest git package:
```bash
sudo apt-get install git -y
```

I then checked the version:
```bash
tom@tom-ubuntu:~$ git --version
git version 2.40.0
```

### Configuring git
We can configure git using the git config command. We can configure git globally or per repository.
We can configure:
- Name
- Email
- Default Editor
- Line Endings (how git should handle them)

The settings are placed in a hierarchy:
- system: all users on the system and all repositories
- global: all repositories for the current user
- local: the current repository


I can check my git config with:
```bash
tom@tom-ubuntu:~$ git config --list
user.name=tom
user.email=<MY EMAIL>
core.autocrlf=input
```
If I wanted to change the settings I could run:
```bash
git config --global user.name "Tom"
git config --global user.email "<MY EMAIL>"
```
We can also set our global core editor:
```bash
git config --global core.editor "code --wait"
```
Here we set the editor to VS Code. The --wait flag is important as it tells git to wait for VS Code to close before continuing.
I will use Intellij:
```bash
git config --global core.editor "intellij-idea-ultimate --wait"
```
I can then open gitconfig with:
```bash
git config --global -e
```
We can also configure end of lines. Different operating systems use different end of line characters:
- Windows: \r\n
- Mac: \r
- Linux: \n

For Windows we should set:
```bash
git config --global core.autocrlf true
```
For mac or linux we should set:
```bash
git config --global core.autocrlf input
```

### Getting help with git
For git config we can check:
https://git-scm.com/docs/git-config

We can also access the same page on the terminal window with:
```bash
git config --help
```
If we want a quick reference we can use:
```bash
git config -h
```

### Git Cheat Sheet
Essential commands every developer should know:
- creating snapshots
- browsing history
- branching and merging
- collaborating using git and github
- rewriting history

### Creating Snapshots

#### Initialize a repository
```bash
git init
```

#### Add files to staging area
```bash
git add file1.js # stages a single file
git add file1.js file2.js # stages multiple files
git add *.js # stages all js files
git add . # stages all files in directory
```

#### Viewing status
```bash
git status # full status
git status -s # short status
```

#### Committing staged files
```bash
git commit -m "commit message" # commits with a one-line message
git commit # opens the default editor to type a long message
```

#### Skipping the staging area
```bash
git commit -am "Message"
```

#### Removing files
```bash
git rm file1.js # removes file from working directory and stages the removal
git rm --cached file1.js # removes file from staging area but keeps it in working directory
```

#### Moving files
```bash
git mv file1.js file2.js # moves file and stages the move
```

#### Viewing staged/unstaged changes
```bash
git diff # shows unstaged changes
git diff --staged # shows staged changes
git diff --cached # shows staged changes
```

#### Viewing commit history
```bash
git log # shows full commit history
git log --oneline # shows short commit history
git log --reverse # Lists commits from oldest to newest
```

#### Viewing a commit
```bash
git show 921a2ff # shows the commit with the given hash
git show HEAD # shows the latest commit
git show HEAD~2 # Two steps before last commit
git show HEAD:file.js # shows the file as it was in the given commit
```

#### Unstaging files (undoing git add)
```bash
git restore --staged file.js # Copies the last version of file.js from repo to index
```

#### Restoring an earlier version of a file
```bash
git restore --source=HEAD~2 file.js
```

### Browsing History

#### Viewing the history
```bash
git log --stat # shows the list of modified files
git log --patch # shows the actual changes made to each file
```

#### Filtering the history
```bash
git log --3 # shows the last 3 commits
git log --author="Mosh"
git log --before="2020-01-01"
git log --after="one week ago"
git log --grep="GUI" # commits with GUI in their message
git log -S"GUI" # commits with "GUI" in their patches'
git log hash1...hash2 # range of commits
git log file.txt # commits that touched file.txt
```

#### Formatting the log output
```bash
git log --pretty=format:"%an commit %H" # shows the author name and commit hash
tom@tom-ubuntu:~/Projects/Devops$ git log --pretty=format:"%an commit %H"
tom commit 089ce591bc16d753b211f627137342cfb4e174d8
tom commit 828a73e35385d26f92bd2a209ba11a022742bc08
tom commit 95478febc871c2e24e2bc662ea85900b3cfa5135
tom commit ec7109e92bb7b2f634c84d30aab195b535ee6c53
tom commit 367360e75bb5abc41fe369e948fa51c1c4cbcc14
tom commit 1f34900bb2ba1eb5bba5a8d8411d6f6d0da0ebce
tom commit 74b1e41133b69992e5edcf15a2857a28960029a1
tom commit b208b9ad8fc348736f581e4264df95c9fe4e13da

```

#### Creating an alias
```bash
git config --global alias.lg "log --oneline"
```

#### Viewing a commit
```bash

git show HEAD~2
git show HEAD~2:file.js # shows the file as it was in the given commit
```

#### Comparing commits
```bash
git diff HEAD~2 HEAD # shows changes between two commits
git diff HEAD~2 HEAD file.js # changes to file.js only
```

#### Checking out a commit
```bash
git checkout dad47ed # checks out the given commit
git checkout master # checks out the master branch
```

#### Finding a bad commit
```bash
git bisect start # starts the bisect session
git bisect bad # marks the current commit as bad
git bisect good 1f34900 # marks the given commit as good
git bisect reset # terminates the bisect session
```

#### Finding contributors
```bash
git shortlog # shows a list of contributors
```

#### Viewing the history of a file
```bash
git log file.txt # shows the commits that touched file.txt
git log --stat file.txt # shows the statistics (the number of changes) for file.txt
git log --patch file.txt # shows the patches (changes) applied to file.txt
```

#### Finding the author of lines
```bash
git blame file.txt # shows the author of each line in file.txt
```

#### Tagging
```bash
git tag v1.0 # tags the last commit as v1.0
git tag v1.0 5e7a828 # Tags an earlier commit
git tag # lists all the tags
git tag -d v1.0 # deletes the tag
```
### Branching and merging

#### Managing branches
```bash
git branch bugfix # creates a new branch called bugfix
git checkout bugfix # switches to the bugfix branch
git switch bugfix # same as checkout
git switch -C bugfix # creates a new branch and switches to it
git branch -d bugfix # deletes the bugfix branch
```

#### Comparing branches
```bash
git log master..bugfix # List the commits in the bugfix branch not in master
git diff master..bugfix # Shows the summary of changes
```

#### Stashing
```bash
git stash push -m "New tax rules" # creates a new stash
git stash list # lists the stashes
git stash show stash@{1} # shows the given stash
git stash show 1 # shortcut for stash@{1}
git stash apply 1 # applies the given stash to the working dir
git stash drop 1 # deletes the given stash
git stash clear # deletes all stashes
```

#### Merging
```bash
git merge bugfix # merges the bugfix branch into the current branch
git merge --no-ff bugfix # creates a merge commit even if FF is possible
git merge --squash bugfix # performs a squash merge
git merge --abort # aborts the merge
```

#### Viewing the merged branches
```bash
git branch --merged # lists the branches that have been merged into the current branch
git branch --no-merged # lists the branches that have not been merged into the current branch
```

### Rebasing
```bash
git rebase master # changes the base of the current branch
```

### Cherry picking
```bash
git cherry-pick dad47ed # applies the given commit to the current branch
```

### Collaboration
#### Cloning a repository
```bash
git clone url
```

#### Syncing with remotes
```bash
git fetch origin master # fetches master from origin
git fetch origin # fetches all objects from origin
git fetch # shortcut for 'git fetch origin'
git pull # fetch + merge
git push origin master # pushes master to origin
git push # shortcut for 'git push origin master'
```

#### Sharing tags
```bash
git push origin v1.0 # pushes the tag to origin
git push origin --delete v1.0
```

#### Sharing branches
```bash
git branch -r # shows remote tracking branches
git branch -vv # shows local and remote tracking branches
git push -u origin bugfix # pushes bugfix to origin
git push -d origin bugfix # removes bugfix from origin
```

#### Managing remotes
```bash
git remote # shows remote repos
git remote add upstream url # adds a new remote called upstream
git remote rm upstream # remotes upstream
```

### Rewriting History
#### Undoing commits
```bash
git reset --soft HEAD^ # removes the last commit, keeps change staged
git reset --mixed HEAD^ # Unstages the changes as well
git reset --hard HEAD^ # Discards local changes
```

#### Reverting commits
```bash
git revert 72856ea # reverts the given commit
git revert HEAD~3.. # reverts the last 3 commits
git revert HEAD~3..HEAD~1 # reverts the last 2 commits
git revert --no-commit HEAD~3...
```

#### Recovering lost commits
```bash
git reflog # shows the history of HEAD
git reflog show bugfix # shows the history of bugfix pointer
```

#### Amending the last commit
```bash
git commit --amend
```

#### Interactive rebasing
```bash
git rebase -i HEAD~5
```

### Creating snapshots
First we will create a directory and initialize a git repository
```bash
tom@tom-ubuntu:~/Projects$ mkdir Moon
tom@tom-ubuntu:~/Projects$ cd Moon
tom@tom-ubuntu:~/Projects/Moon$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Initialised empty Git repository in /home/tom/Projects/Moon/.git/
```

We can view the .git file:
```bash
tom@tom-ubuntu:~/Projects/Moon$ ls -a
.  ..  .git
open .git
```

![image](https://user-images.githubusercontent.com/27693622/233596557-cf4efae6-a7d8-41fc-9fd2-0ef7d7c0dffd.png)

#### Basic git workflow
![image](https://user-images.githubusercontent.com/27693622/233597435-22010553-cd85-487d-9b17-8014f94fbe73.png)




