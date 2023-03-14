# What is Git?

Git is a distributed version control system that tracks changes in any set of computer files.

# What tools can you use?

For this demo I'll be using only the git bash CLI, there's plenty of GUI that exist (such as git kraken) and are very useful to visualize your work, without having to remember all these commands.


# Demo

## Preface

This is just a demo that goes over most of the commands I mainly use on my day to day work. There's so much more to git so if you need to look up other commands I'd highly recommend reading through [the docs](https://git-scm.com/doc).

## Installation

You can install git [here](https://git-scm.com/downloads)

If you wish to do so using a GUI, I would recommend

[Gittyup](https://github.com/Murmele/Gittyup)

[Git Kraken](https://www.gitkraken.com/) (requires a license past the 1 week free trial)


## Lets get started!

Something to keep in mind with Git are the 3 main states. Your files can either be modified, staged or committed.

- Modified means that you have changed the file but have not committed it to your database yet.
- Staged means that you have marked a modified file in its current version to go into your next commit snapshot.
- Committed means that the data is safely stored in your local database.

It'll make more sense once we actually start the demo. But here's a good view of what we are about to go over.

![Stages of Git](https://git-scm.com/book/en/v2/images/areas.png)


## We start by creating and modifying a repository locally


To create a git repo locally, we can run `git init`
  
We can see it created a hidden folder, and our CLI is now aware we are currently in one.

We can now either manually add a file or run `touch hello.txt` to create one.

We can now run `git add hello.txt` to add the file to our staging area.

We can now commit our file in the staging area to the repository by running `git commit -m "Input any message to explain changes made"`

Here the -m parameter indicates that the string that follows will is the message the commit will have.

We can check out what the commits we have made by running `git log` (Note if you have a large commit history you can exit this by typing `q` instead of scrolling all the way down)


### But what if we want to add more than 1 file?

Lets create 2 new files `touch file1.txt` and `touch file2.txt`

We can run `git status` to see that git noticed we have 2 files that are untracked!

Lets add all untracked files instead of doing it one by one with `git add .`

Now to see that everything is indeed tracked we run `git status`

When running `git commit` it is important to note that ONLY staged files will be commited.



Git doesn't only track new files, it tracks modifications of its contents. So running `nano hello.txt` and modifying the contents and running `git status` will tell us that some file was modified.

So lets add this to the staging area, as well and commit it! `git add .` followed by `git commit -m "Made 2 new files and modified hello.txt"`

We can also delete all commits past a certain commit id by running `git reset [commit id]` this will preserve our changes onto our local working directory. If we wish to really change all the files to exactly what they were when the commit happened we run `git reset --hard [commit id]`. If we want to go back one commit and don't feel like getting the id we can use `git reset HEAD~1`. You may modify the 1 to any number to specify any number of commits before the current one.

### What if there's sensitive or useless data we never want to commit and share?

We can create a file named `.gitignore`. Normally we would copy paste in it whatever useless files R/Python/Pycharm/VSCode/RStudio or other tools may generate. You may find the full list of templates [here](https://github.com/github/gitignore).

However it is also useful to be able to modify it yourself. If we created a data directory as such `mkdir data` and we had very private info there. `nano data/secret_keys.txt`. We can add `data/` to our `.gitignore` to never track that directory. We can also ignore specific files and there's also tons of patterns you can create but I won't go deeper into that because there's already too much to cover. If you want to learn about what else you can ignore feel free to read [the docs on .gitignore](https://git-scm.com/docs/gitignore)

## Working with branches

The project is starting to get a bit more crowded and if you have multiple colaborators it would make sense for there to be a development branch and a main copy of the repository.

We can create a copy of the current branch by running `git branch development`. The new branch name is development and we can see all our current branches by running `git branch --list` or shorthand `git branch -l`. 

Lets create another one `git branch whoopsies`, see that it was created using `git branch -l`. You may delete that branch by running `git branch -d whoopsies` and for a sanity check see that its gone by running `git branch -l`

To actually switch branches you need to run `git checkout development`. Now any changes we make on this branch will leave our main branch unaffected.

We can test this. `touch experimental_work.py`, `git add .`, `git commit -m "Adding new python script"`. We can see in `git log` and running `ls` (our working directory) that things have changed. We can even run `git diff main` to see all the changes between the two branches.

Lets do a sanity check and switch branches back to main. `git checkout main` and then run `git log` and `ls` we see that none of the changes happened!

Lets say our work on the development branch looks good and we are now interested in implementing our changes into the local main branch. We can merge as such. `git merge development`.

Now we can see running `git log` that those changes did get made on our main branch.

## What we have done so far

We have been able to keep a history of all changes made locally and that's great but in order to share our code we will need to push our code to a remote repository.

## Working with Remote Repositories

First, lets rename our master branch to main. By default `git init` names it master, but since I wrote this entire tutorial mentioning the `main` branch we will be renaming the branch by running `git branch -m master main`.

We will be using github to host our remote repository. So we go to the `+` sign on our account and create a new repository. We then follow the very simple instructions. Since we already did most of it we will simply run `git remote add origin git@github.com:ghostiek/test.git` to tell our git repo that we need to modify code in this location.

We can inspect our remote using `git remote show origin`

And to push our code to remote we run `git push -u origin main`. This will push our main branch into the remote repository. We add the -u flag to make it so that the next time we want to push to remote we can just run `git push`. If we want to add all branches to the remote repo then we run `git push origin --all`

Origin is the remote's default name but you may rename it to whatever you see fit with `git remote rename old_remote_name new_remote_name`

If a modification has been made on the remote repository, you may update your local repository to the latest commit by running `git pull`

## Making a Pull Request

When working in a real project, you cannot merge your branch locally and push to main, that's a receipe for disaster, there will often be restrictions disallowing such an operation in the first place. The proper way to modify the main branch is to make a Pull Request. If I modify the development branch, make a commit and then push, once I open up github it will tell me that my branch is 1 commit ahead of master and suggest I make a Pull Request. A pull request is a way for me to merge the branch I have been working on with another. We may modify the targer branch to any other, in this example we will use main. Once the Pull Request is made collaborators may discuss it and suggest changes, once you get approval from your peers it may be approved and the branch will be merged into main.

This is the ideal case scenario. But sometimes things get a little messy.



## Merge conflicts and how to resolve them

Say coworker 1 added in a new feature, which got pushed to the main branch when we were still working on our development branch. We unfortunately modified the same lines of code and git now doesn't know which lines to keep.

We may go on the PR, and click on the resolve conflicts button.

This might seem a little confusing at first but it's much more straightforward than it seems. This `<<<<<<< branch_name_1` and everything below until we hit `=======` represents the changes made by our branch, everything below the equal sign until `>>>>>>> master` represents the remote main branch code.

To resolve this conflict, modify the file by keeping or removing whatever changes make sense. In this case I want to remove my coworkers work for my optimized line of code. We then mark it as resolved and commit merge. Our merge is finally successful and we may discuss it in more details before completing our PR.

Once a PR is completed, it is common practice to delete the branch you were working on, and if a new feature needs to be made you may now branch off main.

## What if I want to contribute to other projects?

You may fork their repository and then clone your new remote repository to your local machine using `git clone link_to_repo.git`. And with the knowledge you now have you know how to make changes, put them in the stage area, make a commit, push them to your remote. Finally, you may head to the original repo and make a PR to merge your fork into the main one. Remember to follow proper etiquette the repo has set.











