---
layout: post
title: "Installing Composer in Manjaro"
excerpt: "Short guide on installing composer in Manjaro"
background: /images/manjaro-banner.jpg
---

I couldn’t find instructions anywhere for installing composer in
Manjaro. I managed to get it working using [the technique described for
Arch in this article] but had to do the steps in a different order.

Editing php.ini
---------------

In Manjaro we need to change the php.ini file so that Composer can
install.

Open php.ini for editing from the command line:

    sudo gedit /etc/php/php.ini

Locate and uncomment the following lines:

    extension=openssl.so
    extension=phar.so

Search (ctrl + f) for the `open_basedir` and add the following to the
end of the line:

    :/usr/local/bin/:/root/

Save and close the `php.ini` file.

Downloading and Installing Composer
-----------------------------------

Download and install Composer from the command line:

    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer

Restart the httpd server:

    sudo systemctl restart httpd

Update composer:

    sudo composer self-update

That should be everything sorted!

  [the technique described for Arch in this article]: https://coderwall.com/p/-hwixa
