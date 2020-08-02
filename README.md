# Introduction

Many students have heard of or even used GitHub, but few of them have explored its capabilities. 
In this step by step walkthrough, let's get familiar with Git on the command line while building the foundation of our very own personal website.

# Requirements

Ensure you have access to the command line or terminal on your computer.
This is included on OS X machines, but Windows users may need to Google around (can use e.g. PowerShell).
Make sure to create a GitHub account first as well, though if you're seeing this repository, you should have done so already.
Finally, ensure that `git` runs on your chosen command line.
If the command is not found, you'll need to find a way to install it.
Commonly, Mac users will need to install Xcode and the command line developer tools.

# Step by Step

In this step by step tutorial, I will use `$` to signify commands that should be run on the terminal.
Do **not** copy `$` into your terminal, as your terminal will be unhappy and will throw an error.

## Git Setup

After installing `git`, you'll need to set some configuration options.
Run the following commands in your terminal.

```
$ git config --global user.name "firstname lastname"
$ git config --global user.email "email@domain.com"
```

Running these commands tells `git` about the author of each commit, which makes sure that you get credit for the code you publish.
Next, let's clone, or download, this repository.
Change to a directory you are familiar with.
I use a `repos` folder in my home directory.

```
$ cd ~/repos
```

`cd` represents `change directory`.
The `~` represents your home directory. On Windows machines, this might have unexpected results, but is consistent on UNIX based machines, such as OS X devices.

```
$ git clone https://github.com/ktpumd/git-started
```

Notice that to clone a repository, we simply copy its URL from our browser.
If this is your first time downloading a repository, you will be prompted for a username and password.
Enter your GitHub username and password if prompted.
Now, list the current directory using `ls`; we should see a folder titled `git-started`.

```
$ ls
  git-started
```

Congratulations! Now, you've cloned this repository and can access all of its files in that directory.
Next, let's learn how to create our own repository.

## Creating a Repository

Before we create a repository, let's have a short sidebar.
GitHub provides a feature called GitHub Pages, which is essentially a way you can host a website for free using a GitHub repository.
A repository titled `<username>.github.io` will be accessible at that URL (provided you take some extra steps).
Let's begin by creating this repository.
First, let's create a folder for your repository.
For these examples, I will use `foo` as the example username.

```
$ mkdir foo.github.io
```

Now, enter the directory.

```
$ cd foo.github.io
```

Finally, let's **init**ialize a repository.

```
$ git init
  Initialized empty Git repository in /your/directory/foo.github.io/.git/
```

Note: `.git` is a folder that holds everything `git`-related for a repository.

## Creating a README.md

Next, let's create a `README.md` file in our repository.
`.md` files represent Markdown files, which is a way to mark text up and is very commonly used for `git` repositories.
Run the following command in your repository.

```
$ echo "# Hello World!" >> README.md
```

This command **echo**es text into (**>>**) a file called `README.md`.
We use `#` to represent a header in Markdown (don't worry about this for now).
Now, let's see how our repository has changed using `git status`.

```
$ git status
  On branch master

  No commits yet

  Untracked files:
    (use "git add <file>..." to include in what will be committed)
          README.md

  nothing added to commit but untracked files present (use "git add" to track)
```

***

### Git Staging

Let's have a short aside about `git` staging.
In a repository, there are a few important terms.
We code in the **working directory**, and this is where we make changes to files.
To interact with `git`, which is our version control, we need to tell `git` about our files.
Files that are in our **working directory** are **unstaged** until we add them to version control.
Once added, these files are **staged** for changes, and will be included in the next **commit**.
Try not to overthink this.
Just remember that changes need to be **staged** for `git` to recognize them.

***

Now, let's tell `git` about our new `README.md`.

```
$ git add README.md
$ git status
  On branch master

  No commits yet

  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   README.md
```

`git` has our `README.md` file successfully staged.
Finally, let's **commit** our changes.
We'll need to include a message with our commit as well.

```
$ git commit -m "add README.md"
  [master (root-commit) 1234abc] add README.md
   1 file changed, 1 insertion(+)
   create mode 100644 README.md
```

Great! Now, your file has been committed. Try running `git status` to see what has changed.
Last, but not least, we'll need to get our `README.md` from our local computer to our remote repository.
First, we need to tell `git` where our remote repository is.

```
$ git remote add origin https://github.com/foo/foo.github.io
```

`origin` is a custom name that is standard for our remote repository.
Now, we can **push** from our local **master** branch (where we have been working) to our remote **origin** repository.

```
$ git push -u origin master
  Enumerating objects: 3, done.
  Counting objects: 100% (3/3), done.
  Writing objects: 100% (3/3), 235 bytes | 235.00 KiB/s, done.
  Total 3 (delta 0), reused 0 (delta 0)
  To https://github.com/foo/foo.github.io
   * [new branch]      master -> master
  Branch 'master' set up to track remote branch 'master' from 'origin'.
```

We use `-u` to specify our **upstream** repository.
Next time, we can do `git push` without specifying branches because `-u` chooses defaults for us.
Now, navigate to your repository on GitHub.
You should see **Hello World** on the page.

## Create an index page for your website

Make sure you have cloned this repository first.
Copy the sample `index.html` from this repository to your repository.

```
$ cp ../git-started/index.html .
```

Now, with your text editor of choice, edit the `index.html` file as much or as little as you want (name, title, etc.).
This file will be the entry point for your website.
Don't worry about making many, or even any, changes right now; you can always change it later.

NOTE: I use `vim` to edit text (look up `vimtutor` if you want to learn it easily) and highlighy recommend it to anyone who is serious about coding.

Next, let's **stage** the file for changes.

```
$ git add index.html
```

Let's commit our changes with a message.
Notice that commits use the present tense for verbs!

```
$ git commit -m "add initial website index.html"
  [master (root-commit) 1234abc] add initial website index.html
   1 file changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 index.html
```

Finally, let's push our changes. We don't need to specify upstream this time.

```
$ git push
  Enumerating objects: 4, done.
  Counting objects: 100% (4/4), done.
  Delta compression using up to 8 threads
  Compressing objects: 100% (2/2), done.
  Writing objects: 100% (3/3), 294 bytes | 294.00 KiB/s, done.
  Total 3 (delta 0), reused 0 (delta 0)
  To https://github.com/foo/foo.github.io
     1234abc..1234abc  master -> master
```

## Publishing website on GitHub Pages

Let's publish our website.
Go to GitHub, and find your repository (e.g. `https://github.com/foo/foo.github.io`).
At the top right of your repository page, click the `Settings` button.
Scroll down to the `GitHub Pages` section.
Under `Source`, click the dropdown and select the `master` branch.
Click `Save`, and when the page refreshes, you can scroll down and view the link for your website.
Click the link, and you will see your website.
Done!

