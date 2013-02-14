---
layout: post
title: "How to use Git for collaborative blog editing"
date: 2013-02-14 13:25
comments: true
categories: [Git]
---

### Introduction

I've had a few blogs prior, but I wasn't happy with how unfocused they were and I never blogged consistently on a topic. As I've been programming more, I have realized how useful technical blogs have been and I would like to contribute back to the community by having my own where I can share how I have solved problems I have encountered. 

However, I don't feel that I am the strongest writer out there and asked a friend, Rae Alton, to help edit this blog to give it a more consistent tone, pacing and style. Since I am blogging using [Octopress](http://octopress.org/), which is based on [Jekyll](https://github.com/mojombo/jekyll), and I am a huge fan of the [Git](http://git-scm.com/) workflow I asked that she would also use Git and [Markdown](http://daringfireball.net/projects/markdown/) in the editing process. The only catch is, she has never used Git or another version-control system so some documentation is in order. This just happens to create a great blog post demonstrating how one might use a workflow like this for blogging. So here we are. 

### Why Octopress & Git instead of Wordpress?

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

### So back up, what is this Git thing?

Git is distributed version control. It was written initially for better management of the Linux source code. It is Free Open Source Software. 

Github is a platform for storing, sharing and working with Git repos. A repo is a set of related files which one or more people can work on. 

But let's back up just a bit and parse out what Git is, and why its incredibly awesome. 

Say you're working in a group writing an employee handbook. Now one of the issues that quickly arises is how to split up writing it, and then how to put it together. Normally this involves a lot of people kicking around different versions of MS Word documents, often named something like 'handbookV2.doc' and 'handbookV3withfiringpolicy.doc'. You can use Word's track-changes feature and the merge-document feature, but when it comes down to it this is still messy. Later on, it is difficult to figure out who wrote what parts. Keeping completely different versions going is also difficult, and undoing specific additions is hard too. 

But if you use Git, this becomes much easier. You are able to split out different versions (called branches in Git) for different people to work completely independently. Changes can be merged together with ease. If a specific department wants to take their own version of the document and use it (called a fork), then they are able to do that. Everyone is able to get credit for their contributions and there is a great amount of transparency. You can also see who is at fault for writing the 'No Coffee' policy. 

### Collaborating on Writing and Documentation via Github

Git via the command line can be daunting. Thankfully, there are several tools that can make this significantly easier, including [Github](https://github.com); a web-based hosting service for software development projects that use the Git revision control system. 

To start, sign up for a free account on Github. Then, go to a user's repo that you'd like to help edit, such as the [repo for my blog](https://github.comt/tibbon/octocode). Blog post files are kept in the `source/_posts` directory. Click on a blog post such [as this one you're reading](https://github.com/tibbon/tibbon.github.com/blob/master/source/_posts/2013-02-14-how-to-use-git-for-collaborative-blog-editing.markdown). If you hit the 'Edit' button, you will see an [editing window with the contents](https://github.com/tibbon/tibbon.github.com/edit/master/source/_posts/2013-02-14-how-to-use-git-for-collaborative-blog-editing.markdown) of the blog post in Markdown. 

[Markdown](http://daringfireball.net/projects/markdown/) is pretty simple, especially just to edit.

When you're editing hit 'Commit Changes' and initiate a Pull Request. I can now merge it into my blog and update the changes. This should initiate a Pull Request, which will let the maintainer of the repo (and blog) that changes have been made. 

### Other uses of Github for writers

Git and Github can be amazing ways to collaborate on documents. One thing you'll find when browsing Github, and trying to get various programs to work, is that programmers are often terrible documenters. We make a lot of assumptions. But if you can figure out how to make something work, and you edit the documentation- then you can help make it easier for the next person to use. 