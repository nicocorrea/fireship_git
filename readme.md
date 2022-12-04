# GIT Course

> git config --global user.name "Nicolas Correa"

> git config --global user.email "correan10@gmail.com"

> git config --list

> git init

> git status

> "git add ." or "git add somefile.txt"

This will remove a file from the staging area:

> git reset .

> git commit -m "message that goes with the commit"

Will show details on all past commits, and which one is HEAD:

> git log

Will list all current remotes configured in the local repository:

> git remote

> git remote add origin https://.......

As saying push the main local branch to origin. And by adding only once the flag '-u', this allows to not need to specify 'origin main' when doing 'git pull':

> git push origin main -u

Will capture the changes from the remote repo compared to those from the local repo:

> git fetch

Will merge those changes that fetched before. I can look in VS Code for the branches and I should see different commit identifiers if there's anything to merge from remote to local, after the 'git fetch' was executed:

> git merge origin/master

Will simply do both 'git fetch' and 'git merge'. It is safe to use this approach:

> git pull

Will clone the repo, and the local-directory specification is optional. If I put something (i.e. 'demo'), it will create a folder named 'demo' and then clone the repo inside it:

> git clone repo-url local-directory

Will list all branches:

> git branch

Will create a branch named 'feature-10':

> git branch feature-10

Will delete the branch if it has not been merged into the main branch. Capital D does not care about it:

> git branch -d feature-10

Will switch us from the current branch to that one (i.e. feature-10):

> git checkout feature-10

Will create the branch and checkout to it directly:

> git checkout -b feature-10

Will move us back to the latest branch I was in. This is in case I went to main and need to go back to the previous one and I forgot its name:

> git checkout -

<br>

## HOW MERGE CONFLICTS HAPPEN

We create a branch and go to it

> git branch feature-10 <br>
> git checkout feature-10

We modify for example line 10 in a file and commit it

> git commit -am 'modified bla bla'

We go to main

> git checkout main

We modify the same line in the same file and commit it

> git commit -am 'modified bla bla bla'

When we merge, we get a conflict, and VS Code will show it.

> git merge feature-10

We can check the difference also via command line

> git diff

Once the merge conflict is solved (i.e. using VS Code) I need to commit again the resolution I chose

> git commit -am 'changed bla bla bla' <br>
> git push origin main

If I choose to abort the merge I can use

> git merge --abort

<hr>
<u>NOTE</u>: Forking a repo will copy that repo to your Github account. It maintains a link to the original repo so you can fetch updates, and will set-up as the upstream.

A common thing is that developers may then submit a PR to merge that code into the original, and then the author will decide whether to accept it or not.

<hr>

## MORE ON GIT RESET

<br>
If I want to unstaged a file that was staged, as explained before I use one of these two:

> git reset filename.txt <br>
> git reset .

BUT, I can also go back to a previous commit if I also committed a wrong file, and not just staged it. I can do that by looking at the id of that previous commit:

> git log

and then using:

> git reset the-id-of-the-commit

This way I will go back to seeing all the files along with the modifications I did. Here's a more advanced and dangerous way. If I want to go back to that previous commit AND forget about all changes (including new files I might have created) I can use the following command, and it will destroy them (= no delta). This MUST NOT be used if those commit has already been pushed as it will otherwise will create a situation where developers will be working on code that most probably no longer will be there after you push the new commit you will create without them:

> git reset --hard the-id-of-the-commit

<br>
<b> What about GIT REVERT? </b>

There is a command that will allow you to still revert changes, should you have pushed those to the remote repo. Compared to 'git reset' this command will do not remote the wrong commit-id but leave it in the log, and create a new commit-id with the previous (healthy) commit instead.

> git rever the-id-of-the-commit-that-I-want-to-remove
