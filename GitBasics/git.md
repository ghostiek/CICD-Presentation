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


## Lets get started

### We start by creating and modifying a repository locally


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

Git doesn't only track new files, it tracks modifications of its contents. So running `nano hello.txt` and modifying the contents and running `git status` will tell us that some file was modified.

So lets add this to the staging area, as well and commit it! `git add .` followed by `git commit -m "Made 2 new files and modified hello.txt"









