---
title: "Introducing Admarus - A Peer-to-Peer Search Engine for IPFS"
date: 2023-07-21T13:18:40+02:00
draft: false
---

I've been working on a new search engine system that's fully peer-to-peer, with no trusted third party.
Today, I'm excited to unveil [Admarus](https://admarus.net/), a decentralized search engine for the decentralized web (specifically, IPFS).

<p align="center">
    <a href="https://www.youtube.com/watch?v=AKGpNKwBrOY"><img src="https://admarus.net/demo.gif#2" alt="Demo GIF of searching on Admarus."/></a>
</p>

🔥 [**Try the gateway-based demo!**](https://admarus.net/) 🔥

## 💡 Motivation

IPFS is a network for storing and sharing data.
Hopes are that it could be the foundation of a new, distributed web.
This new web would aim to guarantee freedom of speech, privacy, and access to information, while eliminating censorship and gatekeeping.

However, at present, IPFS primarily functions as a storage solution rather than a fully realized web platform.
Unlike the conventional web, browsing an IPFS-based web is not yet a seamless experience, as finding content can be challenging, if not impossible.

One of the reasons the current web was successful was its ease of finding content.
If we are going to build a new web on IPFS, we need to make IPFS searchable.
And we can't just use a centralized system, because that would be missing the whole point.
The search engine must be decentralized and open, aligning with the core principles of the IPFS network.
For IPFS to be widely adopted and relevant as a web platform, implementing a decentralized and open search engine is essential.

I would like to give credit to [this tweet](https://twitter.com/paoloardoino/status/1534811103670173696) for inspiring me to start working on Admarus.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">A pure peer to peer knowledge indexer and search engine is the real end game.<br>Not blockchain based, it will never scale.<br>Just peer storage, peer indexing, peer stuff.<br>No token will be needed to access knowledge 🤫</p>&mdash; Paolo Ardoino 🍐 (@paoloardoino) <a href="https://twitter.com/paoloardoino/status/1534811103670173696?ref_src=twsrc%5Etfw">June 9, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

There have already been many attempts at building new search engines.
Sadly, all of them are disappointingly centralized and/or not viable.
There is no point in building a new web if it's also going to be ruled by big companies.
As Paolo said, it must be peer-to-peer like IPFS, not reliant on fat blockchains and unsustainable tokens.
This is the idea behind Admarus, and that's what makes it different.

## ✨ Features

- **No storage use**: Admarus indexes data that's already in your Kubo node
- **Search operators**: AND, OR, and NOT
- **Trustless**: Results are verified, not trusted
- **Language detection**: Language is detected from text
- **Scalable**: Gets faster as more peers join
- **Censorship-resistant**: Censors would need full control of more than 95% of the network
- **Open**: Nodes don't discriminate on obscure criteria (hi emails)
- **Decentralized**: No central authority. Multiple peer discovery mechanisms are available
- **Blockchain-free**: No blockchain, no token, just peer-to-peer magic
- **Developer-friendly**: Practical API for building apps and bots

Admarus is open-source, [check it out on Github](https://github.com/mubelotix/admarus)!

<script defer src="https://tarptaeya.github.io/repo-card/repo-card.js"></script>
<div class="repo-card" data-repo="mubelotix/admarus"></div>

## 📐 Design

If you are familiar with the IPFS's design, you will immediately be with Admarus'.

[Kubo](https://github.com/ipfs/kubo) runs a daemon on port `4001` and provides an HTTP API on port `5001`.  
Admarus runs a daemon on port `4002` and provides an HTTP API on port `5002`.

Like IPFS, Admarus has a web user interface and a public gateway for convenience.

Admarus is intended to run on machines that are running Kubo.
When you run the daemon, it automatically connects to Kubo.
It will then start indexing all the documents you have pinned. (Only HTML documents are currently supported.)
These documents will now be searchable in the entire network.

This is game-changing for discoverability on IPFS.
Considering this drives traffic to websites you pin, it gives an incentive to everyone to publish their websites to IPFS.

## 🤝 How to Contribute

<a href="https://census.admarus.net/"><img alt="Documents in corpus badge" src="https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fcensus.admarus.net%2Fapi%2Fv0%2Fstats&query=%24.stats_1h.documents&suffix=%20documents&label=corpus&color=purple"></a>
<a href="https://census.admarus.net/"><img alt="Peers in network badge" src="https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fcensus.admarus.net%2Fapi%2Fv0%2Fstats&query=%24.stats_1h.peers&suffix=%20peers&label=network&color=purple"></a>

At its current stage, the Admarus network is relatively small, indexing only a subset of Wikipedia and a few other websites.
You can make a significant impact by running a node and helping the network grow!

Guides and documentation are available [on the project's wiki](https://github.com/Mubelotix/admarus/wiki).

If you have a static website, consider [adding it to ipfs](https://docs.ipfs.tech/how-to/websites-on-ipfs/multipage-website) and [running Admarus](https://github.com/Mubelotix/admarus/wiki/Installation).
Developers can also contribute by building bridges to prominent websites (news, forums, wikis, torrent websites, etc.), thereby contributing to archiving and decentralizing the web.

You can also directly support the project by [giving it a star on Github](https://github.com/Mubelotix/admarus/) or [donating a few sats](bitcoin:bc1q884745lxdpra7kwqtg5et6f74t3faemccz4v6s).

## 🚀 The Road Ahead

With the Minimum Viable Product (MVP) now available, our next focus is on [the alpha release](https://github.com/Mubelotix/admarus/milestone/2), which is planned for the end of the summer.
Some of the upcoming features include support for image and video documents, UI and UX improvements, performance optimizations, and ranking tweaks.

[Join us](https://github.com/Mubelotix/admarus/) on this exciting journey as we work towards a truly decentralized, open, and censorship-resistant search engine for IPFS!

🔥 [**Try the gateway-based demo!**](https://admarus.net/) 🔥

<!-- ## 🛠️ Bonus: Technical Overview

Let's think this through the easy way.
I will start by describing the naive approach everyone would think of, and then I will explain why it doesn't work and present a solution to its problems.

Imagine the IPFS network: a lot of peers all connected to each other, each hosting some documents.
If you want to query the network, you can just iteratively query each peer for results.
That way, you get a list of results that you can rank and display to the user.

This approach is not viable because it doesn't scale.
If you have a lot of peers, you will have to query each of them, and that's going to take a lot of time.

One important think to note is that if you query everyone for results, many of them will return nothing.
That's because they don't have any document matching your query.
This is a waste of time that can be avoided.
If we could only query peers that are likely to have results, we would be able to get results at constant speed, regardless of how common the query terms are.
This is what the Kamilata protocol does, using a routing algorithm based on Bloom filters to test if a peer or its connections are likely to have results.

To learn more about the Kamilata protocol and how it uses Bloom filters to route queries to the right peers, see [the Kamilata repository](https://github.com/mubelotix/kamilata).
-->
