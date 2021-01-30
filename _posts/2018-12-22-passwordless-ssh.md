---
layout: post
author: Dougie
category: programming
---

Passwordless SSH access is convenient, especially as everything is on my local network. I only really access the Pi remotely and you can configure it to use RSA keys. I’m on Ubuntu Linux so open a terminal and create an RSA key (if you don’t have one):
```
ssh-keygen -t rsa
```
<!-- more -->
You’ll need to upload it to the Pi:
```
ssh-copy-id username@ip_address
```

Now because I can’t be bothered to remember IP addresses, I added a line to /etc/hosts:
```
ip_address     raspi
```

That means that I need to add a more specific entry to the ~/.ssh/known_hosts file to allow for the IP address and name:
```
ssh-keyscan -Ht rsa raspi,ip_address >> ~/.ssh/known_hosts
```

You’ll be asked for a password to unlock the keyring in Ubuntu when you first login but otherwise that’s you with passwordless ssh! You’ll need a static IP address. I couldn’t be bothered messing about with it personally so left the Pi using Dynamic IP allocation and set my router to always give the same address.
