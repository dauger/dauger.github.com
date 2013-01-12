---
layout: post
title: "Where did My OSX Shell Aliases Go?"
date: 2013-01-12 01:53
comments: true
categories: [osx, bash, pebkac]
---
When it comes to \*nix experience, I'm kind of an odd duck. You see, I've been using Linux quite a bit as a desktop since Mandrake Linux came out (1998?). Also, I learned a little bit about running a \*nix server in the late 90s / early 2000s when I was a Java developer. That being said, I never really tried to develop on a *nix system until late 2010 when I bought a Macbook Pro to learn Ruby. I'm still playing catch-up in many ways when it comes to fundimentals.

I recently blew away my OSX Mountain Lion install and started from scratch. While I was setting things up again I thought to myself: "I should really create some aliases for show / hide hidden files, because I can never remember the exact syntax." I did a bit of googling and learned that I should put my aliases in ~/.profile. 

Things worked fine for a day or two until I set up my Ruby environment. Somewhere along the way my aliases stopped working. Part of setting up RVM is pathing the ruby environment in a bash config file such as ~/.bash_profile.

It turns out that .profile doesn't get loaded in shell sessions if .bash_profile exists. D'oh!

[What's the difference between .profile and .bash_profile, and when do you configure which? (Mac)](http://superuser.com/questions/278433/whats-the-difference-between-profile-and-bash-profile-and-when-do-you-config)
> When bash is invoked as an interactive login shell, or as  a  non-interactive  
> shell  with the --login option, it first reads and executes commands
> from the file /etc/profile, if that file exists.  After reading that file,
> it  looks  for  ~/.bash_profile,  ~/.bash_login,  and  ~/.profile, in that
> order, and reads and executes commands from the first one that exists  and
> is readable.  The --noprofile option may be used when the shell is started
> to inhibit this behavior.
