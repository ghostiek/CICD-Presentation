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

## We start by creating and modifying a repository locally


To create a git repo locally, we can run `git init`
  
We can see it created a hidden folder, and our CLI is now aware we are currently in one.

We can now either manually add a file or run `touch hello.txt` to create one.

We can now run `git add hello.txt` to add the file to our staging area.

We can now commit our file in the staging area to the repository by running `git commit -m "Input any message to explain changes made"`

Here the -m parameter followed by whatever string you please, is the message the commit will have.

We can check out what the commits we have made by running `git log` (Note if you have a large commit history you can exit this by typing `q` instead of scrolling all the way down)


But what if we want to add more than 1 file?

Lets create 2 new files `touch file1.txt` and `touch file2.txt`

We can run `git status` to see that git noticed we have 2 files that are untracked!

Lets add all untracked files instead of doing it one by one with `git add .`

Now to see that everything is indeed tracked we run `git status`

When running `git commit` it is important to note that ONLY staged files will be commited.

We can also undo commits by running `git reset [commit id]` this will preserve our changes onto our local working directory. If we wish to really change all the files to exactly what they were when the commit happened we run `git reset --hard [commit id]`. If we want to go back one commit and don't feel like getting the id we can use `git reset HEAD~1`. You may modify the 1 to any number to specify any number of commits before the current one.

Git doesn't only track new files, it tracks modifications of its contents. So running `nano hello.txt` and modifying the contents and running `git status` will tell us that some file was modified.

So lets add this to the staging area, as well and commit it! `git add .` followed by `git commit -m "Made 2 new files and modified hello.txt"`

## Working with branches

The project is starting to get a bit more crowded and if you have multiple colaborators it would make sense for there to be a development branch and a main copy of the repository.

We can create a copy of the current branch by running `git branch development`. The new branch name is development and we can see all our current branches by running `git branch --list` or shorthand `git branch -l`. 

Lets create another one `git branch whoopsies`, see that it was created using `git branch -l`. You may delete that branch by running `git branch -d whoopsies` and for a sanity check see that its gone by running `git branch -l`

To actually switch branches you need to run `git checkout development`. Now any changes we make on this branch will leave our main branch unaffected.

We can test this. `touch experimental_work.py`, `git add .`, `git commit -m "Adding new python script"`. We can see in `git log` and running `ls` (our working directory) that things have changed. We can even run `git diff main` to see that the branches do differ!

Lets do a sanity check and revert back to main. `git checkout main` and then run `git log` and `ls` we see that none of the changes happened!

Lets say our work looks good and we are now interested in modifying the code on our main branch locally. We can merge as such. `git merge development`.

Now we can see running `git log` that those changes did get made on our main branch.












