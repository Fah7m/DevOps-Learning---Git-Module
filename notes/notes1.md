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

