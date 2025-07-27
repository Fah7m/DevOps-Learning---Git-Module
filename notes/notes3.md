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


**Workflow to follow when adding, committing and push is this** 
```
touch app.txt

git status - to check the status of the file

git add app.txt - this will add the app.txt to staging area

git status - this again to check if its there

git commit -m "commit message" - this will commit it before the final step

git push - this pushes the file onto your github repo.
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


Usage of git rebase - this can be used to squash multiple commits into one commit to make the history look better e.g. I make a change to a file and add in 2 extra lines but for each line added, I did 2 whole commits. We can merge this to one commit for housekeeping. 

Here we first added a new branch called **feature-rebase** and added a file called changes.txt - we then added it to staging and commited.

<img width="1054" height="309" alt="image" src="https://github.com/user-attachments/assets/dcd37d86-467c-4f28-b7f6-4077fba1c285" />

We then wanted to make some changes to the file again and added it to staging then commited.

<img width="932" height="582" alt="image" src="https://github.com/user-attachments/assets/2e0b4b5e-65fa-41d9-b5f7-18831aaaee83" />

We can now see in the **git log --online** that there are 3 separate commits

<img width="770" height="136" alt="image" src="https://github.com/user-attachments/assets/6e8533f8-a7dd-4b0c-a9e7-33129725ba18" />

Here we run **git rebase -i HEAD~3 to combine the last 3 commits into one. - We then change the last 2 commits to squash to combine it

<img width="1915" height="982" alt="image" src="https://github.com/user-attachments/assets/0a6866e3-5c30-4923-a9f6-d471b401ffb3" />

And here we add a message for the commit message 

<img width="1793" height="916" alt="image" src="https://github.com/user-attachments/assets/2396ce96-7da3-4ab3-b1d9-13906c5be9db" />

Finally we can see here that the last 3 commits are combined into one with the new commit message. 

<img width="1106" height="108" alt="image" src="https://github.com/user-attachments/assets/0fa34918-d3eb-4a13-be33-d5eb615292ba" />

Then a **git push --set-upstream origin feature-rebase** is done to create the pull request in the repo. - Also we can see the commit history here in github 

<img width="1422" height="191" alt="image" src="https://github.com/user-attachments/assets/79710c1b-fa54-4199-b92d-55a327d17095" />



**Cherry picking** is very useful when you want to grab a commit from another branch and put it on to main or whatever branch.

Here the branch was added and a file was added to a  commit in that branch.

<img width="1272" height="433" alt="image" src="https://github.com/user-attachments/assets/5f28f19c-3d77-4554-9d44-6fb7247550c6" />

I then copied the commit code from that branch using **git log --oneline**

<img width="1107" height="70" alt="image" src="https://github.com/user-attachments/assets/a6db42e3-14cf-4b57-b908-0a43e8f2053f" />

Finally switched to the main branch so I can **cherry pick** the commit and push it on to that branch.

<img width="934" height="457" alt="image" src="https://github.com/user-attachments/assets/7f3abb44-9ab6-4457-a156-701b67f31b8a" />


**git ignore** is very useful for security reasons as we dont wanna push any access keys or env files on to git.

Best thing to do is to create a .gitignore file in your local folder where you work and then in the gitignore, add the files you dont want to be tracked by git such as 

<img width="980" height="91" alt="image" src="https://github.com/user-attachments/assets/477c0ca9-6609-4a85-9182-cc09cba0971c" />

adding node_modules here would be useful too as they take a lot of space.


**git commit amend** is useful for making a change to a commit for example the commit message can be changed or add files to the commit 

<img width="837" height="331" alt="image" src="https://github.com/user-attachments/assets/4825197e-6344-432e-9c1a-6bbcbff5dc82" />


**git hooks** scrapes that run automatically every time a particular event occurs in a repo. - they check whats allowed in based on what the .pre-commit-config.yaml file has in it e.g. there could be requirements in that yaml file for terraform files to have the correct formating or for txt files to have an extra line at the end.

In my yaml file I have added some basic text formatting so it can tell me if something is wrong. 

Here we can see what happens when you commit with the .pre-commit-config.yaml setup - it shows the issue and fixes the issue if that is setup in the yaml file.

<img width="895" height="433" alt="image" src="https://github.com/user-attachments/assets/55a99506-5959-4a6c-9208-1a6a67353093" />

