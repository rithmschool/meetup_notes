# Command Line Part Introduction

### Objectives:

By the end of this chapter, you should be able to:

- Define what Terminal is and how it is structured
- Navigate and list files all over your machine
- Create, read, update and delete files and folders

### What is Terminal?

Terminal is an application that gives us a command line interface (or CLI) to interact with the computer. Everything you can do in Finder you can do in the terminal and more often than not, it is much faster in the Terminal. Although the interface is challenging at first and it seems daunting, with a bit of practice, you'll be up to speed in no time!

### What is a shell? 

You will also hear the term "shell" when learning about terminal so it is important to distinguish these. From Stack Overflow: 

The **shell** is the program which actually processes commands and returns output. Most shells also manage foreground and background processes, command history and command line editing. These features (and many more) are standard in bash, the most common shell in modern linux systems. 

A **terminal** refers to a wrapper program which runs a shell. Decades ago, this was a physical device consisting of little more than a monitor and keyboard. As unix/linux systems added better multiprocessing and windowing systems, this terminal concept was abstracted into software. 

### How Terminal is Structured

In terminal all files and folders begin at the root directory. The root directory is noted by a `/`. Inside the root directory are essential files/folders that your machine needs, but we do not modify the files and folders in the root directory often. Inside of the root directory, we have a folder called `Users` which contains all of the user accounts on your computer, and if you change directory into your user account you will be in the `home` directory, which is denoted by `~`.  For example, if you user name on the computer is `eschoppik`, then your home directory would be `/Users/eschoppik`.  A synonym for the `/Users/eschoppik` path is `~` when you are logged in as `eschoppik`.

### Moving Around

The first thing you want to start to understand when working in the terminal is how to navigate from folder to folder. One of the most common commands you will be using in terminal is `cd` which is short for "change directory." In order to change a directory, type `cd` followed by the directory or a path to the directory. If we want to move back a directory we use `cd ..` and if we want to move into a directory we specify the name of the directory we are moving into. For example, if you are in your home directory and type `cd Desktop`, you should move into your Desktop directory.

We just mentioned that you can type `cd` followed by a directory or path. But what is a path? Let's read some more below:

### Absolute Paths vs Relative Paths

A path is simply the way to reach a file or folder. When we specify a path starting from the root directory `/`, we call that an absolute path. For example, if I am currently in the `~` home directory and I would like to change directories into my Desktop folder, I can do that in two of the following ways:

1. `cd Desktop` - relative to where I am currently
2. `cd /Users/eschoppik/Desktop` - absolute, starting from the root (first `/`, then `Users`, then `eschoppik`, then `Desktop`)

##### Questions to Answer

- What is the difference between `/` and `~`? What do we call each of these directories?
- What command do we use to change directories?
- What is the difference between an absolute and relative path?

### Listing Files

Another one of the most important commands you are going to be using is `ls`, which is used to list directory contents. If you type `ls` in a directory you will see all sorts of content. For example, typing `ls` in your home directory will show you all of the files and folders inside of that directory.  Typically your home drectory contains folders such as `Desktop`, `Documents`, `Downloads`, `Music`, `Pictures`, etc.

### Creating Files And Folders

Now that we have a good understanding of how to change directories and navigate in the terminal, let's see how we can create our own folders and files. To create a folder we use the `mkdir` command followed by the name (or names separated by a space) of the folder(s) that we would like to create. So let's head over to our `Desktop` and create a new folder called `first_folder`.

```sh
cd /Users/$USER/Desktop
mkdir first_folder
```

Whoa...you should be asking yourself, what is that `$USER` thing? It is an environment variable in your shell that keeps track of the current user of the shell. You can also see who `$USER` by typing `echo $USER` or by using the command `whoami`. Try out both methods of checking who the current user is.

As another side note, this tutorial will use absolute paths to navigate, just to make it easier for you to follow along. However, don't feel like you MUST use absolute paths over relative ones.

Now that we made the `first_folder`, how do we change directories into it? If you are thinking of the `cd` command, you're right! So let's `cd /Users/$USER/Desktop/first_folder`. Or, if you are already in your Desktop, you can just `cd first_folder`.

So we just mentioned "if you are already in your Desktop".  How do you know which directory you are in if you forget? Thankfully, there is a handy command called `pwd` which will display the absolute path and let you know what current directory you are working in. So if you are ever unsure, just type in `pwd`.

Now that we are inside our new folder, `first_folder`, let's create a new file.  A simple way to create a file is the `touch` command.  The `touch` command simply creates an empty file.  Let's create a file called `first_file`: `touch /Users/$USER/Desktop/first_folder/first_file`.  Alternatively, if you are currently in the `first_folder` directory, you can simple type `touch first_file`.  Now use the `ls` command to verify that your file was created.

### Displaying Contents Of A File

A very common command to display the contents of a file (also used for concatenating files) is the `cat` command. If you type `cat NAME_OF_FILE` you can see the contents of the file easily.  Try it out on the file you just created, `first_file`.  You should see no output after pressing enter.  There is no output because `first_file` is empty.

Let's add some text to the file so that we can use `cat`.  Type:

`echo "Hello World" > first_file`

The `echo` command simply writes text to the termainl output.  The `>` is called a redirect.  The `>` redirects the output from the command on the left side into the file on the right hand side.  We will see more redirects in the next command line lesson.

Now try using cat on the file again.  Do you see `Hello World`?

There are other ways of seeing the contents of a file in the terminal.  Try using the command `less`: `less first_file`.  `less` is a program that displays the contents of a file and allows the user to navigate up and down through the file or search for text in the file.  To exit `less`, just press `q`.

### Moving Files And Folders

Now that you understand how to create files and folders, let's move onto another essential operation: moving and copying folders. To move files/folders (and something else we will see soon) we use the `mv` command. Lets try this out! 

Let's head back to the Desktop by typing in `cd ~/Desktop` and let's make a new file called `test.txt` (remember that command? If not - stop reading and go through the previous section again). Now on your desktop you should have a folder called `first_folder` and a file called `test.txt`. Our goal is to move `test.txt` inside of `first_folder` - let's do that using the `mv` command. First make sure you are in the Desktop (type `pwd` to be sure) and type `mv test.txt first_folder/test.txt` and press enter.

Did it work? You shouldn't see any kind of success message or confirmation from the terminal, but you also should not see an error. This is very common when working with the terminal: you will see error messages if a command is incorrect, but very rarely see a success message. To make sure we did the correct thing, let's `cd` into `first_folder` and type in `ls`.  We should see `test.txt` inside of `first_folder`.

### Deleting Files And Folders

Alright, enough with this `test.txt` file, let's get rid of it. Make sure you are inside the `first_folder` and type `rm test.txt`. Once again, you shouldn't see much of a response from the terminal, so run a quick `ls` to make sure there is nothing there. Now that it is gone....where did it go? The Trash? The answer is it is completely removed from your computer.  There is no confirmation or undo so be **VERY** careful when using the `rm` command. After you have removed this file, head back a directory and remove the `first_folder` directory.

If you try to use `rm` on its own, you will see this message: `rm: first_folder: is a directory`. So we know that `rm` is for a file, lets use the `rmdir` command to remove `first_folder`. Make sure that there is nothing else inside that folder, or else you will see a message that looks like this: `rmdir: first_folder: Directory not empty`.

If there is anything inside the folder, you will have to use `rm -rf first_folder`. The `r` and `f` in `-rf` are called flags, and they correspond to options that can be passed to the command. To learn more about what `-r` and `-f` do, you can type in `man rm` (`man` is short for manual) and use the arrow keys to move up and down. When you're finished, press `q` to quit.

### Exercise

1. Create a file called `name.txt`
2. Rename the file to `rename.txt` using the `mv` command. What does this tell you about the command?
2. Using the `cp` command, make a copy of `rename.txt` and call it `copy.txt`
3. Remove the file `copy.txt`
4. Create a folder called `answers`
5. Change directories to the `questions` folder
6. Create a file called `first.txt`
6. Create a file called `second.txt`
7. Go back a directory and make a copy of the questions folder and call it `questions_copy`
3. When using `cp -r` what is the `-r` called? What does it do?
4. Delete the original `questions` folder
4. What does the `man` command do? Type in `man rm`. How do you scroll and get out?
5. Look at the `man` page for `ls`.   What does the `-l` flag do?  What does the `-a` flag do?
7. Type the following command to download and save the contents of google.com: `curl https://www.google.com > google.html`
8. Use `less` to look at the contents of `google.html`.
9. Look at the man page for less.  Read the section on /pattern.  Search for the text **hplogo** in the `google.html` file.
5. How do you jump between words in the terminal?
6. How do you get to the end of a line in terminal?
7. How do you move your cursor to the beginning in terminal?
8. How do you delete a word (without pressing backspace multiple times) in terminal?

# Git Introduction

### Objectives:

By the end of this chapter, you should be able to:

- Define what a VCS is 
- Initialize an empty repository and write necessary steps to commit successfully
- Create branches for a separate workflow and merge when necessary
- Contrast merge strategies and fix conflicts when merging

### What is Git?

If you google "what is git" you will probably see the definition for "an unpleasant or contemptible person." Thankfully, Git is much better than that. According to [Wikipedia](https://en.wikipedia.org/wiki/Git_(software)): 

>Git is a version control system that is widely used for software development and other version control tasks. As a distributed revision control system it is aimed at speed, data integrity, and support for distributed, non-linear workflows.

In plain English, Git is a tool that allows developers to track/remember versions of their code over time, and is essential when collaborating with other developers to ensure that "snapshots" taken of the code can be revisited if necessary.

### Getting Started with Git

 Before we can get started with anything Git related, we need to make sure you have Git installed. Type in `git --version` and if you do not see an error, you are good to go. If you are seeing any errors, head back to the first section on installation and make sure you ran `brew install git`. 

Once you have Git installed, you need to "initialize" a repository with Git before you can start using it. Create a folder called `learn_git` and `cd` into that folder.

Once you are in this folder, type in `git init` and you will see something like `Initialized empty Git repository in /Users/YOUR_USERNAME/Desktop/learn_git/.git/`. What does this mean? What do you think just happened? If you type in `ls` you will see that it looks like nothing is there... but how can you view hidden files?

After typing in  `ls -lah` you will see a folder called `.git`. This is what the `git init` command does: it creates a `.git` folder for you. Fortunately, you will almost never have to go into that folder, but without it you will not be able to use any of the git commands in the next step. So remember, the first step to any project with git, is making sure you have a `.git` folder.

### Adding and Commiting Files

In order to take a snapshot of your code (what we will call a "commit") you first need to add your code from your working directory to what is called the staging area. Git wants you to be careful and not just take snapshots haphazardly, so it adds an intermediate area called the staging area where your code goes before it is "committed" (a snapshot is taken). To see what stage your code is at, you can use the `git status` command.

The command that moves code from the staging area is the `git add` command. You can either specify filenames after `git add` or you can add a `.` which will include the entire directory, or you can pass in `-A`. If you want to read more about the differences, check out [this](http://stackoverflow.com/questions/572549/difference-between-git-add-a-and-git-add?rq=1) stack overflow post. 

Finally, when you have added all the files you would like to the staging area, the next step is to commit with a message (you always need one). This is done using the `git commit` command with the `-m` flag. So once you have added, you can then type `git commit -m "initial commit"` and you will make your first commit.

### Seeing commits and changes

Once you have made a commit, you can see the message, author and some additional information using the `git log` command. When you type this in you will also see a very long string which looks like gibberish. This is called the `SHA` and it is a unique identifier for the commit. To get out of `git log` you can type `q`.

Now let's add some additional text files and add and commit a couple more times. Now when you take a look at `git log` you should see a longer history of commits. 

If you want to see differences between your commits you can use the `git diff` command and specify the `SHA` to compare.

### Undoing commits 

Sometimes we end up committing things we do not want to be remembered. To undo commits we can use the `git reset` command. There are 3 flags we can pass to this:

`git reset --soft` - moves the files commited back to the staging area

`git reset --mixed` - moves the files commited back to the working directory

`git reset --hard` - undoes the entire commit (**dangerous**)

### Git Branch Workflow

When working with Git in the terminal, you will see something by your folder called `(master)` - this is the name of the branch you are working on. 

In most modern work flows, we do not do all of our work on a single branch. Instead, we usually have many different branches for certain use cases (bug fixes, new features, deployment), so it's essential to understand how to create, delete, and merge branches

`git checkout -b NAME_OF_BRANCH`

`git checkout NAME_OF_BRANCH`

`git branch -D NAME_OF_BRANCH`

![https://mockupstogo.mybalsamiq.com/projects/diagrams/Git%20Workflow.jpeg?version=2&etag=plZmSSfv_W.UEa66ETw65ft7dpl9sFkE](https://mockupstogo.mybalsamiq.com/projects/diagrams/Git%20Workflow.jpeg?version=2&etag=plZmSSfv_W.UEa66ETw65ft7dpl9sFkE)

### Merging and Merge Conflicts

When we want to move changes from one branch to another, we use the `git merge`command. Depending on the history of our commits, we can merge two different ways:

1. Fast forward
2. Recursive

Unfortunately, merging is not always so easy, and Git has a hard time figuring out which change to use. This is called a _merge conflict_. Let's see an example. Starting in our home directory:

```bash
mkdir merge_conflicts
cd merge_conflicts
git init
echo first > first.txt
git add .
git commit -m "first commit"

git checkout -b new_branch
echo second > second.txt
git add .
git commit -m "adding second.txt"

git checkout master
echo something_else > second.txt
git add .
git commit -m "adding second.txt on the master branch"

git merge new_branch
```

This final command should output

```
Auto-merging second.txt
CONFLICT (add/add): Merge conflict in second.txt
Recorded preimage for 'second.txt'
Automatic merge failed; fix conflicts and then commit the result.
```

Looks like we have an issue because when we merge the new_branch, git does not know which second.txt file to use!

If we take a look at our second.txt file (`cat second.txt`) we will see this

```
something_else
=======
second
>>>>>>> new_branch
```

What we see is HEAD (where master is) and then `new_branch` which is where the new branch is. Let's open up this file in sublime and change it so that it looks like this:

```
second
```

Then let's go back to the terminal and run

```bash
git add .
git commit -m "fixing merge conflict"
```

And we should be good to go

### .gitconfig Settings

If you take a look at `git log` you may not see any information for the author and email. To change this (you will absolutely want this for GitHub so make sure the email you specify is the same one you used to sign up for GitHub), type:

`git config --global user.name "YOUR NAME"`
`git config --global user.email "YOUR EMAIL"`

If you also find it annoying to press `q` every time in `git log`, you can change this as well

`git config --global --replace-all core.pager cat`

### Scratching the surface

Although we have covered quite a bit of Git, we are still just getting started learning about it. Below is a fun chart explaining what happens if you're in trouble with Git. This should not scare you, just give you an idea of how powerful Git is and how many commands there are for all kinds of situations. Take a look, get inspired and then continue on to the exercises!

![http://justinhileman.info/article/git-pretty/git-pretty.png](http://justinhileman.info/article/git-pretty/git-pretty.png)

### Exercise

Now that you have learned how a basic GitHub workflow happens, try running through this a couple times on your own:

- initialize a new repository
- add and commit some new files
- create a new branch
- add some new files on that branch
- commit 
- switch back to master
- merge in your changes
- see your changes using `git log`

Make sure to do this a couple times - there is a good amount of muscle memory with this.