---
layout: blog
keywords: null
title: Setup your External HDD with NextCloud
date: 2021-06-20 23:12:06
thumbnail: /images/uploads/file.jpg
tags:
  - NextCloud
categories: cloud
rating: 5
---


# Pre-requisites
  - [Raspberry Pi](https://amzn.to/3xGuJqf) with [NextCloudPi](https://ownyourbits.com/nextcloudpi/)


If you need any help, Checkout [How to setup NextCloud on a Raspberry Pi]({{< ref "nextcloud-rpi.md" >}}).

# Install External Storage Support
Open your NextCloud dashboard and go to settings.

You should see External Storage Support app and it should be enabled.
![ESS App](/posts/nextcloud/images/ExternalStorageSupport.png)

If you don't, Search for it by clicking on Search button and click on Download and Enable.

# Plug in your HDD
Connect your HDD with your Pi.
Find your Hard drive's device id by executing following command:

{{< highlight bash >}}
sudo lsblk
{{< /highlight >}}

![lsblk output](/posts/nextcloud/images/lsblk.png)

You will want to mount your Hard drive to a specific location. In my case I am mounting my HDD to `/media/My_HDD`
To do this execute following command:
{{< highlight bash >}}
$sudo mkdir /media/My_HDD             # Create respective directory if doesn't exist
$sudo mount /dev/sda1 /media/My_HDD   # Mount your Hard drive
{{< /highlight >}}

Assign proper privileges so that NextCloud can read your HDD data:
{{< highlight bash >}}
sudo chown -R www-data:www-data /path/to/HDD
sudo chmod -R 0750 /path/to/HDD
{{< /highlight >}}

# Configure External Storage Support
Go to Settings and select External Storage Support to configure your attached HDD with NextCloud.
If you are logging in as Admin user, Select the one under **Administration** and not the one under **Personal**.
![Correct ESS Setting](/posts/nextcloud/images/ExternalStorageSupportsetting.png)

Configure your local storage by entering following details:

- **Folder Name**: Name by which you HDD should be displayed in NextCloud.
- **External Storage**: Local (As we have attached our HDD locally.)
- **Configuration**: Path to where your HDD is mounted
- **Available For**: Access Privileges

![Local storage ESS Setting](/posts/nextcloud/images/local.png)

Click on the ✅ and you are good to go.

How did it go? Feel free to share your thoughts in comments.