---
layout: single
title: "Superlight Ubuntu Installation"
excerpt: "Starting with the mini.iso and building a lightweight desktop OS out of it"
comments: false
author_profile: true
categories:
    - Linux
    - Development
header:
    overlay_color: "#000"
    overlay_filter: "0.5"
    overlay_image: /images/ubuntu-banner.jpg
    caption: "Photo credit: [**FreewallSource**](http://freewallsource.com/desktop-ubuntu-wallpaper-20344.html)"
    teaser: images/ubuntu-teaser.jpg
---

I have spent the last couple of years distro-hopping and playing around
with different software, and I realised that no matter what distro I
tried out I was removing most, or all, of the pre-installed software and
installing my own preferred stuff, so thought I could try starting from
fresh instead!

<!--more-->

[I used this article as my starting point] and worked from there.

Installing the Base OS
----------------------

Download the [mini.iso] and run through the installation, leaving all
the options blank when it prompts you as to which ubuntu OS you want to
install, so that it just installs the base OS.

Disable Recommends
------------------

I prefer to disable recommends, as it massively reduces how many
packages get installed and I’m yet to find I need much of the
recommended stuff.

    echo 'APT::Install-Recommends "false";' | sudo tee /etc/apt/apt.conf.d/60recommends

Enable Trim
-----------

If you’re running from an SSD, you should probably [follow this tutorial
on enabling trim].

Speed-Up Tweaks
---------------

You can find plenty of tips and hints in [this post] and [this post][1]
and lots of places on Google, but there are a couple of things that I do
that seem to make a difference to me.

### Adjust the Swappiness

This didn’t effect my boot time, but I did notice that my system feels
much “snappier” after the change. To find out what your swappiness is
set to, run this command from the terminal:

    cat /proc/sys/vm/swappiness

If the value is the default (60) then lowering it (I tend to lower it to
10) can give you a welcome speed boost in certain situations. To do so
you need to edit the `sysctl.conf` file:

    sudo nano /etc/sysctl.conf

Scroll to the bottom of the file, and add the following line:

    vm.swappiness=10

Save and exit the file.

### Install Preload

Preload keeps an eye on what you do and what programs you use most, and
preloads them for a faster boot and snappier operation. This decreased
my boot time by about 15%. You can run your own config for Preload, but
the default one works just fine for me.

    sudo apt-get install preload

Reboot the system to apply these changes.

    sudo shutdown -r now

Install the GUI
---------------

I’m currently favouring the Xubuntu flavour of XFCE4 so I’ve just copied
most of this from the article I mentioned earlier. These packages
install the GUI, gets the icons working, adds the sound settings
manager, the network manager and a few bits and bobs.

    sudo apt-get install xubuntu-desktop xfce4-volumed xfce4-indicator-plugin xfce4-netload-plugin xfce4-screenshooter xubuntu-icon-theme xfwm4-themes thunar-archive-plugin indicator-sound indicator-application pavucontrol menulibre librsvg2-common hicolor-icon-theme xdg-utils libgtk-3-bin gvfs-backends gvfs-fuse network-manager-gnome gnome-keyring fonts-liberation fonts-droid unetbootin

Install the power manager (optional)
------------------------------------

If you run a laptop, then you’ll probably want the power manager
installed.

    sudo apt-get install xfce4-power-manager indicator-power

Install the whisker menu (optional)
-----------------------------------

If you want to run the whisker menu (as I usually do), install it.

    sudo apt-get install xfce4-whiskermenu-plugin

Install my basic software
-------------------------

This is my list of basic software and helpful packages that I tend to
install on whatever distro I’m running at the time.

    sudo apt-get install terminator firefox flashplugin-installer galculator evince gucharmap gparted hardinfo lm-sensors phoronix-test-suite libnotify-bin libqt4-opengl virtualbox virtualbox-dkms virtualbox-qt nautilus-dropbox banshee vlc xarchiver filezilla chromium-browser lame asunder brasero openjdk-7-jre openshot libreoffice-calc libreoffice-writer libreoffice-impress fonts-sil-gentium-basic ttf-dejavu keepass2 ristretto curl ruby git

Install Atom
------------

    sudo add-apt-repository ppa:webupd8team/atom
    sudo apt-get update
    sudo apt-get install atom

Install Skype
-------------

    sudo add-apt-repository "deb http://archive.canonical.com/ $(lsb_release -sc) partner"
    sudo apt-get update
    sudo apt-get install skype

Install LAMP
------------

I just follow the the [Ubuntu guide to installing LAMP.]

Install mcrypt for PHP
----------------------

First install the packaged and enable mcrypt.

    sudo apt-get install mcrypt php5-mcrypt
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

Install SASS
------------

SASS is a ruby gem, so installing it is very simple: (Note that no sudo
is used, as I want to install SASS in the default version of Ruby within
RVM)

    sudo gem install sass

Configure Git
-------------

    git config --global user.name "username"
    git config --global user.email "your_email"

Install Composer
----------------

I tend to install composer globally so that I can call it easily with
`composer` rather than `php composer.phar`.

    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer

Restart
-------

Restart the system now to get to the desktop.

    sudo shutdown -r now

Set up the Panel
----------------

I personally set up my panel almost like Windows XP… It’s embarrassing
but it works for me.

-   Right click the panel and select Panel/Panel Preferences
-   Unlock the panel and drag to the bottom of the screen (grab it in
    the top left corner of the screen)
-   Increase row size to 36px
-   Go to items and set the list up in this order:
    -   Whisker Menu/Application Menu
    -   Separator - expand unticked in config)
    -   Launcher - File Manager
    -   Launcher - Terminal
    -   Launcher - Firefox
    -   Launcher - Atom
    -   Launcher - VirtualBox
    -   Launcher - Keepass
    -   Launcher - Skype
    -   Launcher - Banshee
    -   Separator - expand unticked in config
    -   Window Buttons - untick “show handle”, “switch windows using the
        mouse wheel” and “show windows from all monitors” and tick “show
        flat buttons” in config)
    -   Separator - expand ticked in config
    -   Notification Area (external)
    -   Indicator Plugin (external)
    -   Separator - expand ticked in config
    -   Clock

If you have any extra monitors:

-   Add a new panel and drag to the intended monitor
-   Flick between panel 0 and the new panel on the Display and
    Appearance tabs and make the settings match
-   Go to Items and add Window Buttons
-   Make the Window Buttons config match that of panel 0

  [I used this article as my starting point]: http://flux242.blogspot.de/2014/05/minimal-xubuntu-1404-lts-installation.html
  [mini.iso]: http://cdimage.ubuntu.com/netboot/14.04/
  [follow this tutorial on enabling trim]: http://www.webupd8.org/2013/01/enable-trim-on-ssd-solid-state-drives.html
  [this post]: http://community.linuxmint.com/tutorial/view/114
  [1]: http://www.upubuntu.com/2012/06/11-tips-to-speed-up-computers-running.html
  [Ubuntu guide to installing LAMP.]: https://help.ubuntu.com/community/ApacheMySQLPHP
