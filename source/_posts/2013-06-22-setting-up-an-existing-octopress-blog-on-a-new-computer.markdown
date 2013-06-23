---
layout: post
title: "Setting up an Existing Octopress Blog on a New Computer"
date: 2013-06-22 12:52
comments: true
categories: meta 
---
This information comes from a [post](http://code.dblock.org/octopress-setting-up-a-blog-and-contributing-to-an-existing-one) by [@dblockdotorg](https://twitter.com/dblockdotorg) which was down today while I was trying to set my blog up on a fresh OS install. Therefore, I'm mirroring that content here in case it is unavailable in the future.

    $ git clone git@github.com:username/username.github.com.git
    $ cd username.github.com
    $ git checkout source
    $ mkdir _deploy
    $ cd _deploy
    $ git init
    $ git remote add origin git@github.com:username/username.github.com.git
    $ git pull origin master
    $ cd ..
