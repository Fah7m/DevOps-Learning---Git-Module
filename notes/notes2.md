Forks and Pull Requests
---

Forks and PR's are used for cross team collaboration - can be used where there are external contractors or temporary contributors

A fork is essentially your own personal copy of someone elses Github or Gitlab repo. This doesn't come with any push access to the project so you need to fork it. Github creates a copy under your username and then the fork can be cloned locally and changes can then be made there. 

When your changes are ready, you push your changes to your fork on Github and not directly to the repo. The pull request can then be made from there once this has been done 

So essentially the workflow is 

Fork the repo, clone it locally, make changes on your machine, push changes to your fork, then a pull request is made to your fork for the changes to be pushed. 

Pull Reequest or merge request is a way of saying, i've made changes in my fork so can you pull them into your project or I made changes in my branch, can you push these to main. 

PR - a proposal to merge your branch into theirs (main branch)

Github has a functionality where a project owner can review your code, comment on it and request changes. Once it's ready, finally merge if everythings sound. 

<img width="1820" height="865" alt="image" src="https://github.com/user-attachments/assets/be06df86-dbd5-4951-9099-cac0fb105563" />


Best practices for git 
---

<img width="1234" height="728" alt="image" src="https://github.com/user-attachments/assets/7e450438-d0a7-46e4-97e2-b49971b5092b" />

***The typical workflow in git would be*** - First up what you normally pull the latest clone from the main branch or if it is the first time in the repositry, you may just clone the whole repo.

Then you would create a feature branch - Working on something new that could be pushed in the future without having to mess up the main branch or the main codebase.

You then would work locally editing the code, making changes etc and once you're pleased with this, push on to github

Now the Pull Request/Merge Request comes into play. You open a PR tagging the team members saying to take a look at the code or changes made and once it looks good to them, merge it to the main branch.

Finally team syncs regularly via git pull --rebase or merge is important as team members are also working on their own branches and making changes regularly.

<img width="988" height="734" alt="image" src="https://github.com/user-attachments/assets/7c71fb8b-a148-4117-82d4-2ce3832657ff" />

Trunk based development 
---

In simple term it basically means everyone is working directly on the main branch or short lived branches that get merged back quickly.

To make this work safely the teams normally have a strong ci/cd pipeline meaning every commit gets tested automatically 

Also code quality checks so that only good working code makes it to the main branch - teams like Google and facebook work this way in fast paced environments. 

<img width="1225" height="351" alt="image" src="https://github.com/user-attachments/assets/35287fa9-17cd-460e-9fb2-4c3932b0e7e6" />


Commit Hygiene and best practices
---

Write good commit messages - explaining what this commit is about

Squash before merging PRs - Essentially meaning when you have a bunch of commits that are work in progress for different things like fix button or new feature etc, squad them into one commit for a clean history 

One change per commit - Basically keep a commit or each change or bug that is being made as it helps when debugging or when you want to roll back faster

Avoid noisy merges and chaos names - Nobody wants to see names like fixfixfix or fixfinalfinal2. Also, any merge branch into main into main, into stage into final. - keep it clean 


Pre commit and automation 
---

Pre commit and automation comes in when you've written some code and its messy

Pre-commit is a very common tool that is used for this. Also Huskey for JavaScript and TFLint, TFSec for terraform security. These tools hook into your git so they run automatically before the code is commmited.

They work by, saving your file, git add, git commit, and then boom. The checks run in the background before anything hits the repo. These checks stop any broken code or potential bugs being added into the commit

Hokking these on to your CI pipelines, is a good devops practice and makes life much easier for you later on


Mistakes to look out for
---
Forgetting to pull before push - Always pull first to stay in sync or git will slap you with a rejection

Force pushing to shared branches - Doing git push --force is dangerous as its basically editing a group work without telling anyone - this can cause other team members commits to break 

Committing secrets (AWS keys, env files, private credentials, API keys) - Use gitignore, pre-commit hooks and tools like git secrets or trufflehog.

Merging without code review - THere should be branch protection in place but its important to review what is being merged to a main branch or any branch 

Not using gitignore properly - You don't want to commit 5gb of node modules and OS files are important. Adding these to .gitignore is important 

<img width="954" height="375" alt="image" src="https://github.com/user-attachments/assets/552cf2a4-af20-4f28-a7c7-8897b287d5ec" />


Git at scale
---

Mono repos - instead of having microservice repo's or one repo per service, teams sometimes dump everything into one repo - The benefit of this is that it will simplify things such as dependencies and and shared tooling but make things like ci/cd pipelines much harder. 

To deal with those cons, something called selective builds are used - tools like turborepo, nx and bazel only run tests on the part of the repo that's changed so the entire repo isn't tested. 

There is also something called Spare Checkout which basically grabs the subfolders you're working on - this is useful when the full repo is very large (gigabytes) and you only want to close the bit you need.

There are tools like GIT lFS (Large file storage) to store huge media assests - It replaces the big files with pointers and fetches the actual content separately. 

Git filter repo cleans up the history and strips any secrets or removes folders from old commits

Git isn't just for storing app code anymore, when you have GitOps, your infastruction gets version control too. Tools like argo CD or flux, they monitor Git and rollout changes automatically - THese are like Ci/CD but for your kubernetes clusters. 

In summary git doesnt break at scale but how you ise it has to be mature - the same git more smarter and native workflows. 


Git security and secrets hygiene
---

Committing secrets to git is a fast track method to getting fired as there are bots scanning public repos every minute. 

Tools like git secret, trufflehog and even gitignore basics help with this as they act like security guards that scan your code before you commit and they notify you if there is something of concern.

If you've committed a secret to git, its best to clean your git history using tools like git-filter-repo, BFG repo-cleaner and even just renew your secrets as soon as possible.

Steps to take - you find out you commited secrets > renew your secret > revoke it > move on

Deleting just the file you commit is nout enough as the secret is sitting there in the older commits so best to take care of that as well. 

Another good tip is to audit your git logs to have a look at who made what changes - there are bots that can assist with this to tell you if something sketchy has been commited.


Connecting to GIt
---

<img width="1662" height="743" alt="image" src="https://github.com/user-attachments/assets/bae21944-d630-4cde-b447-88c21f9d5cf7" />

