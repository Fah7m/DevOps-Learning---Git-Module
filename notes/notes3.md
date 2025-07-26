Hands on git notes 
---

Installing git on terminal is done by 

```
sudo apt-get install git
```

Configuring git identity

```
git config --global user.name "usernamehere"

git config --global user.email "email@here.com"
```

Important command to generate a ssh key is here

```
ssh-keygen -t ed25519 -C "email@here.com" -f ~/.ssh/nameofkey

```
Cat the .pub key and copy it to create the ssh key in the github settings > ssh key > add new ssh key


To test login

```
ssh -T git@github.com
```

To initialise a local directory on your pc do 

```
git init
```

Now that this directory is initialised we can create files in here etc but can't push anything to a github repo yet


If I create  a file and do the below, I can see the status or what has happened.

```
git status
```

This will commit the file and add a message for the commit
```
git commit -m "init commit"
```

This command allows you to create a branch and switch between branches 
```
git checkout -b branchname - to create a branch

git checkout main - to switch to a branch
```


**Workflow to follow when adding, committing and push is this** 
```
touch app.txt

git status - to check the status of the file

git add app.txt - this will add the app.txt to staging area

git status - this again to check if its there

git commit -m "commit message" - this will commit it before the final step

git push - this pushes the file onto your github repo.
```



This will allow you to merge branches 
```
git merge branchname2
```

Messages like this can come up to show results - so in this case we got an error as the files we want to merge have a conflicting issue 

<img width="1066" height="129" alt="image" src="https://github.com/user-attachments/assets/be348a6f-5b23-4d72-8673-710d6b8dfb54" />

What I did to resolve this was echo in a break to separate the lines

<img width="1200" height="41" alt="image" src="https://github.com/user-attachments/assets/dee5a6ac-a92b-4021-936d-2cf89b90bc50" />


You can use this to view branches you currently have and delete those branches 

```
git branch

git branch -d branchname
```

To clone a repo you do 
```
git pull
```

When you're pushing a file that is in a new branch you first need to set the upstream to push it 
```
git push --set-upstream origin feature/added-feature
```

You can then see the Pull request that is created on github and see the changes that is made or what's being pushed. 
<img width="1425" height="777" alt="image" src="https://github.com/user-attachments/assets/0ea0e353-3c29-473b-a767-c4434ab1a657" />


If you've commited something and then go back to the file committed and the change is there. This command will restore the file to the last committed state
```
git restore filename.txt
```

If you want to unstage a file you do the following 
```
git restore --staged filename.txt
```

To undo a bad commit you can do one of these three
```
git reset --soft HEAD~1 - this just moves it back to stage

git reset --mixed HEAD~1 - this will unstage it but keep changes

git reset --HARD HEAD~1 - this will unstage it and remove the changes.
```

If you push a change, the best way to revert this is by doing the following - this will create a new commit that undoes the last one in a safe manor that is good for shared branches 
```
git revert HEAD - just save the file and do a repush to see the change
```

This command will show the logs but in oneline so easy to read output
```
git log --oneline
```

This command will show everything that's happened and you can also recover commits from here
```
git reflog
```


**Git stash basically temporarily saves changes to comeback to later. - putting half done work ina separate drawer to comeback to later**

```
git stash push -m "message here"
```

TO view stash list 
```
git stash list
```

This will bring back the file into the stages area but keep it in the stash list
```
git stash apply
```

This will be remove it from stash list and bring it back to staged
```
git stash pop
```

This can clear the stash list 
```
git stash clear
```
