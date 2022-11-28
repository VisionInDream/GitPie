# 1. Configuring Git – the command line

```bash
$ git config --global --edit

```

# First-Time Git Setup

* View all of your settings and where they are coming from using
```bash
$ git config --list --show-origin
```

* Setting up your identity
* You can omit  `--global` if you want to overide the names for a specific project
```bash
$ git config --global user.name "Paul Offei"
$ git config --global user.email "poffei@st.ug.edu.gh"
```

* Setting up your editor
```bash
$ git config --global core.editor vim
```

* Setting up your default branch name
```bash
$ git config --global init.defaultBranch main
```

* Checking for your settings
```bash
$ git config --list
```

* Checking for a specific settings
```bash
$ git config user.name
```

# 2. Git Basics

# Getting a Git Repository

* Initializing a Repository in an Existing Directory
```bash
$ cd vision/gitpie/
$ git init
$ git add .
$ git status .
$ git commit -m "my first commit"
```

* Cloning an Existing Repository
* using either ssh or https
```bash
$ git clone git@github.com:VisionInDream/GitPie.git
$ git clone https://github.com/VisionInDream/GitPie.git
$ git clone git@github.com:VisionInDream/GitPie.git gitpie
$ git clone https://github.com/VisionInDream/GitPie.git gitpie
```

* Recording Changes to the Repository
* Think of `git` as your mini record booking keeping for managing changes in files instead of customers
* You have divided the book into two part `track and untrack` 
* `track `section is where needed information are added and is ready to be stored in the main database or books of accout but can be remove, modified as well. (a.k.a stagging area for snap shot)
* `untrack`  section is a list of reciepts yet to added to the record book keeping (a.k.a unstagging area) 
  
* Checking the Status of Your Files
```bash
$ git status 
```

* Tracking New Files
```bash
$ git add list.py
$ git add love.py grace.py
$ git add .
```

* Staging Modified Files (love.py)
* New files that aren’t tracked have a ?? next to them, new files that have been added to the staging
area have an A, modified files have an M and so on

```bash
$ git status --short
$ git add love.py
$ git status -s
```

* Ignoring Files
* class of files that you don’t want Git to automatically add or even show you as
being untracked
```
# ignore all .a files
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
# ignore all files in any directory named build
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```
In the simple case, a repository might have a single `.gitignore` file in its root
directory, which applies recursively to the entire repository. However, it is also
possible to have additional `.gitignore` files in subdirectories. The rules in these
nested `.gitignore` files apply only to the files under the directory where they are
located. The Linux kernel source repository has 206 `.gitignore` files

```bash
$ cat .gitignore
```

* Viewing Your Staged and Unstaged Changes
* `git diff` by itself doesn’t show all changes made since your last
commit — only changes that are still unstaged
* If you’ve staged all of your changes, `git diff` will
give you no output.

```bash
$ git diff
```

* If you want to see what you’ve staged that will go into your next commit
```bash
$ git diff --staged
```

* `git diff --cached` to see what you’ve staged so far
```bash
$ git diff --cached
```

* Committing Your Changes
```bash
$ git commit
```

* Skipping the Staging Area
```bash
$ git commit -a 
```

* Removing Files
```bash
$ git rm love.py
$ git rm --cached love.py
```

* Moving Files
```bash
$ git mv love.py like.py
```

* Viewing the Commit History
```bash
$ git log
$ git log -p -2
$ git log --stat
$ git log --oneline --graph
```

* Limiting Log Output
```bash
$ git log --since=2.weeks
```

* Undoing Things
* If you want to redo that commit, make the additional
changes you forgot, stage them, and commit again using the `--amend option`

```bash
$ git commit --amend
```

* Unstaging a Staged File
```bash
$ git reset HEAD peace.py
```
Be careful with `git reset` because it operate on the working
directory, not on the committed snapshots


* Unmodifying a Modified File
```bash
git checkout -- love.py
```

* Unstaging a Staged File with git restore
```bash
$ git restore --staged love.py
```

* Unmodifying a Modified File with git restore
```bash
$ git restore love.py
```

* Working with Remotes
* Remote repositories are versions of your project that are hosted on the Internet or
network somewhere
* Collaborating with others involves managing these remote repositories and
pushing and pulling data to and from them when you need to share work

```bash
$ git remote
$ git remote -v
```

* Adding Remote Repositories
```bash
$ git remote add pb https://github.com/Beattitude/gitpie
$ git remote -v
$ git fetch pb
```

* Fetching and Pulling from Your Remotes
```bash
$ git fetch <remote>
$ git fetch origin
```
The command goes out to that remote project and pulls down all the data from that remote project
that you don’t have yet. After you do this, you should have references to all the branches from that
remote, which you can merge in or inspect at any time.
If you clone a repository, the command automatically adds that remote repository under the name
“origin”. So, git fetch origin fetches any new work that has been pushed to that server since you
cloned (or last fetched from) it. It’s important to note that the git fetch command only downloads
the data to your local repository — it doesn’t automatically merge it with any of your work or
modify what you’re currently working on. You have to merge it manually into your work when
You can use the git pull command to automatically fetch and then merge that
remote branch into your current branch. This may be an easier or more comfortable workflow for
you; and by default, the git clone command automatically sets up your local master branch to track
the remote master branch (or whatever the default branch is called) on the server you cloned from.
Running git pull generally fetches data from the server you originally cloned from and
automatically tries to merge it into the code you’re currently working on

* Pushing to Your Remotes
* When you have your project at a point that you want to share, you have to push it upstream

```bash
$ git push <remote> <branch>
$ git push origin main
```

* Inspecting a Remote
* If you want to see more information about a particular remote
```bash
$ git remote show origin
```

* Renaming and Removing Remotes
```bash
$ git remote rename pb paul
$ git remote
$ git remote remove paul
$ git remote
```

* Tagging
Git has the ability to tag specific points in a repository’s history as being important.
Typically, people use this functionality to mark release points (v1.0, v2.0 and so on)

* Listing Your Tags
* Just type `git tag` (with optional -l or --list)
```bash
$ git tag
$ git tag -l "v1.8.5*"
```

* Creating Tags
* Git supports two types of tags: lightweight and annotated.
* A lightweight tag is very much like a branch that doesn’t change — it’s just a pointer to a specific
commit.
* Annotated tags, however, are stored as full objects in the Git database
They’re checksummed;
contain the tagger name, email, and date; have a tagging message; and can be signed and verified
with GNU Privacy Guard (GPG). It’s generally recommended that you create annotated tags so you
can have all this information

* Annotated Tags
```bash
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
$ git show v1.4
```

* Lightweight Tags
To create a lightweight tag, don’t supply any of the -a, -s, or
-m options, just provide a tag name

```bash
$ git tag v1.4-lw
$ git tag
$ git show v1.4-lw
```

* Sharing Tags
```bash
$ git push origin v1.5
$ git push origin --tags # lot of tags
```

* Deleting Tags
```bash
$ git tag -d v1.4-lw
$ git push origin :refs/tags/v1.4-lw # git push <remote> :refs/tags/<tagname>
$ git push origin --delete <tagname> # Deleting in remote server
```

* Checking out Tags
If you want to view the versions of files a tag is pointing to, you can do a git checkout of that tag,
although this puts your repository in “detached HEAD” state, which has some ill side effects

```bash
$ git checkout v2.0.0
$ git checkout -b version2 v2.0.0 # making changes
```

* Git Aliases
Git doesn’t automatically infer your command if you type it in partially. If you don’t want to type
the entire text of each of the Git commands, you can easily set up an alias for each command using
`git config`. Here are a couple of examples you may want to set up

```bash
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```

This technique can also be very useful in creating commands that you think should exist. For
example, to correct the usability problem you encountered with unstaging a file, you can add your
own unstage alias to Git

```bash
$ git config --global alias.unstage 'reset HEAD --' # git unstage fileA
$ git config --global alias.last 'log -1 HEAD'
$ git config --global alias.visual '!gitk'  # git visual to run gitk
```
* creating a branch
```bash
$ git branch kojo
```
