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
git log -3 # shows the last 3 commits
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

#### Real example
![image](https://user-images.githubusercontent.com/27693622/233598724-bebba593-36dd-4f4b-ac0e-29b27f656bb2.png)

Git compresses the content and doesn't store duplicate content. Each commit contains a complete snapshot of our project.
We add files to our project:
```bash
tom@tom-ubuntu:~/Projects/Moon$ echo hello > file1.txt
tom@tom-ubuntu:~/Projects/Moon$ ls
file1.txt
tom@tom-ubuntu:~/Projects/Moon$ echo hello > file2.txt
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master

No commits yet

Untracked files:
(use "git add <file>..." to include in what will be committed)
file1.txt
file2.txt

nothing added to commit but untracked files present (use "git add" to track)
```
We now have changes ready to be committed:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file1.txt
	new file:   file2.txt
```
We now make a change:
```bash
tom@tom-ubuntu:~/Projects/Moon$ echo world >> file1.txt
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file1.txt
	new file:   file2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.txt
```
Git add took a snapshot and added that snapshot to the staging area. We now have a second version of the file.
We then add the change to staging:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git add file1.txt
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file1.txt
	new file:   file2.txt
```
We now commit the change to our repository:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git commit
hint: Waiting for your editor to close the file... CompileCommand: exclude com/intellij/openapi/vfs/impl/FilePartNodeRoot.trieDescend bool exclude = true
[master (root-commit) e5cf52f] Initial commit.
 2 files changed, 3 insertions(+)
 create mode 100644 file1.txt
 create mode 100644 file2.txt
tom@tom-ubuntu:~/Projects/Moon$ git log
commit e5cf52f88b68151c8cfbd0fa4ce601e4142ac34b (HEAD -> master)
Author: tom <tomspencerlondon@gmail.com>
Date:   Fri Apr 21 10:26:37 2023 +0100

    Initial commit.
    
    This is our first commit.
```
Commits shouldn't be too big or too small. We don't want to wait for the whole feature. Commits should be checkpoints for changes.
Each commit should be a logical change. It is important to make the commit messages meaningful. If the commit represents a single unit of work
it can help make the message easier to write. Most people use present tense:
Fixes the bug rather than Fixed the bug

We can also skip staging:
```bash
tom@tom-ubuntu:~/Projects/Moon$ echo test >> file1.txt
tom@tom-ubuntu:~/Projects/Moon$ git commit -am "Fix the bug that prevented users from siging up"
[master 1b2cacd] Fix the bug that prevented users from siging up
 1 file changed, 1 insertion(+)
```

#### Removing files
```bash
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    file2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
The file is still in staging:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git ls-files
file1.txt
file2.txt
```
We can add the change to staging:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git add file2.txt
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
deleted:    file2.txttom@tom-ubuntu:~/Projects/Moon$ git add file2.txt
        tom@tom-ubuntu:~/Projects/Moon$ git status
        On branch master
        Changes to be committed:
        (use "git restore --staged <file>..." to unstage)
        deleted:    file2.txt
```
We now don't have file2.txt in staging:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git ls-files
file1.txt
```
We can now commit the change to our local repository:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git commit -m "Remove unused code."
[master 00a21d9] Remove unused code.
 1 file changed, 1 deletion(-)
 delete mode 100644 file2.txt
```
To remove the file from the working directory and staging area in one step we can run:
```bash
git rm file2.txt *.txt
```

#### Renaming files
If we rename the file we have two changes:
```bash
tom@tom-ubuntu:~/Projects/Moon$ mv file1.txt main.js
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	main.js

no changes added to commit (use "git add" and/or "git commit -a")
```
We now have to add both files:

```bash
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	main.js

no changes added to commit (use "git add" and/or "git commit -a")
tom@tom-ubuntu:~/Projects/Moon$ git add file1.txt main.js
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    file1.txt -> main.js

```
We can change the files and add them to git with:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git mv main.js file1.js
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    file1.txt -> file1.js
```

We can also add files to gitignore:
```bash
tom@tom-ubuntu:~/Projects/Moon$ mkdir logs
tom@tom-ubuntu:~/Projects/Moon$ echo hello > logs/dev.log
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    file1.txt -> file1.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	logs/

tom@tom-ubuntu:~/Projects/Moon$ echo logs/ > .gitignore
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    file1.txt -> file1.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.gitignore
```
We can also remove files that we have added by mistake:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git rm --cached -r bin/
rm 'bin/app.bin'
tom@tom-ubuntu:~/Projects/Moon$ git ls-files
.gitignore
file1.js
```
This link is useful for different templates for .gitignore for different languages:
https://github.com/github/gitignore

We can reduce the verbosity of git status with -s:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file2.js

no changes added to commit (use "git add" and/or "git commit -a")
tom@tom-ubuntu:~/Projects/Moon$ git status -s
 M file1.js
?? file2.js
```
Here M = modified and ?? = untracked.

#### Viewing staged and unstaged commits
git status only lists the files changed. To see the difference we can use:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git diff --staged
diff --git a/file1.js b/file1.js
index badfb70..47c3216 100644
--- a/file1.js
+++ b/file1.js
@@ -1,3 +1,5 @@
 hello
 world
 test
+sky
+ocean
diff --git a/file2.js b/file2.js
new file mode 100644
index 0000000..f5e95e7
--- /dev/null
+++ b/file2.js
@@ -0,0 +1 @@
+sky

```
Here we are comparing two copies of the same file. We then have changes in the old copy and in the new copy indicated by plus
and minus. 

If we want to compare working directory with staging we just run:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git diff
diff --git a/file1.js b/file1.js
index 47c3216..8636dbe 100644
--- a/file1.js
+++ b/file1.js
@@ -1,4 +1,4 @@
-hello
+hello world
 world
 test
 sky

```

### Git log
We can view the history of commits with git log:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git log --oneline
b162a48 (HEAD -> master) Remove bin
db0d1c8 Include bin/ in gitignore
a5e7671 Add bin.
abe9863 add gitignore
00a21d9 Remove unused code.
1b2cacd Fix the bug that prevented users from siging up
e5cf52f Initial commit.
tom@tom-ubuntu:~/Projects/Moon$ git log --oneline --reverese
fatal: unrecognised argument: --reverese
tom@tom-ubuntu:~/Projects/Moon$ git log --oneline --reverse
e5cf52f Initial commit.
1b2cacd Fix the bug that prevented users from siging up
00a21d9 Remove unused code.
abe9863 add gitignore
a5e7671 Add bin.
db0d1c8 Include bin/ in gitignore
b162a48 (HEAD -> master) Remove bin

```

We can use git show to show the changes in a commit:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git log --oneline
b162a48 (HEAD -> master) Remove bin
db0d1c8 Include bin/ in gitignore
a5e7671 Add bin.
abe9863 add gitignore
00a21d9 Remove unused code.
1b2cacd Fix the bug that prevented users from siging up
e5cf52f Initial commit.
tom@tom-ubuntu:~/Projects/Moon$ git show db0d1c8
commit db0d1c8985388c8a97e216f6e67644f6c230af34
Author: tom <tomspencerlondon@gmail.com>
Date:   Fri Apr 21 12:54:18 2023 +0100

    Include bin/ in gitignore

diff --git a/.gitignore b/.gitignore
index 333c1e9..787e9a7 100644
--- a/.gitignore
+++ b/.gitignore
@@ -1 +1,2 @@
 logs/
+bin

```

We can show the difference between HEAD and 2 commits before:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git show HEAD~2
commit a5e7671bdb84e73692ad088fbabfe8efbcb276b3
Author: tom <tomspencerlondon@gmail.com>
Date:   Fri Apr 21 12:53:20 2023 +0100

    Add bin.

diff --git a/bin/app.bin b/bin/app.bin
new file mode 100644
index 0000000..ce01362
--- /dev/null
+++ b/bin/app.bin
@@ -0,0 +1 @@
+hello

```
We can also show changes for a specific file:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git show HEAD~1:.gitignore
logs/
bin
```
We can show all the files in the commit:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git ls-tree HEAD~1
100644 blob 787e9a756a1b16bc07fcb8ee6ad0ca85d321b2fa	.gitignore
040000 tree 64629cd51ef4a65a9d9cb9e656e1f46e07e1357f	bin
100644 blob badfb70fd8b1725682b26674f7b2882e94078579	file1.js
```

### Git objects
Git objects can be:
- commits
- blobs (Files)
- Trees (Directories)
- Tags

#### Unstaging files
We can use git restore undo changes to files:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git restore --staged file1.js
tom@tom-ubuntu:~/Projects/Moon$ git status -s
 M .gitignore
 M file1.js
A  file2.js
```
We can also restore after commits:
```bash
tom@tom-ubuntu:~/Projects/Moon$ git restore --source=HEAD~1 file1.js
tom@tom-ubuntu:~/Projects/Moon$ git status -s
 M .gitignore
?? file1.js

```

### Browsing History
Here we will look at:
- search for commits (by author, date, message, etc.)
- View a commit
- Restore your project to an earlier point
- compare commits
- view the history of a file
- find a bad commit that introduced a bug

#### getting a repository
To show additions for each commit we can use:
```bash
git log --oneline --stat
```
to show changes for each commit we can use:
```bash
git log --oneline --patch
```

We can filter by author:
```bash
git log --oneline --author="Mosh"
```
and also by date:
```bash
git log --oneline --after="2020-08-17"
git log --oneline --after="one week ago"
```
We can also search by message content:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline --grep="GUI"
24e86ee Add command line and GUI tools to the objectives.
```
We can search by the content of the commit:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline -S"OBJECTIVES"
a642e12 (HEAD -> master) Add header to all pages.

tom@tom-ubuntu:~/Projects/Venus$ git log --oneline -S"OBJECTIVES" --patch
a642e12 (HEAD -> master) Add header to all pages.
diff --git a/objectives.txt b/objectives.txt
index d31b40a..c882718 100644
--- a/objectives.txt
+++ b/objectives.txt
@@ -1,3 +1,4 @@
+OBJECTIVES 
 
 By the end of this course, you'll be able to 
 - Create snapshots 
```

For commits between a range:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline fb0d184..edb3594
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
```

To check changes for a file:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline toc.txt
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
ca49180 Initial commit.
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline -- toc.txt
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
ca49180 Initial commit.

tom@tom-ubuntu:~/Projects/Venus$ git log --oneline --patch -- toc.txt
a642e12 (HEAD -> master) Add header to all pages.
diff --git a/toc.txt b/toc.txt
index d019492..cc0798f 100644
--- a/toc.txt
+++ b/toc.txt
@@ -1,5 +1,5 @@
 TABLE OF CONTENT
-================
+
 Creating Snapshots
   - Initializing a repository
   - Staging changes
\ No newline at end of file
50db987 Include the first section in TOC.
diff --git a/toc.txt b/toc.txt
index 8b13789..d019492 100644
--- a/toc.txt
+++ b/toc.txt
@@ -1 +1,5 @@
-
+TABLE OF CONTENT
+================
+Creating Snapshots
+  - Initializing a repository
+  - Staging changes
\ No newline at end of file
ca49180 Initial commit.
diff --git a/toc.txt b/toc.txt
new file mode 100644
index 0000000..8b13789
--- /dev/null
+++ b/toc.txt
@@ -0,0 +1 @@
+

```
This link is useful for git-log abbreviations:
https://git-scm.com/docs/git-log

For instance to show the author and the committer we can use:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --pretty=format:"%an committed %h"
Moshfegh Hamedani committed a642e12
Moshfegh Hamedani committed 50db987
Moshfegh Hamedani committed 555b62e
Moshfegh Hamedani committed 91f7d40
Moshfegh Hamedani committed edb3594
Moshfegh Hamedani committed 24e86ee
Moshfegh Hamedani committed 36cd6db
Moshfegh Hamedani committed 9b6ebfd
Moshfegh Hamedani committed fa1b75e
Moshfegh Hamedani committed dad47ed
Moshfegh Hamedani committed fb0d184
Moshfegh Hamedani committed 1ebb7a7
Moshfegh Hamedani committed ca49180

tom@tom-ubuntu:~/Projects/Venus$ git log --pretty=format:"%an committed %h on %cd"
Moshfegh Hamedani committed a642e12 on Tue Aug 18 09:23:19 2020 -0700
Moshfegh Hamedani committed 50db987 on Mon Aug 17 14:27:50 2020 -0700
Moshfegh Hamedani committed 555b62e on Mon Aug 17 14:26:49 2020 -0700
Moshfegh Hamedani committed 91f7d40 on Mon Aug 17 14:25:43 2020 -0700
Moshfegh Hamedani committed edb3594 on Mon Aug 17 14:24:38 2020 -0700
Moshfegh Hamedani committed 24e86ee on Mon Aug 17 14:23:52 2020 -0700
Moshfegh Hamedani committed 36cd6db on Mon Aug 17 14:22:51 2020 -0700
Moshfegh Hamedani committed 9b6ebfd on Mon Aug 17 14:22:17 2020 -0700
Moshfegh Hamedani committed fa1b75e on Mon Aug 17 14:21:30 2020 -0700
Moshfegh Hamedani committed dad47ed on Mon Aug 17 14:20:50 2020 -0700
Moshfegh Hamedani committed fb0d184 on Mon Aug 17 14:18:09 2020 -0700
Moshfegh Hamedani committed 1ebb7a7 on Mon Aug 17 14:17:31 2020 -0700
Moshfegh Hamedani committed ca49180 on Mon Aug 17 14:17:15 2020 -0700

``` 
This puts the author in green:
```bash
 git log --pretty=format:"%Cgreen%an%Creset committed %h on %cd"
```
We can also add aliases:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git config --global alias.unstage "restore --staged ."
tom@tom-ubuntu:~/Projects/Venus$ git unstage
```

To show a commit two commits before HEAD we can use:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git show HEAD~2
commit 555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6
Author: Moshfegh Hamedani <moshfegh@live.com.au>
Date:   Mon Aug 17 14:26:49 2020 -0700

    Include the note about committing after staging the changes.

diff --git a/sections/creating-snapshots/staging-changes.txt b/sections/creating-snapshots/staging-changes.txt
index bddf7bd..506a158 100644
--- a/sections/creating-snapshots/staging-changes.txt
+++ b/sections/creating-snapshots/staging-changes.txt
@@ -7,3 +7,5 @@ To stage the changes, run:
 You can add multiple files separated by a space. 
 You can use a . to add all the files and subdirectories recursively.
 
+Once you stage the changes, you need to commit them to store the 
+proposed snapshot permanently. 
\ No newline at end of file
```

To show the changes for a file two commits before:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git show HEAD~2:sections/creating-snapshots/staging-changes.txt
STAGING CHANGES 
===============
To stage the changes, run:

> git add <filename>

You can add multiple files separated by a space. 
You can use a . to add all the files and subdirectories recursively.

Once you stage the changes, you need to commit them to store the 
proposed snapshot permanently. 
```
We can also show diff with only the name of the file and status:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git diff HEAD~2 HEAD --name-only
audience.txt
objectives.txt
sections/creating-snapshots/init.txt
sections/creating-snapshots/staging-changes.txt
toc.txt
tom@tom-ubuntu:~/Projects/Venus$ git diff HEAD~2 HEAD --name-status
M       audience.txt
M       objectives.txt
M       sections/creating-snapshots/init.txt
M       sections/creating-snapshots/staging-changes.txt
M       toc.txt

```
To see a complete snapshot we can checkout a commit:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git checkout 24e86ee
Note: switching to '24e86ee'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 24e86ee Add command line and GUI tools to the objectives.
```
![image](https://user-images.githubusercontent.com/27693622/233656583-9337a5f7-7626-4f75-a120-348b37e4f44d.png)

Our head is ad a detached position in the history so git log only shows the commits after the one we checked out:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline
24e86ee (HEAD) Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline --all
a642e12 (master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee (HEAD) Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```
Above we use --all to see the commits before the current HEAD position.

To put the HEAD back to the master branch we can use:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git checkout master
Previous HEAD position was 24e86ee Add command line and GUI tools to the objectives.
Switched to branch 'master'
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

#### Git bisect

We can use git bisect to find a bug. We don't want to checkout all the commits. We can use bisect to find the commit that introduced the bug.
We use:
- git bisect good
- git bisect bad
- git bisect reset

To view short log:
```bash
git shortlog -n -s -e --before="" --after=""
```

To view number of changes on each commit we use:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline --stat toc.txt
a642e12 (HEAD -> master) Add header to all pages.
 toc.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
50db987 Include the first section in TOC.
 toc.txt | 6 +++++-
 1 file changed, 5 insertions(+), 1 deletion(-)
ca49180 Initial commit.
 toc.txt | 1 +
 1 file changed, 1 insertion(+)

```

To view the changes on each commit we use:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline --patch toc.txt
```

If we remove or edit a file in error we can undo the change with git checkout on the file and then commit the change:
```bash

tom@tom-ubuntu:~/Projects/Venus$ git rm toc.txt
rm 'toc.txt'
tom@tom-ubuntu:~/Projects/Venus$ git commit -m "Remove toc.txt"
[master bfbb678] Remove toc.txt
 1 file changed, 5 deletions(-)
 delete mode 100644 toc.txt
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline toc.txt
fatal: ambiguous argument 'toc.txt': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline -- toc.txt
bfbb678 (HEAD -> master) Remove toc.txt
a642e12 Add header to all pages.
50db987 Include the first section in TOC.
ca49180 Initial commit.
tom@tom-ubuntu:~/Projects/Venus$ git checkout a642e12 toc.txt
Updated 1 path from 246d37c
tom@tom-ubuntu:~/Projects/Venus$ git status -s
A  toc.txt
tom@tom-ubuntu:~/Projects/Venus$ git commit -m "Restore toc.txt"
[master 61cf79f] Restore toc.txt
 1 file changed, 5 insertions(+)
 create mode 100644 toc.txt
```
We can use git blame to show who made the change to a file:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git blame audience.txt
a642e122 (Moshfegh Hamedani 2020-08-18 09:23:19 -0700 1) AUDIENCE 
a642e122 (Moshfegh Hamedani 2020-08-18 09:23:19 -0700 2) 
fb0d184c (Moshfegh Hamedani 2020-08-17 14:18:09 -0700 3) This course is for anyone who wants to learn Git. 
a642e122 (Moshfegh Hamedani 2020-08-18 09:23:19 -0700 4) No prior experience is required.
tom@tom-ubuntu:~/Projects/Venus$ git blame -e audience.txt
a642e122 (<moshfegh@live.com.au> 2020-08-18 09:23:19 -0700 1) AUDIENCE 
a642e122 (<moshfegh@live.com.au> 2020-08-18 09:23:19 -0700 2) 
fb0d184c (<moshfegh@live.com.au> 2020-08-17 14:18:09 -0700 3) This course is for anyone who wants to learn Git. 
a642e122 (<moshfegh@live.com.au> 2020-08-18 09:23:19 -0700 4) No prior experience is required.
tom@tom-ubuntu:~/Projects/Venus$ git blame -L 1,3 audience.txt
a642e122 (Moshfegh Hamedani 2020-08-18 09:23:19 -0700 1) AUDIENCE 
a642e122 (Moshfegh Hamedani 2020-08-18 09:23:19 -0700 2) 
fb0d184c (Moshfegh Hamedani 2020-08-17 14:18:09 -0700 3) This course is for anyone who wants to learn Git. 
```

WeWe can restore changes after they have been added:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline
61cf79f (HEAD -> master) Restore toc.txt
bfbb678 Remove toc.txt
a642e12 Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
tom@tom-ubuntu:~/Projects/Venus$ git tag v1.0 bfbb678
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline
61cf79f (HEAD -> master) Restore toc.txt
bfbb678 (tag: v1.0) Remove toc.txt
a642e12 Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

We can tag commits to make them easier to find:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git tag -a v1.1 -m "My version 1.1"
tom@tom-ubuntu:~/Projects/Venus$ git tag
v1.0
v1.1
tom@tom-ubuntu:~/Projects/Venus$ git tag -n
v1.0            Remove toc.txt
v1.1            My version 1.1
tom@tom-ubuntu:~/Projects/Venus$ git show v1.1
tag v1.1
Tagger: tom <tomspencerlondon@gmail.com>
Date:   Fri Apr 21 15:26:36 2023 +0100

My version 1.1

commit 61cf79fcc0d1b47775e29a04678edbae4390520c (HEAD -> master, tag: v1.1)
Author: tom <tomspencerlondon@gmail.com>
Date:   Fri Apr 21 15:22:10 2023 +0100

    Restore toc.txt

diff --git a/toc.txt b/toc.txt
new file mode 100644
index 0000000..cc0798f
--- /dev/null
+++ b/toc.txt
@@ -0,0 +1,5 @@
+TABLE OF CONTENT
+
+Creating Snapshots
+  - Initializing a repository
+  - Staging changes
\ No newline at end of file
tom@tom-ubuntu:~/Projects/Venus$ git tag -d v1.1
Deleted tag 'v1.1' (was 8412a7e)
tom@tom-ubuntu:~/Projects/Venus$ git tag
v1.0

```


### Branching
In this section we will learn:
- How to use branches
- Compare branches
- Merge branches
- Resolve merge conflicts
- Undo a faulty merge
- Essential tools (stashing, cherry picking)

#### What are branches?
![image](https://user-images.githubusercontent.com/27693622/233728158-a0e0d85b-c193-4d8e-969d-b34ba00de74f.png)

Branching allows us to diverge from the main line of work and continue to work without messing with the main line.
We complete our code on a separate feature branch and then when the work is finished we merge into master.
This keeps master as a clean line of work.

The master branch is a pointer to the last commit in the main line of work.
When we create a new branch, Git creates a new pointer to the same commit as the master branch.
When we commit, Git moves the pointer forward automatically. We can add a feature branch from the master branch at any point.
When we move to another branch git moves the head pointer to the latest commit in that branch.

![image](https://user-images.githubusercontent.com/27693622/233729047-49b8a177-dfd8-4e06-be24-89df8bf7d484.png)

We can create a branch with the following commands:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git branch bugfix
tom@tom-ubuntu:~/Projects/Venus$ git branch
  bugfix
* master
tom@tom-ubuntu:~/Projects/Venus$ git switch bugfix
Switched to branch 'bugfix'
tom@tom-ubuntu:~/Projects/Venus$ git branch -m bugfix bugfix/signup-form
tom@tom-ubuntu:~/Projects/Venus$ vi audience.txt
tom@tom-ubuntu:~/Projects/Venus$ git status
On branch bugfix/signup-form
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   audience.txt

no changes added to commit (use "git add" and/or "git commit -a")
tom@tom-ubuntu:~/Projects/Venus$ git add audience.txt 
tom@tom-ubuntu:~/Projects/Venus$ git commit -m "Fix bug preventing signup"
[bugfix/signup-form 7870993] Fix bug preventing signup
 1 file changed, 2 insertions(+), 3 deletions(-)
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline
7870993 (HEAD -> bugfix/signup-form) Fix bug preventing signup
3ba242d (master) add note on audience
2455eab add note for sales-page
710409d Edit gitignore to add files to ignore
61cf79f Restore toc.txt
bfbb678 (tag: v1.0) Remove toc.txt
a642e12 Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 (tag: v0.8) Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```
We can compare commits on the two branches:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log master..bugfix/signup-form 
commit 7870993d2d453a94d88081d72dedf3b2a6edf448 (bugfix/signup-form)
Author: tom <tomspencerlondon@gmail.com>
Date:   Fri Apr 21 21:33:25 2023 +0100

    Fix bug preventing signup

```
We can also compare the code on the two branches:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git diff master..bugfix/signup-form 
diff --git a/audience.txt b/audience.txt
index 38a393a..e7ebd24 100644
--- a/audience.txt
+++ b/audience.txt
@@ -1,5 +1,4 @@
-AUDIENCE 
+WHO THIS COURSE IS FOR
+===================== 
 
 This course is for anyone who wants to learn Git. 
-No prior experience is required.
-Developers and technology professionals will be the main audience.
```
We can also use a shorter comparison command:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git diff --name-status bugfix/signup-form 
M       audience.txt
```

We can stash changes:
```bash
tom@tom-ubuntu:~/Projects/Venus$ vi audience.txt 
tom@tom-ubuntu:~/Projects/Venus$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   audience.txt

no changes added to commit (use "git add" and/or "git commit -a")
tom@tom-ubuntu:~/Projects/Venus$ git stash push -m "New tax rules."
Saved working directory and index state On master: New tax rules.
tom@tom-ubuntu:~/Projects/Venus$ git status
On branch master
nothing to commit, working tree clean

```

We can also store different stashes:
```bash
tom@tom-ubuntu:~/Projects/Venus$ vi audience.txt 
tom@tom-ubuntu:~/Projects/Venus$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   audience.txt

no changes added to commit (use "git add" and/or "git commit -a")
tom@tom-ubuntu:~/Projects/Venus$ git stash push -m "New tax rules."
Saved working directory and index state On master: New tax rules.
tom@tom-ubuntu:~/Projects/Venus$ git status
On branch master
nothing to commit, working tree clean
tom@tom-ubuntu:~/Projects/Venus$ echo hello > newfile.txt
tom@tom-ubuntu:~/Projects/Venus$ git stash push -am "My new stash."
Saved working directory and index state On master: My new stash.
tom@tom-ubuntu:~/Projects/Venus$ git stash list
stash@{0}: On master: My new stash.
stash@{1}: On master: New tax rules.
tom@tom-ubuntu:~/Projects/Venus$ git switch bugfix/signup-form 
Switched to branch 'bugfix/signup-form'
tom@tom-ubuntu:~/Projects/Venus$ git switch master
Switched to branch 'master'
tom@tom-ubuntu:~/Projects/Venus$ git stash show 1
 audience.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
tom@tom-ubuntu:~/Projects/Venus$ git stash apply 1
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   audience.txt

no changes added to commit (use "git add" and/or "git commit -a")
tom@tom-ubuntu:~/Projects/Venus$ git stash list
stash@{0}: On master: My new stash.
stash@{1}: On master: New tax rules.
tom@tom-ubuntu:~/Projects/Venus$ git stash drop 1
Dropped refs/stash@{1} (9a851b8828ac798d7aede2e2b38b3ce5a17ee6eb)
tom@tom-ubuntu:~/Projects/Venus$ git stash drop 0
Dropped refs/stash@{0} (3a8ee40aea4b76f31e41c3f32310fee8f938ebd8)
```

### Merging
- fast forward merges
- 3 way merges

Fast forward merges are possible when there is only one branch and the branch is ahead of the master branch.
It brings the pointer of the master branch forwards.

In the following example the branches have diverged.

![image](https://user-images.githubusercontent.com/27693622/233733855-7d0ef22c-e724-4e95-8aae-e69f077fc340.png)

This is a 3 way merge. The master branch is the base branch. The other two branches are the head branches.
Git creates a new commit called a merge commit to combine the common ancestor and the tip of each branch.

We can view the branches with:
```bash
git log --oneline --all --graph
* 7870993 (bugfix/signup-form) Fix bug preventing signup
* 3ba242d (HEAD -> master) add note on audience
* 2455eab add note for sales-page
* 710409d Edit gitignore to add files to ignore
* 61cf79f Restore toc.txt
* bfbb678 (tag: v1.0) Remove toc.txt
* a642e12 Add header to all pages.
* 50db987 Include the first section in TOC.
* 555b62e Include the note about committing after staging the changes.
* 91f7d40 (tag: v0.8) Explain various ways to stage changes.
* edb3594 First draft of staging changes.
* 24e86ee Add command line and GUI tools to the objectives.
* 36cd6db Include the command prompt in code sample.
* 9b6ebfd Add a header to the page about initializing a repo.
* fa1b75e Include the warning about removing .git directory.
* dad47ed Write the first draft of initializing a repo.
* fb0d184 Define the audience.
* 1ebb7a7 Define the objectives.
* ca49180 Initial commit.
```
This shows a linear path so we can use the fast-forward merge:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git merge bugfix/signup-form 
Updating 3ba242d..7870993
Fast-forward
 audience.txt | 5 ++---
 1 file changed, 2 insertions(+), 3 deletions(-)
```

We can also use the --no-ff option to force a merge commit:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git merge --no-ff bugfix/login
hint: Waiting for your editor to close the file... CompileCommand: exclude com/intellij/openapi/vfs/impl/FilePartNodeRoot.trieDescend bool exclude = true
Merge made by the 'ort' strategy.
 toc.txt | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
```

### Three way merges

Here we have made commits on two separate branches:
```bash
tom@tom-ubuntu:~/Projects/Venus$ vi objectives.txt 
tom@tom-ubuntu:~/Projects/Venus$ git add objectives.txt 
tom@tom-ubuntu:~/Projects/Venus$ git commit -m "Edit objectives.txt"
[master 879bde6] Edit objectives.txt
 1 file changed, 2 insertions(+), 2 deletions(-)
tom@tom-ubuntu:~/Projects/Venus$ git log --oneline --all --graph
* 879bde6 (HEAD -> master) Edit objectives.txt
| * dcabad0 (feature/change-password) Build password form
|/  
*   16e20eb Merge branch 'bugfix/login'
|\  
| * 2b4b44b (bugfix/login) Add table of content edit
|/  
* 7870993 (bugfix/signup-form) Fix bug preventing signup
| * 3e36f77 (refs/stash) WIP on master: 3ba242d add note on audience
|/| 
| * 754d6f0 index on master: 3ba242d add note on audience
|/  
* 3ba242d add note on audience
* 2455eab add note for sales-page
* 710409d Edit gitignore to add files to ignore
* 61cf79f Restore toc.txt
* bfbb678 (tag: v1.0) Remove toc.txt
* a642e12 Add header to all pages.
* 50db987 Include the first section in TOC.
* 555b62e Include the note about committing after staging the changes.
* 91f7d40 (tag: v0.8) Explain various ways to stage changes.
* edb3594 First draft of staging changes.
* 24e86ee Add command line and GUI tools to the objectives.
* 36cd6db Include the command prompt in code sample.
* 9b6ebfd Add a header to the page about initializing a repo.
* fa1b75e Include the warning about removing .git directory.
* dad47ed Write the first draft of initializing a repo.
* fb0d184 Define the audience.
* 1ebb7a7 Define the objectives.
* ca49180 Initial commit.

```
The branches are said to have diverged. We have to run a three way merge:
```bash
git merge feature/change-password
```

We can now show how the tip of each branch have now been merged:
```bash

tom@tom-ubuntu:~/Projects/Venus$ git log --oneline --all --graph
*   4201cab (HEAD -> master) Merge branch 'feature/change-password'
|\  
| * dcabad0 (feature/change-password) Build password form
* | 879bde6 Edit objectives.txt
|/  
*   16e20eb Merge branch 'bugfix/login'
|\  
| * 2b4b44b (bugfix/login) Add table of content edit
|/  
* 7870993 (bugfix/signup-form) Fix bug preventing signup
| * 3e36f77 (refs/stash) WIP on master: 3ba242d add note on audience
|/| 
| * 754d6f0 index on master: 3ba242d add note on audience
|/  

```

We can view merged branches with:
```bash
git branch --merged
```
We can also check unmerged branches with:
```bash
git branch --no-merged
```

### Conflicts
- change1, change2
- change, delete
- Add1, Add2

#### Undoing a faulty merge
![image](https://user-images.githubusercontent.com/27693622/233746819-51490a54-bf5f-4cb5-b1a3-fd836faa45d7.png)

We can reset or delete the merge conflict locally:
```bash
git reset --hard HEAD~1
```
The merge commit is deleted and the branch is reset to the commit before the merge. We should only do this if we haven't shared our history
with anyone else.

Sometimes we merge and we find that the code does not compile or code does not work as expected. We can undo the merge with:
```bash
git revert -m 1 HEAD
```

We can use squash merging with shortlived branches:

```bash
git merge --squash bugfix/photo-upload
```
We should delete the branch following the squash merge:
```bash
git branch -D bugfix/photo-upload
```

### Rebase
We can rebase a branch onto another branch:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git log --all --oneline --graph
* b7a302b (HEAD -> master) update toc.txt
| * 1bed238 (feature/shopping-cart) add cart.txt
|/  
* 6d88063 Fix the bug on the photo upload page.
* 872c064 ignore .idea files
* e712b69 fix conflict
* 7782e40 add master
*   588f8a8 Merge branch 'bugfix/change-password'
```
With rebase we move the base of feature onto the top of the master branch:
```bash
tom@tom-ubuntu:~/Projects/Venus$ git switch feature/shopping-cart 
Switched to branch 'feature/shopping-cart'
tom@tom-ubuntu:~/Projects/Venus$ git rebase master
Successfully rebased and updated refs/heads/feature/shopping-cart.
tom@tom-ubuntu:~/Projects/Venus$ git log --all --graph --oneline
* 18072b4 (HEAD -> feature/shopping-cart) add cart.txt
* b7a302b (master) update toc.txt
* 6d88063 Fix the bug on the photo upload page.
* 872c064 ignore .idea files
* e712b69 fix conflict
* 7782e40 add master
*   588f8a8 Merge branch 'bugfix/change-password'
```
The history is now linear.

We can also cherry-pick commits:
```bash
git cherry-pick 78ad906
```
This applies the commit to the current branch:

```bash
git log --oneline --all --graph
* 8f1a284 (HEAD -> master) write mountain to toc.txt
* ad8744f update toc.txt
| * 78ad906 (feature/shopping-cart) write mountain to toc.txt
|/  
* 18072b4 add cart.txt
* b7a302b update toc.txt
* 6d88063 Fix the bug on the photo upload page.
* 872c064 ignore .idea files
* e712b69 fix conflict
* 7782e40 add master
```
We have applied the commit on the other branch to the current branch.

### Collaboration
- collaboration workflows
- pushing, fetching and pulling
- pull requests, issues and milestones
- contributing to open source projects

#### Workflows
- centralized
  - single repository
- distributed
  - every dev has a repository
- centralized workflow
  - centralized repository to syncrhonise work
- feature branch workflow
  - each feature is developed on a separate branch
  - branches are merged into master
  - branches are deleted after merging
  - no single point of failure
- repository
  - private server
  - hosting cloud services
- integration manager workflow
  - integration manager has write access to the repository
  - integration manager merges branches into master
  - integration manager deletes branches after merging
  - integration manager is a bottleneck
  - integration manager is a single point of failure

#### Sharing tags
We can share tags with:
```bash
tom@tom-ubuntu:~/Projects/Mars$ git tag v1.0
tom@tom-ubuntu:~/Projects/Mars$ git log --oneline
23f4c68 (HEAD -> main, tag: v1.0, origin/main) add file 1
99fb8db Update README
340c6cf Update README.md
70c70ec Update README.md
8fc6c2e Update README.md
e95b243 first commit
tom@tom-ubuntu:~/Projects/Mars$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:TomSpencerLondon/Mars.git
 * [new tag]         v1.0 -> v1.0
```
We can delete tags on origin with:
```bash
tom@tom-ubuntu:~/Projects/Mars$ git push origin --delete v1.0
To github.com:TomSpencerLondon/Mars.git
 - [deleted]         v1.0
```
We can delete them locally with:
```bash
tom@tom-ubuntu:~/Projects/Mars$ git log --oneline
23f4c68 (HEAD -> main, tag: v1.0, origin/main) add file 1
99fb8db Update README
340c6cf Update README.md
70c70ec Update README.md
8fc6c2e Update README.md
e95b243 first commit
tom@tom-ubuntu:~/Projects/Mars$ git tag -d v1.0
Deleted tag 'v1.0' (was 23f4c68)
tom@tom-ubuntu:~/Projects/Mars$ git log --oneline
23f4c68 (HEAD -> main, origin/main) add file 1
99fb8db Update README
340c6cf Update README.md
70c70ec Update README.md
8fc6c2e Update README.md
e95b243 first commit
```
We can add releases with tags on github:
![image](https://user-images.githubusercontent.com/27693622/233861334-0e3a4af2-4b70-402c-be7b-42b5a839c605.png)

#### Pushing a local branch

We can push a local branch to origin with:
```bash
tom@tom-ubuntu:~/Projects/Mars$ git branch -vv
* feature/change-password 23f4c68 add file 1
  main                    23f4c68 [origin/main] add file 1
tom@tom-ubuntu:~/Projects/Mars$ git branch -r
  origin/main
tom@tom-ubuntu:~/Projects/Mars$ git push -u origin feature/change-password
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'feature/change-password' on GitHub by visiting:
remote:      https://github.com/TomSpencerLondon/Mars/pull/new/feature/change-password
remote: 
To github.com:TomSpencerLondon/Mars.git
 * [new branch]      feature/change-password -> feature/change-password
branch 'feature/change-password' set up to track 'origin/feature/change-password'.
```

### Rewriting history
- Why and when to rewrite history
- Undo or revert commits
- Use interactive rebasing to rewrite history
- Recover lost commits

#### Why rewrite history
- History is for what was changed why and when
Bad history:
- poor commit messages
- large commits
- small commits

We want a clean readable history to tell the story of the project from day one.

#### Tools
- squash small, related commits
- split large commits
- reword commit messages
- drop unwanted commits
- modify commits

#### The Golden Rule of Rewriting history
- Don't rewrite history that has been shared with others
Commits in git are immutable. We can't change them. We can only create new commits that reference the old ones.

This is the history of our project:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline --all --graph
* 088455d (HEAD -> master) .
* f666091 WIP
* 111bd75 Update terms of service and Google Map SDK version.
* 72856ea WIP
* 8441b05 Add a reference to Google Map SDK.
* 8527033 Change the color of restaurant icons.
* af26a96 Fix a typo.
* 6fb2ba7 Render restaurants the map.
* 70ef834 Initial commit
```
There are a few issues with the history. There is a typo in "Render restaurants the map.", the WIP commit is noisy and the fix typo
are noisy commits so we can change the messages or drop the commits. There is also a commit that we may want to split into two
commits: "Update terms of service and Google Map SDK version.".

#### Undoing commits
If the commit has been merged we can use git revert HEAD otherwise we can use reset:
```bash
git reset --hard HEAD~1
```
For git reset the options are:
- --soft: reset the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and
  HEAD is updated to the specified commit.
- --mixed: reset the index and working tree. Any changes to tracked files in the working tree since <commit> are preserved
  but not marked for commit. (This is the default.)
- --hard: reset the index and working tree. Any changes to tracked files in the working tree since <commit> are discarded.

This is soft:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git show HEAD
commit 088455d5a7660595eb4b73a7b9dfe07d53f1260d (HEAD -> master)
Author: Moshfegh Hamedani <moshfegh@live.com.au>
Date:   Thu Sep 10 09:28:40 2020 -0700

    .

diff --git a/terms.txt b/terms.txt
index 6ab9fed..63cbee7 100644
--- a/terms.txt
+++ b/terms.txt
@@ -1 +1,2 @@
 completed
+TEST
tom@tom-ubuntu:~/Projects/Mercury$ git reset --soft HEAD~1
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline --all --graph
* f666091 (HEAD -> master) WIP
* 111bd75 Update terms of service and Google Map SDK version.
* 72856ea WIP
* 8441b05 Add a reference to Google Map SDK.
* 8527033 Change the color of restaurant icons.
* af26a96 Fix a typo.
* 6fb2ba7 Render restaurants the map.
* 70ef834 Initial commit
tom@tom-ubuntu:~/Projects/Mercury$ git status -s
M  terms.txt
```

#### Revert
We can revert a commit with:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline --all --graph
* f666091 (HEAD -> master) WIP
* 111bd75 Update terms of service and Google Map SDK version.
* 72856ea WIP
* 8441b05 Add a reference to Google Map SDK.
* 8527033 Change the color of restaurant icons.
* af26a96 Fix a typo.
* 6fb2ba7 Render restaurants the map.
* 70ef834 Initial commit
tom@tom-ubuntu:~/Projects/Mercury$ git revert HEAD~3..HEAD
```
This will revert HEAD, 111bd75 and 72856ea. 

This is noisy so we can reset the change:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline --all --graph
* c7295e4 (HEAD -> master) Revert "WIP"
* dd018df Revert "Update terms of service and Google Map SDK version."
* e83c6e8 Revert "WIP"
* f666091 WIP
* 111bd75 Update terms of service and Google Map SDK version.
* 72856ea WIP
* 8441b05 Add a reference to Google Map SDK.
* 8527033 Change the color of restaurant icons.
* af26a96 Fix a typo.
* 6fb2ba7 Render restaurants the map.
* 70ef834 Initial commit
tom@tom-ubuntu:~/Projects/Mercury$ git reset --hard HEAD~3
HEAD is now at f666091 WIP
```
This is a less noisy revert:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git revert --no-commit HEAD~3..
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline --all --graph
* f666091 (HEAD -> master) WIP
* 111bd75 Update terms of service and Google Map SDK version.
* 72856ea WIP
* 8441b05 Add a reference to Google Map SDK.
* 8527033 Change the color of restaurant icons.
* af26a96 Fix a typo.
* 6fb2ba7 Render restaurants the map.
* 70ef834 Initial commit
```
We can complete the revert with git revert --continue or get out of the state with git revert --abort.

If we make a mistake we can undo the work with reflog:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git reset --hard HEAD~6
HEAD is now at af26a96 Fix a typo.
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline --all --graph
* af26a96 (HEAD -> master) Fix a typo.
* 6fb2ba7 Render restaurants the map.
* 70ef834 Initial commit
tom@tom-ubuntu:~/Projects/Mercury$ git reflog
af26a96 (HEAD -> master) HEAD@{0}: reset: moving to HEAD~6
14746c4 HEAD@{1}: commit: Revert bad code.
f666091 HEAD@{2}: reset: moving to HEAD~3
c7295e4 HEAD@{3}: revert: Revert "WIP"
dd018df HEAD@{4}: revert: Revert "Update terms of service and Google Map SDK version."
e83c6e8 HEAD@{5}: revert: Revert "WIP"
f666091 HEAD@{6}: reset: moving to HEAD
f666091 HEAD@{7}: reset: moving to HEAD
f666091 HEAD@{8}: reset: moving to HEAD~1
088455d HEAD@{9}: commit: .
f666091 HEAD@{10}: commit: WIP
111bd75 HEAD@{11}: commit: Update terms of service and Google Map SDK version.
72856ea HEAD@{12}: commit: WIP
8441b05 HEAD@{13}: commit: Add a reference to Google Map SDK.
8527033 HEAD@{14}: commit: Change the color of restaurant icons.
af26a96 (HEAD -> master) HEAD@{15}: commit: Fix a typo.
6fb2ba7 HEAD@{16}: commit: Render restaurants the map.
70ef834 HEAD@{17}: commit (initial): Initial commit
```
We can then use the reflog to reset to a previous state:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git reset --hard HEAD@{1}
HEAD is now at 14746c4 Revert bad code.
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline --all --graph
* 14746c4 (HEAD -> master) Revert bad code.
* f666091 WIP
* 111bd75 Update terms of service and Google Map SDK version.
* 72856ea WIP
* 8441b05 Add a reference to Google Map SDK.
* 8527033 Change the color of restaurant icons.
* af26a96 Fix a typo.
* 6fb2ba7 Render restaurants the map.
* 70ef834 Initial commit
```
We can amend changes to earlier commits with amend:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git commit --amend
hint: Waiting for your editor to close the file... CompileCommand: exclude com/intellij/openapi/vfs/impl/FilePartNodeRoot.trieDescend bool exclude = true
[master 6a21170] Render cafes on the map
 Date: Sun Apr 23 22:13:19 2023 +0100
 1 file changed, 2 insertions(+), 1 deletion(-)
```

We can now see the change on the commit:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git show HEAD
commit 6a21170c57efd58c4d7bcb4aee75c69d59d8dd1c (HEAD -> master)
Author: tom <tomspencerlondon@gmail.com>
Date:   Sun Apr 23 22:13:19 2023 +0100

    Render cafes on the map

diff --git a/map.txt b/map.txt
index ec02c61..d6d87ce 100644
--- a/map.txt
+++ b/map.txt
@@ -1 +1,2 @@
-red restaurants
+blue restaurants
+cafes
```
If we want to undo adding the file to the last commit we can do:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git reset --mixed HEAD~1
Unstaged changes after reset:
M	map.txt
tom@tom-ubuntu:~/Projects/Mercury$ git status -s
 M map.txt
?? file1.txt
tom@tom-ubuntu:~/Projects/Mercury$ git clean -fd
Removing file1.txt
```
We can then add and commit the file:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git add .
tom@tom-ubuntu:~/Projects/Mercury$ git commit -m "Render cafes on the map."
[master 37f3159] Render cafes on the map.
 1 file changed, 2 insertions(+), 1 deletion(-)
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline
37f3159 (HEAD -> master) Render cafes on the map.
14746c4 Revert bad code.
f666091 WIP
111bd75 Update terms of service and Google Map SDK version.
72856ea WIP
8441b05 Add a reference to Google Map SDK.
8527033 Change the color of restaurant icons.
af26a96 Fix a typo.
6fb2ba7 Render restaurants the map.
70ef834 Initial commit
tom@tom-ubuntu:~/Projects/Mercury$ git show HEAD
commit 37f315966a725267998d89bf059e3008c703e621 (HEAD -> master)
Author: tom <tomspencerlondon@gmail.com>
Date:   Sun Apr 23 22:18:45 2023 +0100

    Render cafes on the map.

diff --git a/map.txt b/map.txt
index ec02c61..d6d87ce 100644
--- a/map.txt
+++ b/map.txt
@@ -1 +1,2 @@
-red restaurants
+blue restaurants
+cafes
```

#### Amend earlier commits
We can edit earlier commits with rebase:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline
37f3159 (HEAD -> master) Render cafes on the map.
14746c4 Revert bad code.
f666091 WIP
111bd75 Update terms of service and Google Map SDK version.
72856ea WIP
8441b05 Add a reference to Google Map SDK.
8527033 Change the color of restaurant icons.
af26a96 Fix a typo.
6fb2ba7 Render restaurants the map.
70ef834 Initial commit
tom@tom-ubuntu:~/Projects/Mercury$ git rebase -i 8527033
```
This opens a text editor with the following:
```bash
edit 8441b05 Add a reference to Google Map SDK.
pick 72856ea WIP
pick 111bd75 Update terms of service and Google Map SDK version.
pick f666091 WIP
pick 14746c4 Revert bad code.
pick 37f3159 Render cafes on the map.

# Rebase 8527033..37f3159 onto 8527033 (6 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

We now change a file on this commit:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ echo license > license.txt
tom@tom-ubuntu:~/Projects/Mercury$ git add .
tom@tom-ubuntu:~/Projects/Mercury$ git commit --amend
hint: Waiting for your editor to close the file... CompileCommand: exclude com/intellij/openapi/vfs/impl/FilePartNodeRoot.trieDescend bool exclude = true
[detached HEAD bfa0651] Add a reference to Google Map SDK.
 Author: Moshfegh Hamedani <moshfegh@live.com.au>
 Date: Wed Sep 9 17:41:49 2020 -0700
 2 files changed, 2 insertions(+)
 create mode 100644 license.txt
 create mode 100644 package.txt

```

The graph now looks like this:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git log --oneline --all --graph
* bfa0651 (HEAD) Add a reference to Google Map SDK.
| * 37f3159 (master) Render cafes on the map.
| * 14746c4 Revert bad code.
| * f666091 WIP
| * 111bd75 Update terms of service and Google Map SDK version.
| * 72856ea WIP
| * 8441b05 Add a reference to Google Map SDK.
|/  
* 8527033 Change the color of restaurant icons.
* af26a96 Fix a typo.
* 6fb2ba7 Render restaurants the map.
* 70ef834 Initial commit

```
We now continue the rebase:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git rebase --continue
```
git show on the commit shows the changes:
```bash
tom@tom-ubuntu:~/Projects/Mercury$ git show bfa0651
commit bfa06512d06f347b32adbb0a082301739ec12385
Author: Moshfegh Hamedani <moshfegh@live.com.au>
Date:   Wed Sep 9 17:41:49 2020 -0700

    Add a reference to Google Map SDK.

diff --git a/license.txt b/license.txt
new file mode 100644
index 0000000..8da8489
--- /dev/null
+++ b/license.txt
@@ -0,0 +1 @@
+license
diff --git a/package.txt b/package.txt
new file mode 100644
index 0000000..7324ece
--- /dev/null
+++ b/package.txt
@@ -0,0 +1 @@
+Google Map 1.0.0
```

We can also split commits with rebase with the following commands:
```bash
git rebase -i f9162d5^
git log --oneline --all --graph
git reset HEAD^
git status -s
git add package.txt
git commit -m "update google map sdk version 1.0 - 2.0"
git log --oneline --all --graph
git add terms.txt
git commit -m "add terms of service"
```