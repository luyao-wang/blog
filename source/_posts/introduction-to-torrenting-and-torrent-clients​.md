---
title: Introduction to torrenting & torrent clients​
date: 2017-08-23 21:57:56
categories:
- 程序媛💁‍技术贴
- en 🇺🇸
- school🎓
- theory
tags:
- torrent
- torrenting
- torrent client
- BitTorrent
- Tracker
---

### What is a torrent client?​

A tool that helps assist users in downloading files seamlessly, quickly, and without depending upon a centralized server.​

Implements the BitTorrent protocol. Why use torrenting? We’ll explore this next.​

### Torrenting: Terminologies & Why Torrent?​

Torrents are files that point to a remote server or themselves act as the server. This server contains a list of machines that contain portions of the file(s) to download.

Machines that are downloading a file are known as `“peers”`.​

Machines that contain even just a portion of a file AND are able to share the file are known as `“seeds”`. ​
When multiple machines all are sharing the same torrent file, this is known as a `“swarm”`.​

Torrenting is much faster than utilizing a centralized server for two main reasons:​

- High levels of traffic to a machine can slow down the machine or cause a crash from servicing too many requests at once.​

- BitTorrent protocol allows seeds themselves to *immediately* start sharing information once portions of a file have been downloaded. Another machine does not need to wait for the first machine to finish downloading the file before it can receive parts of the file.​

**`Illustration of a typical BitTorrent Swarm​`**

![](https://raw.githubusercontent.com/webtorrent/bittorrent-tracker/master/img.png)

### Managing Torrents​

The decentralized nature of torrenting is great in theory but for it to work in practice, we’d still need some way of keeping track of all the machines downloading a file (peers) and all the machines that are acting as a container for a file (seeds).​

BitTorrent handles this via a `“Tracker”`. The tracker keeps track of all peers connected in a swarm along with all of the various seeds that peers can connect to, to access a file.​

The tracker also keeps track of what “part” of a file is attached to what machine. This ensures that peers will get the various pieces of data that they need for a file and no duplicate copies of information that has already been attained.​

**`BitTorrent Tracker Diagram​`**
![](http://images.morehawes.co.uk/bittorrent/tracker.png)

### BitTorrent Vulnerabilities : Loss of Seed​

BitTorrent’s use of swarms & multiple seeds for components of a file allows peers to potentially download files faster. Part of this is by allowing machines with only a *portion* of a file to immediately begin transferring data. But what happens if a seed exits a swarm? Do we lose a vital chunk of data?​

No! BitTorrent works around this by way of “rarest first” algorithm. What is the “rarest first” algorithm?​

Each piece of data in a file is assigned a value. Each peer in a swarm has attached with it a reference to those pieces of data. When a new peer joins the swarm, the BitTorrent protocol will look for the data with the lowest reference count (therefore the rarest piece) and will give any and all new peers that section of data before any “common” pieces of information.​

Now if a seed in the BitTorrent swarm goes away (e.g. disconnect), chances are higher that all other peers will have any pieces of data that the lost seed contained.​

### BitTorrent Vulnerabilities: Multiple Requests​

Rarest-first algorithm helps us circumvent the issue of data loss from a seed being removed from a swarm but another pitfall is the bottleneck imposed on each seed of the swarm.​

When a peer requests a portion of a file from a seed, the seed must spend some time accessing the component of the file and stream it to the peer. ​

When too many requests are made to a seed at once, the seed may refuse to communicate with a peer. This is known as `“choking”`.​

To work around choking, BitTorrent will rotate which seed should be targeted by a peer via a "choking algorithm". Likewise, to “unchoke” a seed, the server will send an unchoke message to tell it to stop blocking requests from peers that may be targeting the seed.​

### BitTorrent Vulnerabilities: Ambiguous Speeds​

All seeds are peers but not all peers are seeds. When a peer is a member of a swarm and downloads a file but does not act as a seed, this peer is known as a `"leech"`.​

High prevalence of `"leechers"` will impose a lot of stress on the number of requests given to a seed while at the same time not increasing file transfer performance. Controlling the amount of leechers could block out some potential users and/or add in extra overhead.​

The exact number of peers for any given swarm and any given file is heavily dependent both on the popularity of a file (more downloaded files will have more seeds, therefore higher download speeds for new peers) and on the number of seeds attached to a given swarm.​

Because of this, the exact speeds of any given swarm are speculative at best. For business class software, this kind of ambiguous speeds could result in the software failing to achieve popularity on the market. ​

### Ancillary Challenges: No search engine!​

One problem posed with torrent clients is the lack of a search engine built in. When a peer intends to torrent a file, the user of the peer must know exactly what they are looking for *and* where to look for it. Torrent search engines do exist as third parties but are not built into the box. ​

Utilization of these third parties *also* pose problems both due to the fact that at times torrents are used to transfer illegal content (e.g. copyrighted materials) and due to that fact, at times these torrent search engines will contain malicious software (malware).​

At times the validity of a particular torrent can be suspect as well. Torrent files themselves (especially if in a compressed format such as .zip) can at times contain malware. This makes at least some torrent search engines even harder to trust.​

### Sources Used & Useful Links

- BitTorrent Tracker: http://images.morehawes.co.uk/bittorrent/tracker.png​

- Rarest First Principle: http://conferences.sigcomm.org/imc/2006/papers/p20-legout.pdf​

- First BitTorrent Tracker Diagram : https://raw.githubusercontent.com/webtorrent/bittorrent-tracker/master/img.png

- Second BitTorrent Tracker Diagram : http://images.morehawes.co.uk/bittorrent/tracker.png

- vaibhav-walia@github : https://github.com/vaibhav-walia

- WebTorrent, LLC.@github : https://github.com/webtorrent/bittorrent-protocol

- WebTorrent, LLC.@github : https://github.com/webtorrent/create-torrent

- WebTorrent, LLC.@github : https://github.com/webtorrent/webtorrent-cli
​
- Node.js v8.4.0 Documentation : https://nodejs.org/api/fs.html

- npm : https://www.npmjs.com/

- Internet Archive : https://archive.org/

- Vuze : https://wiki.vuze.com/w/Legal_torrent_sites

- patorjk : http://patorjk.com/software/taag/#p=testall&f=Larry%203D&t=CS%206580%20Final%20Demo


​


