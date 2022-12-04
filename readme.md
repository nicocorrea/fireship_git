# This are all GIT commands from the course in Fireship

git config --global user.name "Nicolas Correa"

git config --global user.email "correan10@gmail.com"

git config --list

git init

git status

"git add ." or "git add somefile.txt"

git reset . -> This will remove a file from the staging area.

git commit -m "message that goes with the commit"

git log -> Will show details on all past commits, and which one is HEAD.

git remote -> Will list all current remotes configured in the local repository

git remote add origin https://.......

git push origin main -u -> As saying push the main local branch to origin. And by adding only once the flag '-u', this allows to not need to specify 'origin main' when doing 'git pull'.

git fetch -> Will capture the changes from the remote repo compared to those from the local repo.

git merge origin/master -> Will merge those changes that fetched before. I can look in VS Code for the branches and I should see different commit identifiers if there's anything to merge from remote to local, after the 'git fetch' was executed.

git pull -> Will simply do both 'git fetch' and 'git merge'. It is safe to use this approach.

git clone repo-url local-directory -> Will clone the repo, and the local-directory specification is optional. If I put something (i.e. 'demo'), it will create a folder named 'demo' and then clone the repo inside it.

git branch -> Will list all branches.

git branch feature-10 -> Will create a branch named 'feature-10'

git branch -d feature-10 -> Will delete the branch if it has not been merged into the main branch. Capital D does not care about it.

git checkout feature-10 -> Will switch us from the current branch to that one (i.e. feature-10).

git checkout -b feature-10 -> Will create the branch and checkout to it directly.

git checkout - -> Will move us back to the latest branch I was in. This is in case I went to main and need to go back to the previous one and I forgot its name.
change at line 46
