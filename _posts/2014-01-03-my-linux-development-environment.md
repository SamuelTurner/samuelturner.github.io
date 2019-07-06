---
layout: single
title: "My Linux Development Environment"
excerpt: "How I tend to set up my development environment using Xubuntu"
comments: false
author_profile: true
categories:
    - Linux
    - Development
header:
    overlay_color: "#000"
    overlay_filter: "0.5"
    overlay_image: /images/xubuntu-banner.jpg
    caption: "Photo credit: [**SapphireGD**](http://sapphiregd.com)"
    teaser: images/xubuntu-teaser.jpg
---

I first wrote this post over a year ago when I was setting up my desktop
and laptop using Linux Mint, in order to give me a reference to follow
when setting up a new computer. Since then I’ve scrapped Mint, Manjaro
XFCE, Manjaro KDE and finally settled on Xubuntu. It gives the
simplicity and huge community of Ubuntu, without all the bloatware and
with the XFCE interface.

I’ve cut out much of the original post, as it was just me trying to
justify my preferences. This is just how I like to do things.

Install Xubuntu
---------------

Just download the Xubuntu .iso from [xubuntu.org][xubuntu.org] and install
using the [installation guide on help.ubuntu.com][ubuntu-installation-guide].

### Enable Trim

If you’re running from an SSD, you should probably
[follow this tutorial on enabling trim][enable-trim].

Speed-Up Tweaks
---------------

You can find plenty of tips and hints in [this post][speed-up-tweaks] and
[this post][speed-up-tweaks-2] and lots of places on Google, but there are
a couple of things that I do that seem to make a difference to me.

### Adjust the Swappiness

This didn’t effect my boot time, but I did notice that my system feels
much “snappier” after the change. To find out what your swappiness is
set to, run this command from the terminal:

    cat /proc/sys/vm/swappiness

If the value is the default (60) then lowering it (I tend to lower it to
10) can give you a welcome speed boost in certain situations. To do so
you need to edit the `sysctl.conf` file:

    sudo gedit /etc/sysctl.conf

Scroll to the bottom of the file, and add the following line:

    vm.swappiness=10

Click save, close and then restart the system for the change to take
effect.

### Install Preload

Preload keeps an eye on what you do and what programs you use most, and
preloads them for a faster boot and snappier operation. This decreased
my boot time by about 15%. You can run your own config for Preload, but
the default one works just fine for me.

    sudo apt-get install preload

Removing Bloatware
------------------

I like to remove a few things I never use or don’t get on with just to
tidy up the launcher and reduce the number of packages that get updated
when I update.

**Some of these commands use the \* wildcard to remove all related
packages. Take great care in checking the list of packages that will be
removed.**

    sudo apt-get remove gimp*
    sudo apt-get remove abiword*
    sudo apt-get remove pidgin*
    sudo apt-get remove thunderbird*
    sudo apt-get remove xchat*
    sudo apt-get remove transmission*
    sudo apt-get remove simple-scan
    sudo apt-get remove gnumeric*
    sudo apt-get remove parole
    sudo apt-get remove gmusicbrowser
    sudo apt-get remove file-roller*
    sudo apt-get remove software-center*
    sudo apt-get remove mousepad*
    sudo apt-get remove onboard*
    sudo apt-get remove gnome-mines*
    sudo apt-get remove gnome-sudoku
    sudo apt-get remove xfburn
    sudo apt-get remove xfce4-notes*

Installing Preferred Applications
---------------------------------

After removing the bloat, I tend to install most or all of these alternative applications and extras:

    sudo apt-get install nautilus-dropbox
    sudo apt-get install flashplugin-installer
    sudo apt-get install banshee
    sudo apt-get install vlc
    sudo apt-get install xarchiver
    sudo apt-get install gedit
    sudo apt-get install lame
    sudo apt-get install asunder
    sudo apt-get install openjdk-7-jre
    sudo apt-get install openshot
    sudo apt-get install htop
    sudo apt-get install lm-sensors
    sudo apt-get install libreoffice

### Install Skype

[Install the latest skype in Xubuntu][installing-skype].

Install LAMP
------------

I just follow the the [Ubuntu guide to installing LAMP][installing-lamp].

Install mcrypt for PHP
----------------------

First install the packaged and enable mcrypt.

    sudo apt-get install mcrypt
    sudo apt-get install php5-mcrypt
    sudo php5enmod mcrypt

This only gives mcrypt and php the ability to work together, but not
with apache. To do so, you must edit apache2’s php.ini file:

    sudo nano /etc/php5/apache2/php.ini

Then add the following line under the dynamically compiled extensions
section of php.ini:

    extension=mcrypt.so

Then restart apache2:

    sudo service apache2 graceful

Install PHPMyAdmin
------------------

Run the following command and follow the prompts:

    sudo apt-get install phpmyadmin

Once done, save and close the file. All that is left is to restart
Apache in order to get PHPMyAdmin to run.

    sudo service apache2 graceful

Install Atom
------------

This installs Atom from the ppa.

    sudo add-apt-repository ppa:webupd8team/atom -y &&
    sudo apt-get update &&
    sudo apt-get install atom -y

Install Ruby with RVM
---------------------
I do an awful lot with Ruby alone, but it’s also required to run many
tools I use. Installing Ruby with RVM allows you to have multiple
versions of Ruby installed and switch between them as needed. First off
you’ll need to install curl:

    sudo apt-get install curl

Next you’ll have to use curl to download and compile RVM. (This will
take some time)

    sudo curl -L https://get.rvm.io | bash -s stable --ruby

To start using RVM you need to run the following:

    source ~/.rvm/scripts/rvm

RVM will install with the latest stable version of Ruby, which at the
time of writing is Ruby 2.0.0. If you need any older versions, just run:

    rvm install x.x.x

If you have installed an older version of Ruby that you want to use as
the default version, simply run:

    rvm use x.x.x --default

Install RubyGems
----------------

If you’re going to do anything with Ruby, you’re probably going to need
to install gems, so you’ll need RubyGems:

    sudo apt-get install rubygems

Install SASS
------------

SASS is a ruby gem, so installing it is very simple: (Note that no sudo
is used, as I want to install SASS in the default version of Ruby within
RVM)

    gem install sass

Install Git
-----------

    sudo apt-get install git

Next you need to configure Git slightly.

    git config --global user.name "username"
    git config --global user.email "your_email"

Install VirtualBox
------------------

[Follow this guide to install virtualbox][virtualbox-installation-link].

Install Composer
----------------

I build a lot of stuff in Laravel, which requires Composer. I tend to
install it globally so that I can call it easily with `composer` rather
than `php composer.phar`.

    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer

Finished!
---------

All done! That’s pretty much all I need, but I’ll keep updating this
post as I change things.

  [xubuntu.org]: http://xubuntu.org
  [ubuntu-installation-guide]: https://help.ubuntu.com/community/Installation?action=show&redirect=InstallingXubuntu
  [enable-trim]: http://www.webupd8.org/2013/01/enable-trim-on-ssd-solid-state-drives.html
  [speed-up-tweaks]: http://community.linuxmint.com/tutorial/view/114
  [speed-up-tweaks-2]: http://www.upubuntu.com/2012/06/11-tips-to-speed-up-computers-running.html
  [installing-skype]: http://xubuntugeek.blogspot.co.uk/2012/10/how-to-install-latest-skype-in-xubuntu.html
  [installing-lamp]: https://help.ubuntu.com/community/ApacheMySQLPHP
  [virtualbox-installation-link]: http://tecadmin.net/install-oracle-virtualbox-on-ubuntu/
