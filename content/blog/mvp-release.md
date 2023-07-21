---
title: "Introducing Admarus - A Peer-to-Peer Search Engine for IPFS"
date: 2023-07-21T13:18:40+02:00
draft: true
---

I've been working on a new search engine system that's fully peer-to-peer, with no trusted third party.

I'm excited to announce [Admarus](https://admarus.net/), a decentralized search engine for IPFS.

<p align="center">
    <a href="https://www.youtube.com/watch?v=AKGpNKwBrOY"><img src="https://admarus.net/demo.gif#2" alt="Demo GIF of searching on Admarus."/></a>
</p>

🔥 [**Try the gateway-based demo!**](https://admarus.net/) 🔥

## 💡 Motivation

As a long time IPFS user, I've always wanted to use IPFS whenever I could.
The thing is, no matter how much I wanted to, I ended up not using it at all.
And the reason is simple: I just couldn't find anything on it.

IPFS needed a search engine.

It is only when I stumbled upon [this tweet](https://twitter.com/paoloardoino/status/1534811103670173696) that I realized how important this issue is.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">A pure peer to peer knowledge indexer and search engine is the real end game.<br>Not blockchain based, it will never scale.<br>Just peer storage, peer indexing, peer stuff.<br>No token will be needed to access knowledge 🤫</p>&mdash; Paolo Ardoino 🍐 (@paoloardoino) <a href="https://twitter.com/paoloardoino/status/1534811103670173696?ref_src=twsrc%5Etfw">June 9, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

If we are going to build a *new* web, we need a *new* way to find content on it.

IPFS needs a *decentralized, open, and censorship-resistant* search engine.
If we fail to build one, the whole ecosystem will fail.

There have been many attempts at building new search engines.
Sadly, all of them are disappointingly centralized and/or not viable.
There is no point building a new web if it's going to be ruled by the same centralized entities.
As Paolo said, it must be peer-to-peer like IPFS, not reliant on fat blockchains and unsustainable tokens.
This is the idea behind Admarus.

## ✨ Features

- **No storage use**: Admarus indexes data that's already in your Kubo node
- **Search operators**: AND, OR, and NOT
- **Trustless**: Results are verified, not trusted
- **Language detection**: Language is detected from text
- **Scalable**: Gets faster as more peers join
- **Censorship-resistant**: Censors would need full control of more than 95% of the network
- **Open**: Nodes don't discriminate on obscure criteria (hi emails)
- **Decentralized**: No central authority. Multiple peer discovery mechanisms available
- **Blockchain-free**: No blockchain, no token, just peer-to-peer magic
- **Developer-friendly**: Practical API for building apps and bots

Admarus is obviously open source, [check it out on Github](https://github.com/mubelotix/admarus)!

<script defer src="https://tarptaeya.github.io/repo-card/repo-card.js"></script>
<div class="repo-card" data-repo="mubelotix/admarus"></div>

## 📐 Design

If you are familiar with the IPFS's design, you will immediately be with Admarus's.

Kubo runs a daemon on port `4001` and provides an HTTP API on port `5001`.  
Admarus runs a daemon on port `4002` and provides an HTTP API on port `5002`.

Kubo offers a webui.  
Admarus offers a webui.

Admarus is intented to run on machines that are running Kubo.
When you run run the daemon, it automatically connects to Kubo.
It will then start indexing all the documents you have pinned. (Only html documents are supported yet.)
These documents will now be searchable in the entire network.

This is game-changing for discoverability on IPFS.
Considering this drives traffic to websites you pin, it gives an incentive to everyone to publish their websites to IPFS.

## Run a node

 all pinned documents in your Kubo IPFS node.
These documents will now be searchable by other peers running Admarus.

## Ambition

## Design


## Technical Overview

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

## Making IPFS relevant

Admarus incentivizes people to publish their websites on IPFS, because it will drive traffic to them.
