---
title: How to setup NextCloud on a Raspberry Pi
date: 2021-06-20 09:12:06
tags:
  - NextCloud
  - Raspberry Pi
categories: cloud
keywords: null
thumbnail: https://www.google.com/url?sa=i&url=https%3A%2F%2Fhelp.nextcloud.com%2Ft%2Fnextcloud-instalation-not-running-on-rpi-8gb-model%2F85325&psig=AOvVaw32iiYkT1C0aFG4yOYwkkvH&ust=1624434944138000&source=images&cd=vfe&ved=0CAcQjRxqFwoTCOCf-vDhqvECFQAAAAAdAAAAABAD
rating: 3
---
I am personally (and digitally) deeply integrated into the Google ecosystem. And because of that I've been feeling a little paranoid because of posts like [this](https://news.ycombinator.com/item?id=26390833) and [this](https://news.ycombinator.com/item?id=24965432). I have been thinking of decreasing my reliance on Google services step by step.

So, when Google discontinued their **Unlimited Free Storage** plan for [Google Photos](https://www.cnet.com/how-to/google-photos-unlimited-free-storage-has-ended-heres-what-to-do-now/), I took it as an opportunity to look for a better alternative. 

Following are some of the open-source solutions that you can self host and use it as an alternative to [Google Photos](https://photos.google.com/):

* [Piwigo](https://piwigo.org/)
* [Photo Prism](https://photoprism.app/)
* [Lychee](https://lychee.electerious.com/)

There is another entry which doesn't exactly fit into this category, But it is helpful for the underlying cause of Backing up your data.

# Introducing Nextcloud

> Nextcloud is a suite of client-server software for creating and using file hosting services.

Nextcloud stores your files in conventional directory like structure and you can also access them using [WebDAV](http://www.webdav.org/). Apart from that it also provides vast range of functionalities through its plug and play architecture where you can install variety of [Nextcloud Apps](https://apps.nextcloud.com/) that suit your requirements.

Plus, it can be hosted on wide variety of hardware appliances with lots of [options](https://nextcloud.com/install/#instructions-server). 

# Raspberry Pi

> The Raspberry Pi is a tiny and affordable computer that you can use to learn programming through fun, practical projects.

You have to be living under a rock if you don't know about these little minions.
I already have a [Raspberry Pi](https://amzn.to/3xGuJqf) which I was using for [Pi-Hole](https://pi-hole.net/), Content streaming on local network and lots of other things.

So, let's dive into how we can setup Nextcloud on Raspberry Pi.

# Pre-requisites

You will need following things before you start:

* [Raspberry Pi](https://amzn.to/3xGuJqf) (Preferably 4 for better performance)
* [SD Card](https://amzn.to/3vEx9E9)
* [USB Drive](https://amzn.to/3cXwIhQ) (Optional)

If you have a smaller SD card than a `3.0` USB drive will help you store your /(root) partition on USB.

# Flash NextCloudPi

There are multiple options to install NextCloud on your Raspberry Pi, But we will cover the easiest one which is to use the [NextCloudPi](https://ownyourbits.com/nextcloudpi/) image.

Follow below steps to flash latest image of NextCloudPi on your Raspberry Pi:

1. Download your [NextCloudPi image](https://ownyourbits.com/downloads/) for RPI.
2. Verify `md5sum` of downloaded archive file with the one mentioned on the website.
3. Extract the archive file.
4. Install [Raspberry Pi Imager](https://www.raspberrypi.org/software/) to flash downloaded image on your SD card.

   * You can also use [Etcher](https://www.balena.io/etcher/) if you like.

* Steps for using Raspberry Pi Imager

  1. Open Raspberry Pi Imager.
  2. Click on Choose OS
  3. Scroll down and click on `Choose Custom`
  4. Select image file that you extracted from the downloaded archive file.
  5. Click on Choose Storage.
  6. Select your SD Card.
  7. Click on Write. (`Note`: This will erase all the data on SD Card.)

5. Remove the SD card and insert it to the Raspberry Pi. Then connect the Raspberry Pi to your home router with an ethernet cable and power on your Raspberry Pi.

# Finding IP Address of Pi

Once you have connected your Pi to your network and it is powered on, You can use one of the tools like [Angry IP Scanner](https://angryip.org/download/) or [nmap](https://nmap.org/) to find its IP address.

# Enabling SSH on Pi

By default SSH access on your Pi will be disabled. You will need to enable it from the webUI of NextCloud. Follow below steps to do so:

1. Go to `https://nextcloudpi` or `https://nextcloudpi.local` 
2. If that doesn't work go to https://`rpi_Address`:4443 in your browser.

   ![Backup your NextCloud password](/images/uploads/activateScreen.png "NextCloud activation screen")
3. Export your NextCloudPi passwords to a secure place.
4. Click on Activate.
5. Do not Refresh if Activation takes some time. If you do your old passwords will be invalidated.

   `Note:` If you forget to take backup of your password before activating NextCloudPi then go to `https://nextcloudpi/activate` to get the password screen again.
   If you see activation successful message than Congratulations!! You have setup NextCloud on your Raspberry Pi.
6. Go to `https://rpi_address:4443/?app=dashboard`
7. Select SSH under Networking from left hand side navigation bar.
      

   ![SSH Settings in NextCloud dashboard](/images/uploads/ssh_nextcloud.png "SSH Settings")
8. Check the **Activate** box.
9. Set the username password and click on **Apply**.

You should be able to login to your Pi using SSH now.

Now that you have your own cloud setup on your local network. What are your inputs on it?
Share your ideas on how you are using it in the comments below.