---
layout: default
title: ZeroSync
subtitle: effortless, simple file syncing
---

The project takes place during the winter semester 13/14 at the [University of Applied Science Wiesbaden](http://www.hs-rm.de/en/dcsm-faculty/degree-programs/applied-computer-science-bsc/index.html), Germany. It is going to be developed in the context of the Independent Study Module. 

> **Note** <br/> The offical project title is **Eine Cloud-Folder Anwendung**.

## ZeroSync in a Hundred Words

ZeroSync aims to combine features of Dropbox, Owncloud, Sparkleshare, BitTorrent Sync and other cloud sync products. Providing rapid file synchronization ranging from small to super large files. Additional features include version control, secure peer to peer communication, simple user management and one time access. The overall goal should be *zero effort* and *simplicity* for the user. Another goal for the far future is to add a Dropbox like Datastore API.
ZeroSync is LGPLv3 open source.

## Motivation

During the winter break in January 2013 I (@sappo) finally had some time to build my own private cloud. I needed an easy to setup, comfortable to use solution with version control that would run on my raspberry pi.
At first I tried owncloud. The especially rich feature set of this project really excited me. After doing lots of optimization on my pi starting from overclocking, reducing the memory footprint to pushing php to it's edge and more, I still was stuck with an incredible slow syncing process. It would take almost 45 minutes to sync 300 files on my local LAN. Next I tried Sparkleshare. It has proven itself as stable and I even used it for a couple of weeks with fellow students. By using git under the hood it offers a popular version control system. The problem with, rolling back changes is a really laborious process and it's just not optimized for handling large files. When BitTorrent Sync hit the web later 2013 I was amazed by the ease of use. With the peer to peer features I knew from BitTorrent and it's great discovery functionality it's currently my preferred solution. Even thought BitTorrent isn't open source and is also missing a version control.
As none of the above mentioned project offered a real solution to my problem I started the idea of ZeroSync.

## Planned components
> **Please note!** <br/> The features described below and on the component's wikis goes beyond the project's scope. Members can choose their own workload depending on their personal skill.

###Core library
The core library implements common functionality every component requires. Every component embedding the core will become an _ZeroSync Participant_. ZeroSync libzs is going to handle the peer to peer communication between participants. It also provides a simple version handling where it needs the participant to store or provide data. Components are different from a storing and providing data point of view. So this methods can't be part of the core itself and need to be implemented by the participant. A desktop client for example stores and provides data by accessing the local file system, a mobile clients may do so as well. On the other hand a server has to store files in some sort of content repository due to the version control it offers and query them when requested to provide them by the core. Further the web app doesn't store any data at all but requires the metadata to keep up to date.<br/> 
Another part of the core will be a discovery functionality which will work at least for the local LAN.

### File sync client
The client watches to file system for changes. Each operation system (Linux,Mac and Windows) therefore needs a own watch implementation. It also needs to listen for changes from other clients to keep everything in sync.

### File sync server
It handles the version control of files

### Web App Interface
It provides services for administrative tasks, browsing and downloading the files

### Android/iOS Client
Provides partial sync e.g. for music or videos

> **Programming Language!** <br/> The core library will be entirely written in C due to performance reasons. The other components can be implemented in **any language** you like. 

## Interested?

Check out the components and their wikis

* Core library [libzs](http://libzs.zerosync.org) [wiki](http://wiki.libzs.zerosync.org)
* File sync client [zeroclient](http://zclient.zerosync.org) [wiki](http://wiki.zclient.zerosync.org)
* File sync server [zeroserver](http://zserver.zerosync.org) [wiki](http://wiki.zserver.zerosync.org)

