---
layout: post
title: "Fixing Bluetooth Headphone Sound Quality in Ubuntu 16.04"
excerpt: "How to fix sound quality issues with bluetooth headphones in 16.04 LTS"
background: /images/ubuntu-banner.jpg
---

For as long as I've used 16.04 LTS in all flavours - I've had the same issue with my bluetooth headphones sounding terrible. This is due to an inability to select the A2DP profile for "High Fidelity Playback" and it defaulting back to the "Headset Head Unit".

This method is roughly described in a [comment on Stack Overflow][slack-comment], but I'm going to flesh it out a bit.

First, install Bluetooth Manager:

	sudo apt install blueman

Next, edit the config file for bluetooth&hellip;

	sudo nano /etc/bluetooth/main.conf 

&hellip;and add the following lines:

	Disable=Headset
	Enable=Source

Now just restart the bluetooth service:

	sudo service bluetooth restart

From now on, when you need to manage any bluetooth devices, do so through Bluetooth Manager.

That's it! The original comment does mention installing `pavucontrol` as well, but I've not needed to install it so far.

[slack-comment]: https://askubuntu.com/questions/863930/bluetooth-headset-cant-set-a2dp-high-fidelity-playback-poor-sound-quality/864312#864312
