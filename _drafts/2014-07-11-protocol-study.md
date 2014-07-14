---
layout: post
title: TCP/IP学习（一）
tags: 技术
---
## TCP/IP学习（一） ##

The internet protocol provides for transmitting blocks of data called **datagrams** from sources to destinations, where sources and destinations are hosts identified by fixed length addresses.

The internet protocol uses four key mechanisms in providing its service:
网间协议通过四种机制来提供服务
- Type of Service
- Time to Live
- Options
- Header Checksum

The type of service is an **abstract or generalized set of parameters** which characterize the service choices provided in the networks that make up the internet.

If the time to live reaches zero before the internet datagram reaches its destination, the internet datagram is destroyed.

Addresses are fixed length of four octets (32 bits). An address begins with a network number, followed by local address (called the "rest" field).

The data of the long datagram is divided into two portions on a **8 octet (64 bit) boundary**
(the second portion might not be an integral multiple of 8 octets, but the first must be).

Call the number of 8 octet blocks in the first portion NFB (for Number of Fragment Blocks).

Internet Header Length is the length of the internet header in 32 bit words, and thus points to the beginning of the data.  Note that the minimum value for a correct header is 5.