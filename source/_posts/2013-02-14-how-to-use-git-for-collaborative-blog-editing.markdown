---
layout: post
title: "How to use Git for collaborative blog editing"
date: 2013-02-14 13:25
comments: true
categories: [Git]
---

Introduction
============

I've had a few blogs prior, but I wasn't happy with how unfocused they were and I never blogged consistently on a topic. As I've been programming more, I have realized how useful technical blogs have been and I would like to contribute back to the community by having my own where I can share how I have solved problems I have encountered. 

However, I don't feel that I am the strongest writer out there and asked a friend, Rae Alton, to help edit this blog to give it a more consistent tone, pacing and style. Since I am blogging using [Octopress](http://octopress.org/), which is based on [Jekyll](https://github.com/mojombo/jekyll), and I am a huge fan of the [Git](http://git-scm.com/) workflow I asked that she would also use Git and [Markdown](http://daringfireball.net/projects/markdown/) in the editing process. The only catch is, she has never used Git or another version-control system so some documentation is in order. This just happens to create a great blog post demonstrating how one might use a workflow like this for blogging. So here we are. 

Why Octopress & Git instead of Wordpress?
===========

When I initially what I'm doing here, Rae asked why this is better than Wordpress. Wordpress is used by millions and does have strength in its easy of use and ubiquity. However, it is my opinion that Wordpress has several weaknesses that I find troubling: 

* It is written in PHP. I'm not going to go off on the traditional rant about the weaknesses of PHP, but rather just say that I'm significantly more comfortable in Ruby
* It lacks anything resembling an MVC pattern- or any pattern Every time I touch Wordpress I'm find it impossible to figure out where/why database calls are being made, how the data is structured, and debugging becomes a mess. In constrast, with something more structured like Jekyll or Rails I can easily figure out the lay of the land and debug things. 
* Theming and Plugins in Wordpress are a mess. The code for each of these is of highly inconsitent quality, there are rarely code-based tests, and there's no good dependency manager like [Bundler](http://gembundler.com/) to help keep things in order.
* The versioning that Wordpress offers is nice, but very limited compared to Git, which allows splitting, merging and tracking of changes in an infinite number of ways. This is potentially overkill for a blog, but when Rae makes changes, I can easily see line for line what changes have been made. Wordpress also largely requires that I'm online all the time, and use a GUI to edit things. 
* Wordpress installations often get slow and are heavily database dependant. It isn't uncommon to see a Wordpress page with 100's of SQL queries per page load. Of course this can be optimized, but this becomes problematic when you attempt to upgrade. When using [Disqus](http://disqus.com/) for comments, a blog really doesn't need to be dynamic in my opinion. Octopress generates a static site, which Github will host for me for free, and I can deploy changes with a single command line.
* The security model in Wordpress is incredibly poor by default and leaves a lot of room for misconfiguration easily. Setting up file permissions, storage of database passwords in plain text, editing pages over HTTP, encouraging users to enable FTP, etc... 
* Wordpress (by default) doesn't push for a Git-based workflow to deploy, version and backup the code. I can't count how many Wordpress installations I've seen that just have monthly tar files, or worse renamed folders, to try to version things. 
* I also really don't like MySQL compared to Postgres for a relational database, although as I highlighted above, I don't feel that a blog needs a database. 

This isn't to say no one should ever use Wordpress. For me, I just feel that when weighing out these things that there isn't any compelling reason for me to use it. Octopress delivers everything I could want in a blog, and Git offers a huge amount of power and control. 

So back up, what is this Git thing?
============

Git is distributed version control. It was written initially for better management of the Linux source code. It is Free Open Source Software. 

Github is a platform for storing, sharing and working with Git repos. A repo is a set of related files which one or more people can work on. 

But let's back up just a bit and parse out what Git is, and why its incredibly awesome. 

Say you're working in a group writing an employee handbook. Now one of the issues that quickly arises is how to split up writing it, and then how to put it together. Normally this involves a lot of people kicking around different versions of MS Word documents, often named something like 'handbookV2.doc' and 'handbookV3withfiringpolicy.doc'. You can use Word's track-changes feature and the merge-document feature, but when it comes down to it this is still messy. Later on, it is difficult to figure out who wrote what parts. Keeping completely different versions going is also difficult, and undoing specific additions is hard too. 

But if you use Git, this becomes much easier. You are able to split out different versions (called branches in Git) for different people to work completely independently. Changes can be merged together with ease. If a specific department wants to take their own version of the document and use it (called a fork), then they are able to do that. Everyone is able to get credit for their contributions and there is a great amount of transparency. You can also see who is at fault for writing the 'No Coffee' policy. 

Getting Started
==========

The first, and probably most painful part, is getting Git installed properly and configured with Github. This is going to vary slightly between Windows, Linux and OS X. 

Install the newest version of Git from the main Git site. If you already have Homebrew installed on OS X, then you can try `brew install git` in the terminal. 

This brings to one thing that we'll be using a lot- the terminal or command prompt. Perhaps you've never used the terminal, or perhaps its been a while. First you've gotta open it:

* In Windows, go to the Start menu and click on Run. A dialog box will pop up where you will type 'cmd.exe' and hit enter/click ok. 
* In OS X, click on the Spotlight icon in the upper right hand corner and type 'terminal' and then hit enter when the Terminal application is highlighted. This is also accessible in Applications/Utilities/Terminal. 
* In Linux, you might start off at a terminal prompt (sometimes called bash prompt). If some windowing system runs automatically, there should be something called 'Terminal' or similar in a pretty obvious menu. 

In all of these, once you're at the command prompt you can type things, and then hit enter/return on your keyboard to run them. You can also copy/paste things into this window. If something is stuck and not moving, you can always hit `CTRL-C` on your keyboard to stop whatever is running. You can also make this window and the text bigger, but the detail of that is operating-system specific. 

Once you have Git installed, you can run it from the command line by just typing `git`. Easy enough eh? Unfortunately, running that alone doesn't do incredibly much and we need to configure a few things. 

Using your web browser, create an account on Github. This is free and should take about a minute at most. Make sure to use a decent password that is unique. 

Now, continue to follow the excellent instructions from [Set Up Git](https://help.github.com/articles/set-up-git) article on Github to setup Git's security keys, your username, email, etc. You'll be putting these commands into the terminal that we learned to open above. 

Now we're ready to start using Git!

Using Git for editing an Octopress Blog
==========

First, you need to create a fork of my blog unless you're listed as a contributor on my page (Rae, we'll add you as one, but follow the below anyway). In your web browser, go to [my blog's Github repo](https://github.com/tibbon/octosource) and the the 'Fork' button in the upper right hand area of the page. It makes a copy of my blog in your Github account. Near the middle of the page, there is now a selector for HTTP, SSH and Git Read-Only. Select 'SSH' and copy the URL listed there, which should look like `git@github.com:YOU_USER_NAME/octosource.git`.

Now in your terminal, we're going to type in the code below. What we're doing here is moving to your home directory, creating a new directory called 'code', changing into this directory, cloning your new Git repo (which is a fork of mine), changing into the new directory created, and then finally adding my repo as a 'remote' which we'll use later. 

```
cd
mkdir code
cd code
git clone git@github.com:YOUR_USER_NAME/octosource.git
cd octosource
git remote add upstream git@github.com:tibbon/octosource.git
```

If everything went well, then you should be in a directory with a handful of files. To see the names of them type `ls -al` in Linux/OS X and `dir` in Windows. 

What we need to do next is open up this directory in whatever text editor suits you. On OS X, I use TextMate which isn't free but is awesome. There's a free 30-day trial though. On Windows, you might try something like [Komodo](http://www.activestate.com/komodo-edit) or [Notepad++](http://notepad-plus-plus.org/). Linux has countless options as well. Search on Google for 'open source code editor'. A good one will have code highlighting at least for Markdown. You do not want to use something like Microsoft Word to edit these files. Notepad could work in a pinch, but lacks text highlighting and is generally pretty limited feature-wise.

Blog posts are stored in Octopress in the source/_posts directory. They use a format called Markdown which helps format the text. Take a few minutes a read over the [Markdown documentation](http://daringfireball.net/projects/markdown/). Its cleaner and easier than reading HTML. For the most part if you're just editing it should be relatively self-explainitory.

So, let's say you've opened this blog post, which is stored as `source/_posts/2013-02-14-how-to-use-git-for-collaborative-blog-editing.markdown` and made some changes. Let's see if Git knows that you changed the files. From the terminal try the following:

`git status`

Git knows you've changed the blog post! Every time you change a tracked file, Git knows about it. 

Now, let's push code back to Github, and do a 'Pull Request', which will let me know that changes have been made. We're going to create a 'commit', but first we have to tell Git which files to add to the commit. 

```
git add .
git commit -m "A commit message goes here. This describes the changes that are made. You might say something like you made the second paragraph more clear."
git push origin master
```

Now, go back to your forked Github repo at https://github.com/YOUR-USERNAME/octosource and click 'Pull Request'. Write whatever appropriate for a commit message, and click Ok. You've now made a Pull Request that I can merge in!

But what happens when I start a new blog post for you to edit? You need to 'pull' instead of pushing now. First, make sure all changes you have made are commited by running the add, commit and push lines above. Then run the following:

```
git pull remote upstream
```

This will get changes from my repo, and pull them locally to your machine. You'll likely want to do a `git push origin master` to put these immediately into your repo before you start to edit. Then, when you're done editing just do the add, commit, push cycle again, and do a Pull Request from Github. 

Alternative Method 1
============

Instead of doing all of this, there are two alternatives that are worth mentioning. If you are a contributor on my blog, then you can actually push directly to my repo! Instead of creating your own fork and adding me as a remote, you can do the following instead:

```git clone git@github.com:tibbon/octosource.git
cd octosource
(make a change)
git add .
git commit -m "I made a change!"
git push origin master```

To get new changes after a while, you'd simple `git pull origin master`. Now realistically, you should make what are called 'branches' instead of a fork now, so you can save your own along the way without pushing to 'master'. You should think of the master branch as the canonical/final product. Git branching is a little more complicated and Github has a [wonderful tutorial](http://learn.github.com/p/branching.html) on it. But below is the gist of what you'll do. 

```
git checkout -b grammar-updates  #This creates a new branch called grammar-updates and checks it out for you, so you can now start making changes
(make some changes to files)
git add .
git commit -m "I made lots of changes here"   #You will do the cycle of git add and git commit a lot here, making small changes along the way. Think of them as save points in a game.
git push origin grammar-updates # This will push the grammar-updates branch to Github
git checkout master             # This changes you back to master
git merge grammer-updates       # This merges your changes into master
git push origin master          # This pushes your changes to master to Github.
``` 

Alternative Method 2
=========

The second alternative is to skip all the commandline stuff, and edit directly from a fork on Github. This is good for editing text, but significantly less good for editing real code. Knowing your way around Git is a great job skill and really helps set you apart from the pack. This is clearly the easier method- but I really encourage you to learn the Git workflow manually at some point too!

To edit directly from Github, [go to my repo](https://github.com/tibbon/octosource), browse to `source/_posts/blogpost.markdown` and then click the 'Edit' button. This will create a fork for you, and you can now edit the file in the browser-editor on Github. You can even make it full-screen for editing! When you're done hit 'Commit Changes' and initiate a Pull Request. I can now merge it into my blog and update the changes. 