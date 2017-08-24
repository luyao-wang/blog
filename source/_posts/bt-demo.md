---
title: CS6580 Final Presentation - Miniature BitTorrent Client 💻
date: 2017-08-23 15:05:54
categories:
- Node.js
- npm
- torrenting
- school🎓
- tmp
tags:
- tmp
---

```

      ___           ___           ___           ___
     /\  \         /\  \         /\__\         /\  \
    /::\  \       /::\  \       /::|  |       /::\  \
   /:/\:\  \     /:/\:\  \     /:|:|  |      /:/\:\  \
  /:/  \:\__\   /::\~\:\  \   /:/|:|__|__   /:/  \:\  \
 /:/__/ \:|__| /:/\:\ \:\__\ /:/ |::::\__\ /:/__/ \:\__\
 \:\  \ /:/  / \:\~\:\ \/__/ \/__/~~/:/  / \:\  \ /:/  /
  \:\  /:/  /   \:\ \:\__\         /:/  /   \:\  /:/  /
   \:\/:/  /     \:\ \/__/        /:/  /     \:\/:/  /
    \::/__/       \:\__\         /:/  /       \::/  /
     ~~            \/__/         \/__/         \/__/


```

### Prerequisites

node `v8.4.0`

npm `5.3.0`

### Dependencies

```
"dependencies": {
    ["bencode"](https://www.npmjs.com/package/bencode.js): "^0.10.0",
    ["parse-torrent"](https://www.npmjs.com/package/parse-torrent): "^5.8.1",
    "reinstall": "^2.0.0",
    "request": "^2.79.0"
}
```

### Demo

```
Luyaos-MacBook-Pro:Downloads luyaowang$ cd bt-demo
Luyaos-MacBook-Pro:Downloads luyaowang$ npm ls
Luyaos-MacBook-Pro:Downloads luyaowang$ cd srcc
Luyaos-MacBook-Pro:Downloads luyaowang$ node torrent.js ./../testTorrents/1.torrent
Luyaos-MacBook-Pro:Downloads luyaowang$ node torrent.js ./../testTorrents/2.torrent
Luyaos-MacBook-Pro:Downloads luyaowang$ node torrent.js ./../testTorrents/s.torrent
```

### Sample Run

```
Luyaos-MacBook-Pro:bt-demo luyaowang$ node torrent.js ./../testTorrents/1.torrent
134.154.70.45:6687 Messages: Error: connect ECONNREFUSED 134.154.70.45:6687,Closed


172.78.20.37:50563 Messages: Connected,handshake sent ,handshake complete ,Sent interested ,Bitfield
received ,Have(4),Have(11),Have(2),Have(6),Have(12),Have(9),Have(8),Have(5),Have(7),Have(10),Have(1)
,Have(0),Have(3),Un-Choke received ,Sent request for 4 ,Received all blocks for piece 4,valid
piece,Sent request for 11 ,Received all blocks for piece 11,valid piece,Sent request for 2 ,Received
all blocks for piece 2,valid piece,Sent request for 6 ,Received all blocks for piece 6,valid piece,Sent
request for 12 ,Received all blocks for piece 12,valid piece,Sent request for 9 ,Received all blocks
for piece 9,valid piece,Sent request for 8 ,Received all blocks for piece 8,valid piece,Sent request
for 5 ,Received all blocks for piece 5,valid piece,Sent request for 7 ,Received all blocks for piece
7,valid piece,Sent request for 10 ,Received all blocks for piece 10,valid piece,Sent request for 1
,Received all blocks for piece 1,valid piece,Sent request for 0 ,Received all blocks for piece 0,valid
piece,Sent request for 3 ,Received all blocks for piece 3,valid piece,No more pieces to request


100% done
Done:13
Remianing:0
Download Complete!
File will be saved at : ./../Downloads/
```

### Useful Links

- [Node.js v8.4.0 Documentation](https://nodejs.org/api/fs.html)

- [npm](https://www.npmjs.com/)

- [Internet Archive](https://archive.org/)

- [Vuze](https://wiki.vuze.com/w/Legal_torrent_sites)

- [patorjk](http://patorjk.com/software/taag/#p=testall&f=Larry%203D&t=CS%206580%20Final%20Demo)

### Acknowledgements

Credits to [vaibhav-walia@github](https://github.com/vaibhav-walia), [WebTorrent, LLC.: create-torrent](https://github.com/webtorrent/create-torrent), [WebTorrent, LLC.: webtorrent-cli](https://github.com/webtorrent/webtorrent-cli), [WebTorrent, LLC.: bittorrent-protocol](https://github.com/webtorrent/bittorrent-protocol)
