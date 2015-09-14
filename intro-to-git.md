---
title: Introduction to Git
author: Alexey Shiklomanov
---

# Why version control?

> An essential aspect of creativity is not being afraid to fail.
> --- Edwin Land

How often do you use the "undo" function on your computer? If you're anything 
like me, it's multiple times a *minute*. In other words, I make mistakes or 
second-guess my decisions almost constantly while working. The fact that my 
computer keeps a history of every action I perform and allows me to instantly 
revert them has not only saved me countless hours but also given me the 
courage to try new things without worrying about causing lingering damage.

Now, imagine if you had finer control over the "undo" feature. For instance, 
what if you want to see a history of everything you've done without actually 
reverting?  Or, what if you wanted to try something new but have quick and 
easy access to an older, working version in case you broke something?  
Moreover, what if you wanted to do any of these things while collaborating on 
a project with multiple people?

Enter **version control**. At its core, version control is a combination of a 
more advanced "undo" feature and a dairy or lab notebook. Whenever you make a 
significant change to whatever you're working on, you save it through your 
version control system along with a note describing what you did and why.  
Eventually, you end up with an annotated history of everything you did to a 
file along with the capability to instantly go back to any point in that 
history. If you're working on a project with multiple people, version control 
also keeps track of who did what and when, so that if something breaks, you 
can quickly and easily follow the paper trail and figure out whom to blame.

If all of this sounds appealing to you, read on! The rest of this page is 
devoted to introducing Git--one of the most popular and powerful version 
control systems in use today.


# Getting started with Git

## Prerequisites

There are multiple graphical user interfaces, application plugins, etc. for 
Git, but I've found that the most robust way to use Git is via the command 
line. After all, every major operating system (yes, even Windows!) has the 
command line, and the git commands for them work exactly the same, so if you 
follow my guide, you will be able to use Git on any computer where it is 
installed. Moreover, if you spend a lot of time working remotely--for 
instance, on a high-performance computer cluster--you will ONLY have the 
command line available to you. And finally, the command line guarantees you 
access to every one of Git's myriad of features, whereas most graphical user 
interfaces restrict you to more common ones.

That being said, to be able to follow this guide, you should have some basic 
knowledge of how to use the command line. In case you don't, here is a quick 
rundown of how to navigate your computer using the command line:

* `cd` -- This is the fundamental navigation tool. It stands for "change 
  directory", where "directory" is the computer science term for "Folder." The 
  usage is simply `cd PATH` where `PATH` is the location of the folder 
  *relative to where you currently are*. For instance, if you start in your 
  `home` folder on OSX/Linux (`C:\Users\username` directory on Windows) and 
  want to navigate to the "Documents" folder, the command is simply `cd 
  Documents` (NOTE that it is case-sensitive). To move up in the folder tree 
  (e.g. to return to the home folder after the previous command), type `cd ..` 
  If you ever get lost, `cd` with no argument will take you back to the home 
  directory (i.e.  where your "Documents", "Pictures", "Downloads", etc.  
  folders probably live).

* `ls` -- This tells you the contents of your current folder (think "list").  
  I instinctively issue `ls` after every `cd` to know what files and 
  directories I'm looking at.

* `pwd` -- "Print working directory". This shows you what directory you are 
  currently in.

These commands will help you navigate the command line, but none of them 
actually do anything. There are more online command line guides out there than 
I could possibly list here, so I'll let you discover those on your own. That 
being said, if you want to learn more about specific ways in which I use the 
command line (and there are many -- I use the command line for pretty much 
every aspect of coding and development), follow the "CLI" section of this 
blog!

## Installation

If you're on a Windows or OSX system, the most straightforward way to install 
git is to download the [GitHub app][https://github.com/download] and then have 
it install the command line tools for you. On Linux systems, there is a good 
chance git is already installed (try running `git --version` and see if it 
throws an error), but if it isn't, you can install using standard repository 
management tools (e.g. `apt-get` on Ubuntu, `yum` on CentOS, `pacman` on 
Arch).

On OSX and Linux, you can then open up Terminal and type `git --version` to 
confirm that Git is installed and working. On Windows, your best bet is to use 
the "Git Shell", packaged with the GitHub installation, although an emulator 
like Cygwin or even Windows' native DOS or Powershell will probably work too.

## Creating a repository

Before integrating Git into your real work, I've found it helpful to learn and 
test out Git's features on simple example repository. That way, you can feel 
free to try different commands without the risk of deleting important 
information, and makes it easier to follow along with my directions.

To begin, create a new folder (in any location you choose). You can call it 
whatver you want -- the name doesn't matter and can be changed at any time.  
Once you've created the folder, open up the command line and navigate to that 
directory. Type `ls` and confirm that the directory is empty. 

The command to initialize a Git repository is `git init`. Running it should 
give the following output:

```
Initialized empty Git repository in <directory>/.git
```

This will set up the directory for version control by creating a hidden folder 
containing relevant Git information and files. Run this command and then check 
for the existence of the folder by entering `ls -a` (the `a` flag shows all 
directories in the current path, including those that are hidden).  Don't 
worry about the contents of this folder -- 99% of what you do in Git will 
never require you to look in there -- but take comfort in the knowledge that 
everything related to Git's knowledge of the repository is in that folder and 
nowhere else. If for whatever reason you want to stop Git tracking the folder 
but keep your files, you can simply delete this hidden Git folder. 

## Tracking a file

Now that we have a folder tracked by Git, let's create a file for Git to 
track.  Using a plain text editor like Notepad or TextEdit, create a blank 
text file called `file1.txt` in your Git test folder. Confirm that the file is 
there with the `ls` command. Once that's done, enter `git status`. You should 
see the following:

```
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	file1.txt

nothing added to commit but untracked files present (use "git add" to track)
```

There are three different ways that Git perceives changes: working, staged, 
and committed. To "save" -- or in Git's lingo, "commit" -- a change, you 
perform the following steps:
1. **Make the actual change.** A "change" can be as little or big as you want 
   -- there are basically no restrictions on how small or large it can be, but 
   when in doubt, smaller changes are better than bigger ones because they are 
   easier to backtrace and undo. Any changes you make before performing the 
   subsequent steps are make in the **working** state and are not saved to 
   Git.  In the above example, our change was creating the file `file1.txt`.

2. **Stage the change**. Staged changes are those that are ready to be 
   committed, but have not been committed yet. The reason that all changes are 
   not automatically committed is that you may want to make multiple changes 
   first and then commit each change separately. Or, more often, you may only 
   want to commit changes to certain files and not others.  Staging is 
   typically done with the `git add <filename>` command, so for our example, 
   run the command `git add file1.txt`.

   Run `git status` again and you will see the following helpful information.

```
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   file1.txt

```

   The change we made -- the addition of `file1.txt` -- will be committed, or 
   permanently saved, the next time we run `git commit`. However, if we change 
   our minds, at this point, we are free to "unstage" that change (by running 
   `git reset HEAD <name of staged file>` -- don't worry about what all of 
   this means yet) and/or add more changes as we see fit. You can use `git 
   add` to stage changes as many times as you want before actually committing.
   
3. **Commit the change**. This is where you make a note describing the change 
   the change you made and why you made it and then save the change to Git's 
   history. Running `git commit` by itself will open up a simple text editor 
   asking you to write a commit message. If you feel comfortable using 
   something like "nano" or "vi" to edit files in terminal, proceed with that; 
   otherwise, a simpler approach is to enter your message directly into the 
   command by running `git commit -m "<your message here>"` (making sure to 
   surround the message in quotes. For our example, enter the following: `git 
   commit -m "Created file1.txt"` and you will see the following summary of 
   the change:

```
[master (root-commit) 810e800] Created file1.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file1.txt
```

*__NOTE__: At this point, Git may ask you for some information if it doesn't 
have it already, such as your name and email.  This is used to store **who** 
committed each change in the history, which is very useful for collaborations.  
This information is a global setting, so once you set it for the first time on 
your computer, you never have to do it again (unless you want to change it).*

One critical feature of Git is the ability to view your revision history. This 
can be done via the `git log` command, which returns the full list of past 
commits for a repository:

```
commit 810e800fb4f35d18f06fd385212b7d1830c0f099
Author: <your name>
Date:   <the current date and time>

    Created file1.txt
```

That long string of letters and numbers after "commit" is the automatically 
assigned unique identifier of the commit. When you refer to commits in Git 
commands, you have to use this ID rather than the commit message or anything 
else like that. Fortunately, you don't have to use the entire string -- the 
first 6 characters will do in just about any reasonable case. More on that 
later...

## Editing a file

Our first change created a new file. Now, let's edit it! 

First, for illustrative purposes, run `git status` and you should see the 
following:

```
On branch master
nothing to commit, working directory clean
```

This is good! It means all of our changes are committed to Git's history. Now, 
fire up your text editor of choice, add some text to your `file1.txt`, and 
save it. Run `git status` again and you will see the following message:

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   file1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Git recognizes that the version of `file1.txt` currently in the directory is 
different from the one at the end of one it has saved, so it detects that a
change has been made. To see exactly what has changed, you can use `git diff`, 
which shows all of the unstaged changes made since the last commit:

```
diff --git a/file1.txt b/file1.txt
index e69de29..e965047 100644
--- a/file1.txt
+++ b/file1.txt
@@ -0,0 +1 @@
+Hello
```

This may look a little bit crypic, but all it's saying is that the line 
"Hello" has been added to the file `file1.txt`. Lines that have been added or 
modified start with `+` while those with deletions start with `-`. The `git 
diff` command has many more powerful uses that you are welcome to explore on 
your own (and that I may address in a later post).

Once you are satisfied with the text you want to add, run `git add file1.txt` 
to stage this change followed by `git commit -m "<message>"` to permanently 
save it. 

## Branching
