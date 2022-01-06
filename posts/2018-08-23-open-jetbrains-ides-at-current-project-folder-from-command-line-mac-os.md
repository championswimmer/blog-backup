---
title: Open Jetbrains IDEs at current project folder from Command Line (Mac OS)
slug: open-jetbrains-ides-at-current-project-folder-from-command-line-mac-os
date_published: 2018-08-22T19:30:08.000Z
date_updated: 2018-08-22T19:46:23.000Z
tags: jetbrains, macos, linux, commandline
excerpt: How to make sure you can open Jetbrains IDEs from command line on MacOS
---

Years of working with Linux means the only way I feel comfortable opening apps is from the command line. One of the biggest reasons why is I can `cd` to any folder and then open my IDE *in that folder* very easily. For example to open current folder in Sublime or VS Code I use - 

    vscode .
    
    # -- or --
    
    subl .

![](/content/images/2018/08/image-4.png)
Doing the same with Jetbrains IDEs (I am a regular user of IDEA, Webstorm and CLion) used to be possible till some time ago, but somehow doesn't work out of the bat for 2018.x versions. So the first thing I tried was creating a **symlink** to the actual launcher script within the .app folder

    sudo ln -s "/Applications/WebStorm 2018.2 EAP.app/Contents/MacOS/webstorm" /usr/bin/webstorm

Problem with that is, I have now started to use the [Jetbrains Toolbox](https://www.jetbrains.com/toolbox/app/) which means the .app folder in which me IDE is, keeps changing every month when I update the IDE. 
![](/content/images/2018/08/image-3.png)
This is where the `open` command in Mac comes in handy. You can *open* an app and pass arguments using the following syntax.

    open -a "App Name" --args arg1 arg2

To make use of it, what I do is I keep launcher scripts in my personal bin folder like `~/usr/bin/idea` and others for *webstorm* and *clion* etc. Here is what my script looks like - 

This way I can launch IDEA on my current folder

    idea .

Or on any folder

    idea /path/to/project

Hope that helps any other fellow Mac OS users out there opening IDEs from command line :) 
