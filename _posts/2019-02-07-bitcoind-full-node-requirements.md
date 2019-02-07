---
layout: post
title: Bitcoind (Full Node) Requirements
comments: true
tags:
 - bitcoin
 - bitcoind
 - lightning
 - benchmark
 - meetup
---
Some of those that showed up to last night's [Phoenix Bitcoin Meetup](https://www.meetup.com/Arizona-Bitcoin-Meetup/events/257998536/) showed interest in running a full node / lightning node, possibly on a Raspberry Pi or Odroid single-board computer. There were questions about system requirements. I believe a baseline requirement for a lightning node is running a full node, so I thought I'd give my observations running a full node at almost pure default settings (no custom .conf file) run with this command: `bitcoind -conf=$(pwd)/bitcoin.conf -datadir=$(pwd) -txindex -logips -server -rpcpassword=$BTC_RPC_PASSWORD -rpcuser=$BTC_RPC_USER -daemon -disablewallet`

My `bitcoind` (server) process is taking up 1.4GB of memory as it runs. It idles between 1-5% CPU (running an i7-4770 w/ 4 virtual cores). The bandwidth idles (ie not aggressively syncing the entire chain from scratch) at a constant 10KB/s. Keep in mind that means each week you're sucking 60*60*24*7=604800 =~ 605MB, or about 2.5GB a month.

The "blocks" directory containing the blockchain and its indices take up about 200GB. The chainstate directory containing the utxo set is about 3GB. The (optional) txindex takes up about 20GB. That's a total of about 220GB.

There are several guides to run this on a Raspberry Pi or other singleboard computers in order to get the CPU / Mem / Bandwidth. Almost all recommend bootstrapping the node with a full-size computer first, then moving the files over to the single-board.

For anyone interested, I am willing to bring an external drive to a future meetup containing my bitcoind directory. This way, you can bootstrap your own node without having to download & seed the entire 200GB blockchain on your own. It took me over a week, so this should save you a lot of time. Just let me know.

I will probably also run a Bitcoin Cash and Bitcoin SV node since they share the majority of their blocks with Bitcoin Core, so they are already bootstrapped well for me and I can deduplicate the files. I plan to finish writing a distributed blockchain explorer in the near future using IPFS, hopefully for all three coins.
