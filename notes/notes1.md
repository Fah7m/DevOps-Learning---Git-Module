Git version control 
---

Git allows you to track changes to code over time

Lets you undo, inspect and collaborate 

Revert, review, and branch safely

Git is essential for Devops as it is a key part in the CI/CD pipeline.

Centralised (SVN) vs Distrubuted VCS (GIT)

<img width="1143" height="499" alt="image" src="https://github.com/user-attachments/assets/7a32e3d5-cc86-4589-bde9-c8ac92aca7d5" />

Git is like everyone having their own copy where as SVN is like a google doc file, if it goes down nobody can make changes.

Git is not a file tracker
----

Git is not justa  file tracker, it is much smarter

What Git tracks instead of tracking line by line text is snapshots, not diffs.

Git takes a snapshot of what the file looks like at the point in time - so if you change one line it takes a new snapshot of that file.

Git uses a key-value store (SHA-1 hash) 

A commit in git is a pointer to a full snapshot of your project its not just changes.

GIT stores everything as objects (blobs, trees)

Git doesn't care about the filename but isntead it only cares about the content - if the content changes then the hash changes and if the content is the same, git reuses the same object.

This is what makes so fast and reliable as you can rip through massive changes.


Git terminology
---

<img width="1566" height="979" alt="image" src="https://github.com/user-attachments/assets/b8c4e801-6c44-4e9f-ba5e-f6042350c3de" />


The Git directory 
---

This directory has a secret folder called .git 

This .git directory holds everything your git needs to function such as History, config, branch.

The .git/refs directory is where tags and branches are stored 

The .git/object is where git keeps every commit, blob and tree all compressed and stored by SHA hash.

The .git/config is where your repo specific settings are stored. - different remotes or user info for your project, they will go here

The .git/HEAD tells git what branch or commit your currently on

The .git/index is the staging area which is a temporary zone between editing your files and comitting them.

Git builds the next snapshot in the .git/index 


Git commands
---

<img width="1796" height="971" alt="image" src="https://github.com/user-attachments/assets/b48bb9bf-af23-4087-87cb-a35aefc22c75" />

Git init - Simply initialises a new repo and the tracking then starts 

Git add - This is basically staging your files to be added to the commit 

Git commit - This takes a snapshot of whats being staged 

Git status - This shows you whats going on, whats changed, 

Git log - This shows the commit history - can check who broke something or where something broke

Git diff - Shows whats changed between your working files, staging area or commit - improtant for code reviews, or debugging issues.


3 main areas of GIT
---

***The working direcotry*** is where we actively edit our files whether its a python script, terraform module or a kubernetes manifest. - Git doesn't track them yet 

***The staging area (index)*** is where you put files that you're preparing to commit - basically telling git these are the files I want to include in the next snapshot. Git add can be used to move changes into the staging area.

***Repositry*** This si where your commits and history are stored. ONce you're on git commit, the files go from staging into the actual repo as a new snapshot

***The flow*** Working directory > git add ? Staging area > git commit > Respoitry 


Tracking history in Git
---

Tracking history in devops is important to help with debugging or who made what change or that last helm values file etc..

Git log - Gives the full commit history and is useful when you want to walk back to see what happened recently.

git log --oneline --graph - This shows a clean visual branch layout - handy with delaing merge changes or release branches

git show <commit? - Lets you see exactly what happened in a certain commit. 

Git diff - Compares the unstaged changes with the last commit which is great for cheaking what you broke before committing. 

git diff --staged - Compares the staged changes (Current files in staging area) to the the last commit - essentially comparing what you're about to push to the repo to what was already pushed in the last commit.

Git blame <file> - Shows who last changed each line and its super useful for debugging or reviewing a config file 

Git reflog - Shows every head momvement even stuff that were deleted - if you accidentally nuked the branch or did a bad rebase, reflog can help recover it on occassions. 


Git vs Github
---

<img width="1850" height="858" alt="image" src="https://github.com/user-attachments/assets/801de27d-d207-4da7-a96c-a9eb48a285b7" />

Essentially the difference between the 2 is that Git runs locally on your machine and you make changes to your repo offline without having to touch the internet.

Git is the actual verstion control tool that you use to make changes on Github or Git lab.

Whereas Github is a platform which is a cloud service and it hosts your repo online so you can collaborate with others. - You can open pull requests, review code and automate ci/cd pipelines like github actions 

So to break it down:

Git runs locally - Github runs on the cloud (internet)

Git tracks your history and Github helps teams collborate

Github can be swapped with Github, Gitlab, bitbucket, Azure devops whereas Git is the foundation that is used within these platforms.


Branching 
---

Branching is one gits most powerful features as it lets you work on multiple things at once without messing up the main project. - basically add a new branch to the tree to maybe test the bug that was fixed or test a new feature

***Branching commands*** 
git branch - this shows a list of a branches that you currently have and makes branches

git checkout -b <branchname> - Old way of swithing to a new branch in one go 

git switch -c <branchname> - The mordern way of doing the above

Git switch <branchname> - switching to an existing branch 

git branch -d <branchname> - Basically delete a branch but git can stop you if that branch hasn't been merged yet just to be safe

<img width="1437" height="798" alt="image" src="https://github.com/user-attachments/assets/69447c79-3c01-451c-9cd0-f1b8c0e3368a" />


Merging 
---

This comes to play when you're done working with a branch and want to bring those changes back into another branch. - merging combines changes from one branch to another

There can be issues with merging when both branches have diverged meaning the commits on the main and the added on branch are different, git can do a recursive merge or true merge

This true merge or recursive merge creates a merge commit that ties both historys together however, if the same files were edited on both sides then a merge conflict would occur

The merge conflict could only be fixed manually.

<img width="1621" height="973" alt="image" src="https://github.com/user-attachments/assets/fd15d691-b345-4e54-8fdc-7ebb8779886d" />


Visualise branches and logs
---

The diagram shows how a merge commit would look - so the main branch has a added branch where the feature is created/tested then there is a initial commit to make that feature added on to the main branch.

Some commands to visualise git logs 

<img width="1506" height="865" alt="image" src="https://github.com/user-attachments/assets/b319d9ea-75f1-42c5-b984-83e93fad1cf3" />


Rebase, stach, cherry pick
---

THese three tools are more advanced tools in git that give you more control of your git history

Rebase vs Merge - Merge is a safe and friendly way of bringing two branches together, and preserves the history and adds a merge commit to see where the branch is joined

Merge is great of 

Whereas Rebase is more advanced and surgical as it rewrites your git history to make it look like the branch was always built off the latest commit - this gives a cleaner timeline with no merge commits and is good for cleaning up your brand before opening Pull Requests.

Merge is better for working with others and you want collaboration and you dont face many issues, you use merge here - better for shared team workflows 

Rebase on other hand is better to use when your pushing the branch up for a Pull Request so that the git history looks cleaner before anyone else sees it 

DO NOT rebase shared branches as rewriting the history that others are already using can break stuff 

Merge keeps history - Rebase rewrites them 


Git stash 
---

This comes to play when your in the middle of making changes in a branch and you need to move to another branch however you are not ready to commit. This is where git stash comes in to play.

Git stash hides away all your uncommited changes 

Git stash list - shows all your stashes or any work you've stashed away.

Git stash apply - it reapplies the latest hash but keep it in the list - great for reusing certain work in another branch 

Git stash pop - reapplies the stash and deletes it from the stash - so when you no longer need that stash use this instead of keeping it around.

<img width="1003" height="500" alt="image" src="https://github.com/user-attachments/assets/c97afe32-3eb7-435c-9dec-d08bf82af2f7" />


Reset, Revert and Cherry-pick
---

Git revert is the more safer one out of the bunch - it creates a brand new commit that undo the affects of a previous one but it doesnt mess with the history so its fine to use in shared branches.

git reset literally moves the branch pointer backwards meaning it doesn't look at the most recent commit. The soft keeps the changes although the pointer is moved back. The mixed moves the pointer and unstages your changes. The hard basically nukes everything (removes your changes completely) and this should be used with care. - good locally but dangerous in shared branches as it rewrites history

git cherry-pick this lets you take a certain commit from another branch somewhere else and apply it to your current one - this is useful for hot fixes or targetted changes. 

***Summary*** 
You want to use revert when you want to undo stuff safely on a shared branch. Then you use a reset when you want to move back in history locally.

Finally cherry-pick is best used when you want to copy a certain commit from somewhere else without having to marge a that whole branch. 
