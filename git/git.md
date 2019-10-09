links
https://rogerdudler.github.io/git-guide/
https://hackernoon.com/understanding-git-fcffd87c15a3

settings
git config --list --show-origin
git config --show-origin user.name

setup identity
git config --global user.name "Damian Jardim"
git config --global user.email dljardim@outlook.com

set editor to vscode
git config --global core.editor code

help
git help verb
git verb --help
man git-verb
git commit -h

## setup in current directory
mkdir my-project
cd my-project
git init

git add .
git add file.txt

git commit -m 'initial commit'

## clone in current directory
this creates a folder called 'github-project' 
git clone https://github.com/github-project/github-project

git clone https://github.com/github-project/github-project mydirectory


## commands
git status
git status --short (-s)

## .gitignore
templates: https://github.com/github/gitignore 
ignore lines starting with #
glob patterns
start / / end
! negate a pattern ! override previous pattern

changes made but not staged
staged but not commited

changes made which are unstaged ( does not compare to last commit)
git diff 

compares staged file to last commit
git diff --staged 

diff tools - compare emerge vimdiff
git difftool
git difftool --tool-help

## commit
git commit -m "initial commit"

add files to staging automatically when modified
git commit -a


## remove

dont track file
git rm filename.txt
git rm --cached filename.txt

remove all files in the log directory with .log extension ( need \ when using *)
git rm log/\*.log


# moving files
rename a file
git mv from.txt to.txt
(or)
mv from.txt to.txt
git rm from.txt
git add to.txt


# commit history
git log
git log -2

include the differences (git diff)
git log --patch (-p) 

list of files changed / added / removed - summary at end
git log --stat

git log --pretty=oneline
git log --pretty=short
git log --pretty=full
git log --pretty=fuller

customize output
git log --pretty=format:"%h - %an, %ar : %s"

git log --since=2.weeks

git log -S function_name

changing last commit message
git commit --amend

replace last commit 
git commit -m 'initial comment'
git add forgotten_file
git commit --amend

unstage file that is currently staged
git reset HEAD file.txt

unmodify file - replace file to last commit version
git checkout -- file.txt

# remote repo
remote repo can be on local machine

show remotes
git remote

origin = default name of repo cloned from
cloned repo - show origin of cloned repo - sever cloned from
git clone https://github.com/proj1/proj1
cd proj1
git remote
git remote -v

add remote repo
git remote add _shortname _url
git remote add pb https://github.com/paulboone/ticgit

shortname can be used on the commandline instead of url
git fetch _shortname
(shortname)/(branch) _shortname/master


get all data from remote - does not merge
git fetch <remote>

pull = fetch + merge
git pull 

git clone
- set up local master branch to track remote master branch
git pull 
- fetches data from server cloned from then merge

pushing to remote
git push <remote><branch>
git push origin master
must fetch new changes before pushing yours

list other pulls origin (master pushes to master (up to date))
if not update

git remote show - shows current push and pull branch config

change remote shortname
git remote rename oldname newname

remove remote
git remote remove shortname

tag - annotated tags
git tag -a v1.4 -m "my version 1.4"
light
git tag tagname

send 1 / all tags to remote server
git push origin tagname
git push origin --tags

delete tag local / remote
git tag -d tagname
git push origin --delete tagname

# git alias ?
git config --global alias.aliasname 'reset HEAD --' 
git config --global alias.last 'log -1 HEAD'

run external command in alias ( ! )
git config --global alias.visual '!gitk'

# branching

git branch newbranch

switch branch
git checkout testing
git checkout master
- moves HEAD

HEAD - pointer to the local branch you're working on

# merge commit ??


# remote repo / remote tracking branches

add remote reference to other git servers
git remote add remote-repo
git fetch remote-repo

## pushing

to push requires write access
git push _remote_ _branch_
git push origin other-branch

refs/heads/serverfix:refs/heads/serverfix
(local)serverfix:(remote)serverfix
refs/heads/  = git internals

git push origin serverfix
git push origin serverfix:serverfix

- use if branch names differ
(local) = differentname
(remote) = serverfix
source:destination 
git push origin differentname:serverfix 
git push origin serverfix:awesomebranch


## remote tracking branch
set local branch - to a remote branch
-u 
--set-upstream-to

set local branch to a remote branch -
git branch -u origin/serverfix

git checkout --track origin/serverfix

cloning creates a tracking branch 'master' that tracks origin/master

tracking branch that uses a different remote (not origin)
tracking branch that does not track the master branch

create local branch 'mybranch'
git branch -u origin/mybranch

git branch -vv
'ahead by 2' - we have 2 commits locally that are not pushed to the server