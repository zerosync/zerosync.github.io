---
layout: default
title: ZeroSync
subtitle: effortless, simple file syncing
---

The project takes place during the winter semester 13/14 at the [University of Applied Science Wiesbaden](http://www.hs-rm.de/en/dcsm-faculty/degree-programs/applied-computer-science-bsc/index.html), Germany. It is going to be developed in the context of the Independent Study Module. 

> **Please Note!** <br/> ZeroSync is the code name for the offical project title **Eine Cloud-Folder Anwendung**.

## ZeroSync in a Hundred Words

ZeroSync aims to take the best features of Dropbox, Owncloud, Sparkleshare, BitTorrent Sync and other cloud sync products. It focuses on a pure peer to peer communication strategy where all components desktop client, server, mobile app and web app are equal and only differ in the extra service they provide. The key features will be ultra fast file synchronization ranging from small to super large files, a version control system, secure peer to peer communication , a simple straightforward user management and one time access. The overall goal should a *zero effort* and *intuitive* user experience. ZeroSync is LGPLv3 open source.

## Motivation

During the winter break in January 2013 I (@sappo) finally had some time to build my own private cloud. I needed an easy to setup, comfortable to use solution with version control that would run on my raspberry pi.
At first I tried owncloud. The especially rich feature set of this project really excited me. After doing lots of optimization on my pi starting from overclocking, reducing the memory footprint to pushing php to it's edge and more, I still was stuck with an incredible slow syncing process. It would take almost 45 minutes to sync 300 files on my local LAN. Next I tried Sparkleshare. It has proven itself as stable and I even used it for a couple of weeks with fellow students. By using git under the hood it offers a popular version control system. The problem with, rolling back changes is a really laborious process and it's just not optimized for handling large files. When BitTorrent Sync hit the web later 2013 I was amazed by the ease of use. With the peer to peer features I knew from BitTorrent and it's great discovery functionality it's currently my preferred solution. Even thought BitTorrent isn't open source and is also missing a version control.
As none of the above mentioned project offered a real solution to my problem I started the idea of ZeroSync.

## Planned components
> **Please note!** <br/> The features described below and on the component's wikis goes beyond the project's scope. Each participant of the project can choose their own workload depending on their personal skill. The component's use cases within the wiki are just ideas on how the component might work. **You shape the details!** 

###Core library
The core library implements common functionality every component requires. Every component embedding the core will become an _ZeroSync Participant_. ZeroSync libzs is going to handle the peer to peer communication between participants. It also provides a simple version handling participants can leverage. Further it will pass updates from other participants to store and request to provide data to other participants. Components are different from a storing and providing data point of view. So the implementation for storing and providing data can't be part of the core itself and needs to be implemented within the components. A desktop client for example stores and provides data by accessing the local file system, a mobile clients may do so as well. On the other hand a server has to store files in some sort of content repository due to the version control it offers and query them when requested to provide. Ans a web app doesn't store any data but may request the metadata and single files for download.<br/> 
Another part of the core will be a discovery functionality which will work at least for the local LAN.

### File sync client
The clients primary task is to watch the file system for changes. Each operation system (Linux, Mac and Windows) has there own methods and functions for this. Therefore each OS needs an own watch implementation.  But we don't have to start from scratch here. Open source projects like owncloud already handling this pretty well. One idea could be to fork their client and only use the file system watch part. In case of an updated file the client will inform others about the change. And provide the data once they request it.

### File sync server
The server is just another participant within the peer to peer network. It adds a version control system that can be accessed by a special API. Viewing older version of a file and restoring them will be part of the web app. The API enables each participant to add these features. The version control will happen automatically once a new or updated files is received from another participants. The server also provides files to other clients when requested to. 

### Web App Interface
It provides services for administrative tasks, browsing and downloading the files

### Android/iOS Client
Provides partial sync e.g. for music or videos

> **Programming Language!** <br/> The core library will be entirely written in C due to performance reasons. The other components can be implemented in any language. **You choose your own weapon!**

## Interested?

Check out the components and their wikis

* Core library [libzs](http://libzs.zerosync.org) [wiki](http://wiki.libzs.zerosync.org)
* File sync client [zeroclient](http://zclient.zerosync.org) [wiki](http://wiki.zclient.zerosync.org)
* File sync server [zeroserver](http://zserver.zerosync.org) [wiki](http://wiki.zserver.zerosync.org)



