# **GIT Course**

> git config --global user.name "Nicolas Correa"
>
> git config --global user.email "correan10@gmail.com"
>
> git config --list
>
> git init
>
> git status
>
> "git add ." or "git add somefile.txt"

This will remove a file from the staging area:

> git reset .
>
> git commit -m "message that goes with the commit"

Will show details on all past commits, and which one is HEAD:

> git log

and if I would like to have a better view of it, I'd rather use:

> git log --graph --oneline --decorate

Will list all current remotes configured in the local repository:

> git remote
>
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

---

## **HOW MERGE CONFLICTS HAPPEN**

We create a branch and go to it

> git branch feature-10
>
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

> git commit -am 'changed bla bla bla'
>
> git push origin main

If I choose to abort the merge I can use

> git merge --abort

---

**NOTE**: Forking a repo will copy that repo to your Github account. It maintains a link to the original repo so you can fetch updates, and will set-up as the upstream.

A common thing is that developers may then submit a PR to merge that code into the original, and then the author will decide whether to accept it or not.

---

## **MORE ON GIT RESET**

If I want to unstaged a file that was staged, as explained before I use one of these two:

> git reset filename.txt
>
> git reset .

BUT, I can also go back to a previous commit if I also committed a wrong file, and not just staged it. I can do that by looking at the id of that previous commit:

> git log

and then using:

> git reset the-id-of-the-commit

This way I will go back to seeing all the files along with the modifications I did. Here's a more advanced and dangerous way. If I want to go back to that previous commit AND forget about all changes (including new files I might have created) I can use the following command, and it will destroy them (= no delta). This MUST NOT be used if those commit has already been pushed as it will otherwise will create a situation where developers will be working on code that most probably no longer will be there after you push the new commit you will create without them:

> git reset --hard the-id-of-the-commit

**What about GIT REVERT?**

There is a command that will allow you to still revert changes, should you have pushed those to the remote repo. Compared to 'git reset' this command will DO NOT remove the wrong commit-id but leave it in the log, and create a new commit-id with the previous (healthy) commit instead.

> git revert the-id-of-the-commit-that-I-want-to-remove

**PAY ATTENTION** here because in the 'git reset' I use the commit-id that I want to go back to, whereas in 'git revert' I use the commit-id that I want to remove.

---

## **GIT AMEND**

If I need to amend the message of a commit I can use:

> git commit --amend -m "better message"

And if I forgot to add a file, instead of using 'git reset' I can use:

> git add filename.txt
>
> git commit --amend --no-edit

---

## **GIT STASH**

If you want to save your work for later, whether it was staged already or not, without committing it, like something experimental to work on later, you can use the following command which will delete AND save the changes in a list of stashes:

> git stash

Using it this way allows you to associate a name to it:

> git stash save cool-stuff

And I can go back to it by using either 'pop' which will get the most recent item in the list, or else the 'apply' follow by the index of the stash in the list.

> git stash pop
>
> git stash apply 1

---

## **GIT REBASE**

From a feature branch, rebase the latest changes from the master branch. This makes it look like I started working on this feature from the code on the latest commit on the main branch.

> git checkout feature-branch
>
> git rebase

**NOTE**: Considering what this means when working with teams, it might be safer to create an extra branch from the current feature, do rebase there, and if all works well, remove the temporary feature branch and rebase my feature branch, and continue from there.

---

## **GIT SQUASH**

If I have been creating a couple of commits that were simple changes, it may not make much sense to push all as this will show all of them in the remote repo and maybe more work for the understanding of what's been added in between them (and why).

> git rebase -i origin/main

**NOTE**: The 'origin/main' here is eventually those two that need to be rebased. It can be origin/feature-branch.

this is the test branch

This is added into main branch.. motherfuckeeeeer.

This is a new motherfuckeeeeeer.

One commit.

Two commit.
