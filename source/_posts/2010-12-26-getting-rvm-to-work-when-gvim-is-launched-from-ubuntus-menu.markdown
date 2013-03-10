---
layout: post
title: "Getting RVM to Work when GVIM is Launched from Ubuntu's Menu"
date: 2010-12-26 23:01
comments: false
categories: ubuntu
---
If you want to use GVim as your Ruby editor in Ubuntu (and most likely any other Gnome based distro), you've probably found out that your .bashrc file is not read when launching GVim from the Gnome menu. This means that your RVM paths are not available in the scope of apps launched from the menu. However, when launching apps from the menu, the launcher can access your .profile file. That being the case, here is a quick work-around for this issue:

Add the following code to your ~/.profile file:
```bash
# This loads RVM into the session scope of the launcher.
[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"
```
Next create a script that you can use to start up GVim. Example ~/Apps/GVim/gvimstart.sh. In this script, place the following:
```bash
#!/bin/bash
source ~/.profile 
gvim
```
Then right click on the applications menu and choose "Edit Menus". Then find your GVim launcher and point the command entry to your script.

I am, by no means, a Gnome expert, so please let me know if you are aware of a better solution.

Happy coding! 
