---
title: "Introducing Admarus - A Peer-to-Peer Search Engine for IPFS"
date: 2023-07-21T13:18:40+02:00
draft: true
---

I've been working on a new search engine system that's fully peer-to-peer, with no trusted third party.

I'm excited to announce [Admarus](https://admarus.net/), a decentralized search engine for IPFS built on this system.
<p align="center">
    <a href="https://www.youtube.com/watch?v=AKGpNKwBrOY"><img src="https://admarus.net/demo.gif#2" alt="Demo GIF of searching on Admarus."/></a>
</p>

## Motivation

As a long time IPFS user, I've always been frustrated because I didn't use it as much as I would have liked.
The thing is that it's hard to know what's on IPFS, so people end up not using it at all.
It's when I saw this tweet that I realized what was missing:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">A pure peer to peer knowledge indexer and search engine is the real end game.<br>Not blockchain based, it will never scale.<br>Just peer storage, peer indexing, peer stuff.<br>No token will be needed to access knowledge 🤫</p>&mdash; Paolo Ardoino 🍐 (@paoloardoino) <a href="https://twitter.com/paoloardoino/status/1534811103670173696?ref_src=twsrc%5Etfw">June 9, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

If we are going to build a new web, we need a way to find content on it.  
IPFS needs a search engine.

There have been previous attempts at building one, but it's very disappointing to see that they were all centralized and/or not viable.
There is no point building a new web if it's going to be ruled by the same centralized entities.  
IPFS needs a *decentralized, open, and censorship-resistant* search engine.

As Paolo said, it must be peer-to-peer like IPFS, not reliant on fat blockchains and unsustainable tokens.
A lot of search engine projects for web3 nowadays are not truly decentralized, not truly open, not truly free and far from censorship-resistant.

Now that I knew what the right direction was, I started working on a new system that would allow us to build a search engine that's truly decentralized, open, and censorship-resistant.

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
