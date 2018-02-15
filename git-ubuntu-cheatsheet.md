# GIT on Ubuntu Cheatsheet

This cheatsheet provides a collection of commonly used GIT commands on an Ubuntu based system.

## Getting Started

### Installation

```bash
sudo apt-add-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
git --version
```

### Create Repository

* Create new folder 'recipes' and change path to new 'recipes' folder

  ```bash
  mkdir recipes && cd recipes
  ```

* Create empty repository ('.git' hidden folder is created)

  ```bash
  git init
  ```

* Set the username to be attached to commits

  ```bash
  git config user.name "bob"
  ```

* Set the email address to be attached to commits

  ```bash
  git config user.email "bob@somewhere.com"
  ```

* Set the editor to be used with git edits

  ```bash
  git config core.editor vim
  ```

* Set the tool to be used with git merges

  ```bash
  git config merge.tool meld
  ```

* Set the default LF formatting

  ```bash
  git config core.autocrlf input
  ```

* Enable colourization

  ```bash
  git config color.ui always
  ```

* Set push default

  ```bash
  git config push.default simple
  ```

* The first commit of a repository can not be rebased like regular commits, so it’s good practice to create an empty commit as your repository root

  ```bash
  git commit -m "root"
  ```

* Create empty readme markdown file

  ```bash
  touch README.md
  ```

* Append some content to README.md file

  ```bash
  echo "# Recipes README" >> README.md
  ```

* Display contents of README.md file

  ```bash
  cat README.md
  ```

* Display all new or modified files (changes)

  ```bash
  git status
  ```

* Add all current changes to next commit

  ```bash
  git add .
  ```

  OR

  Specifically add README.md to next commit

  ```bash
  git add README.md
  ```

* Commit all current changes

  ```bash
  git commit -m "Add README"
  ```

* Link local repository to a remote (like github, gitlab, bitbucket, tfs etc) repository

  ```bash
  git remote add origin [url]
  ```

* Push all changes to remote repository

  ```bash
  git push -u origin master
  ```

---

## Configuration

Git configuration can be managed at 3 levels of specificity:

* Local - applies only to current git repository
* Global - applies to all git repositories for the current user
* System - applies to all git repositories for all users

### Local Configuration

Run the following commands via the terminal from the root of your git project (where the .git hidden folder resides) to view or edit a list of local settings.

#### View and Edit Local Config

Command | Description
--- | ---
cat ./.git/config | View local config
vim ./.git/config | Edit local config
git config --edit | Use default configured editor to edit local config

#### Get Local Config Settings

Command | Description
--- | ---
git config --list | List all git config settings
git config user.name | Get username config setting
git config user.email | Get email config setting
git config core.autocrlf | Get autocrlf (see note below) config setting
git config core.editor | Get editor config setting
git config merge.tool | Get merge tool config setting

#### Set Local Config Settings

Command | Description
--- | ---
git config user.name "bob" | Set username config setting
git config user.email "bob@bob.com" | Set email config setting
git config core.autocrlf input | Set autocrlf (see note below) config setting
git config core.editor vim | Set editor config setting
git config merge.tool meld | Set merge tool config setting

### Global Configuration

Run the following command via the terminal from any location

#### View and Edit Global Config

Command | Description
--- | ---
cat ~/.gitconfig | View global config
vim ~/.gitconfig | Edit global config
git config --global --edit | Use default configured editor to edit global config

#### Get Global Config Settings

Command | Description
--- | ---
git config --global --list | List all git config settings
git config --global user.name | Get username config setting
git config --global user.email | Get email config setting
git config --global core.autocrlf | Get autocrlf (see note below) config setting
git config --global core.editor | Get editor config setting
git config --global merge.tool | Get merge tool config setting

#### Set Global Config Settings

Command | Description
--- | ---
git config --global user.name "bob" | Set username config setting
git config --global user.email "bob@bob.com" | Set email config setting
git config --global core.autocrlf input | Set autocrlf (see note below) config setting
git config --global core.editor vim | Set editor config setting
git config --global merge.tool meld | Set merge tool config setting

### System Configuration

Run the following commands via the terminal from any location

First check that system wide config exists.

```bash
ls /etc/gitconfig
```

#### View and Edit System Config

Command | Description
--- | ---
cat /etc/gitconfig | View global config
vim /etc/gitconfig | Edit global config
git config --system --edit | Use default configured editor to edit system config

#### Get System Config Settings

Command | Description
--- | ---
git config --system --list | List all git config settings
git config --system user.name | Get username config setting
git config --system user.email | Get email config setting
git config --system core.autocrlf | Get autocrlf (see note below) config setting
git config --system core.editor | Get editor config setting
git config --system merge.tool | Get merge tool config setting

#### Set System Config Settings

Command | Description
--- | ---
git config --system user.name "bob" | Set username config setting
git config --system user.email "bob@bob.com" | Set email config setting
git config --system core.autocrlf input | Set autocrlf (see note below) config settinsystem
git config --system core.editor vim | Set editor config setting
git config --system merge.tool meld | Set merge tool config setting

#### A note on autocrlf

One can instruct Git to convert CRLF to LF on commit but not the other way around by setting core.autocrlf to input. This setup means that one can use CRLF endings in Windows checkouts, but with LF endings on Mac and Linux systems. In order to do this, run any one of the following commands depending on required specificity.

Command | Specificity
--- | ---
git config core.autocrlf input | local
git config --global core.autocrlf input | global
git config --system core.autocrlf input | system

### Alias Configuration

* Create alias to display log summary of commit history

  ```bash
  git config --global alias.log-summary "log --all --pretty=format:'%h %ad - %s%d [%an]' --graph --date=short"
  ```
* Create alias to display commit history as a graph

  ```bash
  git config --global alias.log-graph "log --oneline --decorate --graph"
  ```

* Resetting HEAD pointer to previous commit and preserve all changes as unstaged changes

  ```bash
  git config --global alias.unstage "reset HEAD --"
  ```
---

## Commands

### Create Repositories

Command | Description
--- | ---
git init | created new local repository in current directory
git init [project-name] | create new local repository with specified name
git clone [url] | downloads a project and its entire version history

### Manage Local Changes

Command | Description
--- | ---
git status | Lists all new or modified files to be committed
git status -u | Like *git status*, but also lists all untracked files even files inside directories)
git status --ignored | List all files and folders that are currently ignored (based on .gitignore file)
git add . | add all new and modified files to next commit
git add . -n | do dry run for add all new and modified files to next commit
git add [file-name] [file-name] | adds specified files to next commit
git commit -m "descriptive message" | records file snapshots permanently n version history
git commit -m "descriptive message" --amend | add current changes to previous commit
git commit --amend --no-edit | add current changes to previous commit using message from previous commit
git log @{u}.. | display a list of pending commits (commits that have not been pushed)

### Undo Changes

#### git revert

Using *'git revert'* is a safe way of undoing commits. Instead of removing a commit, a new commit is created with all the changes undone. Use *'git revert'* when you want to remove a specific commit from the history but you still wish to preserve any changes from that commit.

Command | Description
--- | ---
git revert [commit] | undo specified commit

#### git reset

Using *'git reset'* is essentially a permanent undo meaning that there is no way to access original changes.

Command | Description
--- | ---
git reset HEAD -- [file] | Unstage all changes to previous commit but eave working directory unchanged. The '--' is used to separate paths from revisions
git reset [file] | Equivalent to above as HEAD (previous commit) is ptional and is used by default
git reset --hard | Unstage all changes to match working directory of last ommit. All uncommited changes are lost
git reset [commit] | Unstage all changes to specified commit but preserve uncommited changes
git reset --hard [commit] | Unstage all changes to match working directory of specified commit. All uncommited changes are lost

### Synchronize Changes

Command | Description
--- | ---
git remote -v | show list of remotes
git remote show [remote] | show information about remote
git remote add [short-name] [url] | add new remote repository named *[short-name]*
git push -u origin --all | push local repository to remote
git push | push local changes to remote
git pull | download changes and merge into HEAD
git fetch | download object and refs
git fetch origin | get data only from origin
git fetch --all | get data from all remotes
git fetch --all --prune | get data for all remotes and remove all deleted data

### Manage Branching

Command | Description
--- | ---
git branch | show list of local branches
git branch -r | show list of remote branches
git branch -a | show list of both local and remote branches
git branch -v | show list of branches along with details of last commit on each branch
git branch -vv | like *git branch -v* but also shows which branches are tracked
git show-branch | shows the commit ancestry graph
git checkout [branch-name] | switch from current branch to *[branch-name]*. Switches HEAD branch
git checkout -b [branch-name] | create new branch called *[branch-name]* and switch to it
git branch --merged | see which branches are already merged into the branch you’re on
git branch --no-merged | see all the branches that contain work you haven’t yet merged in
git branch -d [branch-name] | safe delete *[branch-name]*. will not delete branch if there are any uncommited changes
git branch -D [branch-name] | force delete *[branch-name]* ignoring any uncommitted changes
git push --set-upstream origin [branch-name] | share and transfer *[branch-name]* to remote server
git merge [branch-name] | combines the specified branch’s history into the current branch
git push origin --delete [branch-name] | deletes remote branch called [branch-name]
git fetch && git checkout [branch-name] | checkout remote branch

### Manage Commits

Command | Description
--- | ---
git log @{u}.. | display a list of pending commits (commits that have not been pushed)
git cherry-pick abc123 | add specific commit (abc123) to current branch

### Manage Tags

Command | Description
--- | ---
git tag | show a list of existing tags
git tag -a V1.0 -m "Created V1.0 release." | create an annotated tag (the preferred approach)
git show tag V1.0 | show information relating to specified tag
git tag -d V1.0 | remove tag from repository
git checkout -b [branch-name] [tag-name] | You can’t really check out a tag in Git, since they can’t be moved around. If you want to put a version of your repository in your working directory that looks like a specific tag, you can create a new branch at a specific tag with '`git checkout -b [branch-name] [tag-name]`'
git push --set-upstream origin [tag-name] | share and transfer tag *[tag-name]* to remote server
git push --set-upstream origin --tags | share and transfer all tags to remote server

### GIT log

Command | Description
--- | ---
git log | display commit history
git log -10 | display last 10 commits
git log -p -1 | display differences in last commit
git log --pretty=oneline | short | full | fuller` | display commit history using specified format
git log --pretty=oneline -2 | display last 2 commits using one line per commit
git log --pretty=oneline --author='' | display commit history filtering by author
git log --pretty=oneline --since='5 minutes ago' | display commit history for last 5 minutes
git log --pretty=oneline --until='5 minutes ago' | display commit history until 5 minutes ago
git log --all --pretty=format:'%h %ad \| %s%d [%an]' --graph --date=short | custom log format
git log --oneline --decorate --graph | another custom log format

**Formats:**

* --pretty="..." defines the format of the output.
* %h is the abbreviated hash of the commit
* %d are any decorations on that commit (e.g. branch heads or tags)
* %ad is the author date
* %s is the comment
* %an is the author name
* --graph informs git to display the commit tree in an ASCII graph layout
* --date=short keeps the date format nice and short