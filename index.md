---
layout: default
title: Home
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
permalink: /
---

# BENDOCS YO, I'll put cool stuff here at some point.....
{: .fs-9 }

## DOCKER (NEEDS PAGE)

* Start all stopped containers
* `sudo docker start $(docker ps -a -q)`


## MOUSE LAGGING
* If mouse is lagging, change the wifi channel (2.4GHZ seems to be the main culprit)


## ADD THIS INFO FOR SSH KEYS:

There are 3 things you would need to do in order to switch to a using an ssh key rather than a password.

The first step would be to generate an ssh key. On your machine, in the terminal run the following command

 ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
When you’re prompted to “Enter a file in which to save the key,” press Enter. This accepts the default file location.

Now you should have an SSH key located in

~/.ssh/id_rsa.pub
Copy the contents of the file.

The second step is to add the key to your Droplet. To do that, SSH to it

ssh root@YOurDropletIp
Once you are in open the following file and paste what you’ve copied for your ssh key in it

nano ~/.ssh/authorized_keys
Inside the file on the last line, paste it. Disclaimer, it should all be on one line!

Now you’ve added your SSH key.

The third step is to enable key authentication on the droplet. While you are on the droplet open the following file

nano /etc/ssh/sshd_config
Inside the file, search for a directive called PubkeyAuthentication. This may be commented out. Uncomment the line and set the value to “yes”. This will enable your ability to log in through SSH using ssh keys:

PubkeyAuthentication yes
Save and close the file when you are finished. To actually implement the changes we just made, you must restart the service.

service ssh restart
That’s it you now can ssh with a key rather than a password.

Regards, KDSys
