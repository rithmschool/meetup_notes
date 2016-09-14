# Github Introduction

### Objectives:

By the end of this chapter, you should be able to:

- Compare and contrast Git and GitHub
- Create a remote repository and push/pull from a local repository using SSH
- Fork and clone remote repositories and create additional remotes
- Understand the process of issuing a pull request 

### What is GitHub?

GitHub is a web-based Git repository hosting service. Simply put, it is a tool used for collaboration and repository hosting (that uses Git). This is something **VERY** different from Git so make sure you understand that Git and GitHub are not the same thing.

### Create a Remote repository

Once you have an account, head over to [https://github.com/new](https://github.com/new) and create a repository. In this example, we will be creating a repository called `first_repo`. Do not worry about the description or checking the box to initialize the repository with a README. 

```bash
echo "# first_repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/elie/first_repo.git
git push -u origin master
```

Let's go through these steps one by one 

1. `echo "# first_repo" >> README.md` - we are passing some markdown (don't know what the `#` does? Head back to the [first section](./01-install-and-essential-tools.md) and learn some more about markdown!). We pass the text "# first repo" to a file called `README.md`

2. `git init` - make sure we have a repository 

3. `git add README.md` - let's add the README.md file (we can also do `git add .` or `git add -A` here)

4. `git commit -m "first commit"` - add a commit with the message "first commit"

5. `git remote add origin https://github.com/elie/first_repo.git` - this is where things get fun. This command tells our local repository about a remote repository located somewhere. The location of our remote repository is `https://github.com/elie/first_repo.git`. Now if we want to send our code to GitHub we can just type in `git push https://github.com/elie/first_repo.git master` - but typing that whole URL is quite a pain. Instead, it would be better if we could give the URL a nickname (also called an alias) - that is what "origin" is!

So going back, `git remote add` is how we tell our local repository about a remote repository (that we can send/retrieve code from). `origin` is a nickname for where the repository is actually located (at `https://github.com/elie/first_repo.git`).

6. `git push -u origin master` - Now we can send our code from a local repository to our remote repository (which we aliased to `origin` in the previous command). The `-u` flag allows us in the future to only have to type `git push` instead of `git push origin master`. 
 
So to review this command - `git push` is how we send code from a local repository to a remote repository. `origin` is where we are sending it (specifically to `origin/master` which is the master branch on our remote repository). `master` is the local branch where we are sending our code from.

### Pushing code up to GitHub

Now when you type in `git push`, you will be prompted to enter your username and password for GitHub. While that is fine once or twice, it becomes quite a nuisance if you are pushing or pulling (retrieving code) frequently. It would be nice if we could establish some trust between our computer and GitHub so that when we run `git push` or `git pull`, GitHub does not need to authenticate us. To do that we are going to create an SSH key.

### Creating an SSH Key

This can be a bit intimidating, but if you follow the steps carefully, you should be able to get this to work.

1. Start here - [https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
2. Continue here - [https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)
3. Finish here - [https://help.github.com/articles/testing-your-ssh-connection/](https://help.github.com/articles/testing-your-ssh-connection/)

### Fork

Now that we know how to push code up to GitHub, let's discuss a GitHub specific concept: forking.

When working with others, you may sometimes not be able to push directly to that repository (imagine if we could just push our code to some of the world's largest open source projects...that would be pretty crazy). So what we need to do is make a copy of someone else's remote repository and make sure it is under our username so that we can push code to it. 

To practice forking - head over [here](https://github.com/rithmschool/learn_forking) and on the top right you will see a button with the text Fork. Click on this button and you will have a copy of the repository under your name!

Remember, the "forking" is a **GitHub** concept, and not something directly related to Git. It is simply the way to make your own copy of a repository on your account where you have permission to push your code to GitHub.

### Clone

Once you have forked the repository, you need to take that repository (the remote one you just made) and download the code on your local computer (make a local repository). Instead of making a folder and going through the whole `git init` process and adding a remote, you can use the `git clone` command, which takes a link the to repository and downloads it (with the remote set up!)

Head over to your forked copy of the repository and you will see a button that is either set to `HTTPS` or `SSH`. When you click on this button it should display "Choose a clone URL" - **Make sure that your is using SSH**. Then copy the link by either selecting and copying or by clicking the icon next to the link (when you hover over it - it should say "copy to clipboard").

In the terminal (you can start in your home directory) run the command `git clone PASTE_URL_HERE`

Now that you have the repository locally, add a new file or make some changes, add and commit them and run `git push origin master` and you should see your updated changes in your forked copy.

### Pull Request

Now let's say you are collaborating with the `rithmschool` organization (where you forked the repository from) and you would like to merge your changes with the original repo that you forked (remember you can't just push up to it, because you do not have permission to do that). You can issue a pull request and someone who has permission can either merge or reject it.

To do this, click on the "New pull request button" and then click on the "Create pull request". You should then be able to go to the original repository.

### Retrieving Code from Github + Setting Upstream

Now what happens if someone else makes a pull request? How do we get that code to our computer? Do we have to fork and clone all over again? Nope! Instead we will use a different and easier work flow.

1. Make sure everything is committed first locally
1. Pull the latest code from GitHub (from a new remote which we will call `upstream`)
2. Fix merge conflicts if there are any
3. Push the code back up to `master`

So what is going on in step 2? What is this `upstream` thing we are talking about? Well, we have our remote called `origin` which corresponds to the forked repository, but if a change has been made to the original repository which we forked, we want to get the latest changes! Even though we can't push to that repository, we can `pull` to get the latest changes. But in order to do that we need to tell Git what remote repository to pull the code from. So let's add a new remote called `upstream`

`git remote add upstream git@github.com:rithmschool/learn_forking.git`

We can now run `git pull upstream master` to get the latest code from the original repo, and then we can run `git push origin master` to update our forked copy with the latest code.

### Exercise

Let's take a bit of time to practice this git workflow! It is so valuable to just practice this workflow a couple times, since you will most likely doing it professionally as well as in your individual projects and open source contributions. Here are some things to do.

1. Create a local repository and add and commit some files
2. Create a remote repository and push your code from the local repo to the remote
3. Fork the repo [https://github.com/rithmschool/git_practice](https://github.com/rithmschool/git_practice) - clone it and submit a pull request
4. Create a new branch locally and push it to github

### Additional Resources

[https://guides.github.com/](https://guides.github.com/)

[https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
