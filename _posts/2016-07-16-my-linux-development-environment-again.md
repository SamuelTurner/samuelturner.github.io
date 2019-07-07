---
layout: post
title: "My Linux Development Environment&hellip; Again"
excerpt: "How I set up my development environment using Kubuntu"
background: /images/kubuntu-17.04-banner.jpg
---

Introduction
------------

I play around with my preferred desktop linux environments a lot for various reasons, but every now and again I arrive at a setup I really like and end up sticking with it for a while. This is the latest iteration.

This time around, I've fallen for Kubuntu 17.04 (KDE is just awesome these days), and don't actually need to change very much about it any more&hellip;

Install Kubuntu
---------------

Start by downloading the Kubuntu .iso from [kubuntu.org][kubuntu.org] and install using the [installation guide on userbase.kde.org][kubuntu-installation-guide].

### Enable Trim

If you’re running from an SSD, you should probably [follow this tutorial on enabling trim][enable-trim].

Removing Pre-Installed Software
------------------

I actually like most of the default programs in Kubuntu, so there really isn't much to remove compared to my previous configs.

**Some of these commands use the \* wildcard to remove all related packages. Take great care in checking the list of packages that will be removed.**

    sudo apt remove ktorrent ktorrent-data
    sudo apt remove konversation konversation-data
    sudo apt remove akregator
    sudo apt remove kmail
    sudo apt remove ktnef
    sudo apt remove kaddressbook
    sudo apt remove kontact
    sudo apt remove korganizer
    sudo apt remove knotes
    sudo apt remove skanlite
    sudo apt remove kde-telepathy*
    sudo apt remove kleopatra
    sudo apt remove kate
    sudo apt remove libreoffice*
    sudo apt remove dragonplayer


Installing Preferred Applications
---------------------------------

After removing the bloat, I tend to install most or all of these alternative applications and extras:

    sudo apt install nautilus-dropbox
    sudo apt install flashplugin-installer
    sudo apt install openshot
    sudo apt install htop
    sudo apt install lm-sensors
    sudo apt install terminator
    sudo apt install git
    sudo apt install ssh
    sudo apt install xclip
    sudo apt install vlc

Install Sublime
------------

Follow the instructions on the [Sublime Text installation page][sublime-text-install].

Install VirtualBox
------------------

[Follow this guide to install virtualbox][virtualbox-installation-link].

Install Jekyll Dependencies
---------------------------

This blog uses the [Minimal Mistakes][minimal-mistakes] Jekyll theme, and relies on a few packages being installed so the required gems can be installed..

    sudo apt install ruby ruby-dev ruby-bundler libffi-dev zlib1g-dev liblzma-dev g++ autogen autoconf libtool

Finished!
---------

All done! That’s pretty much all I need, but I’ll keep updating this
post as I change things.

  [kubuntu.org]: http://kubuntu.org
  [kubuntu-installation-guide]: https://userbase.kde.org/Kubuntu/Installation
  [enable-trim]: http://www.webupd8.org/2013/01/enable-trim-on-ssd-solid-state-drives.html
  [virtualbox-installation-link]: http://tecadmin.net/install-oracle-virtualbox-on-ubuntu/
  [minimal-mistakes]: https://mademistakes.com/work/minimal-mistakes-jekyll-theme/
  [sublime-text-install]: https://www.sublimetext.com/docs/3/linux_repositories.html
