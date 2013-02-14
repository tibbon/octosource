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


### So back up, what is this Git thing?

Git is distributed version control. It was written initially for better management of the Linux source code. It is Free Open Source Software. Essentially, it allows multiple people to work on a document (or series of documents) all at once, and generally not step on each other's toes. 

Github is a platform for storing, sharing and working with Git repos. A repo is a set of related files which one or more people can work on. 

### Collaborating on Writing and Documentation via Github

Git via the command line can be daunting. Thankfully, there are several tools that can make this significantly easier, including [Github](https://github.com); a web-based hosting service for software development projects that use the Git revision control system. 

To start, sign up for a free account on Github. Then, go to a user's repo that you'd like to help edit, such as the [repo for my blog](https://github.com/tibbon/octosource). Blog post files are kept in the `source/_posts` directory. Click on a blog post such [as this one you're reading](https://github.com/tibbon/tibbon.github.com/blob/master/source/_posts/2013-02-14-how-to-use-git-for-collaborative-blog-editing.markdown). If you hit the 'Edit' button, you will see an [editing window with the contents](https://github.com/tibbon/tibbon.github.com/edit/master/source/_posts/2013-02-14-how-to-use-git-for-collaborative-blog-editing.markdown) of the blog post in Markdown. 

[Markdown](http://daringfireball.net/projects/markdown/) is pretty simple, especially just to edit.

When you're editing hit 'Commit Changes' and initiate a Pull Request. I can now merge it into my blog and update the changes. This should initiate a Pull Request, which will let the maintainer of the repo (and blog) that changes have been made. 

### Other uses of Github for writers

Git and Github can be amazing ways to collaborate on documents. One thing you'll find when browsing Github, and trying to get various programs to work, is that programmers are often terrible documenters. We make a lot of assumptions. But if you can figure out how to make something work, and you edit the documentation- then you can help make it easier for the next person to use. 