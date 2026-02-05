---
tags:
  - cloud
---

The first computer networks were generally used within an organization to facilitate the exchange of information between people and computers

A second benefit was the ability to share physical resources (useful for sharing printers for example)

These first networks of close-by computers are called **Local Area Networks**, or most commonly known as *LAN*. They can be as small as two computers connected or as big as having a whole university connected

## Ethernet

The most famous LAN network was *Ethernet*, used also nowadays.
It works by having a series of computers connected to a single, common **Ethernet cable**

When a computer wants to send information, the computer sends an electrical signal through the common cable. To know which computer was the information sent for, each computer has a unique **MAC Address** (Media Access Control Address). So computers only process data when they see their MAC Address in the header

> The general term for this approach is **CSMA** (Carrier Sense Multiple Access), in which the 'Carrier' is any shared transmission medium that carries data (copper wire for Ethernet and radio waves for Wifi)

The rate at which the carrier transmits its data its called **Bandwidth**

### Problem: Collision
When we have multiple computers trying to send information, the connection can't support sending multiple data at the same time. (Collision)
One solution for this problem is to make computers check whether there is a signal in the wire and wait in silence until the signal is done to send theirs.
The problem with this solution is how to determine which computers sends their information next. So to fix this, each computer waits some random period of time before re-transmitting its information. However, at a large scale collision may still happen.
The solution is to instead make the computer wait double the time. For example, if in the first try the computer waited 1 second, then in the next try it will wait 2 seconds. This is called **Exponential Back-off** and it is used worldwide by both Ethernet and WiFi connections.

Even with this, it is not worth to have an entire network of computers connected on one shared Ethernet cable.

So the final solution is to reduce the number of devices in any given shared carrier, or called the **Collision Domain**. For example, if we have 6 computers in one collision domain, we can reduce the likelihood of collisions by breaking it down into **two** collision domains by using a *network switch*
The network switch is only turned on when data must go from a computer in one collision domain to another computer in a different one. This is done by keeping a list of which MAC Address belongs to which collision domain.

In a bigger scale, this is how the Internet works, which includes a LOT of these switches as there are a lot of collision domains.

## Routing
The simplest way to connect two distant computers, or networks, is by allocating a communication line for their exclusive use. 
One example of this is **Circuit Switching**, in which you switch whole circuits to **route** traffic to the correct destination. However, this is very inflexible and expensive

Another approach is **Message Switching**. Instead of a dedicated route from A to B, data is passed through several stops. The number of stops the data takes is called *hop count*, which is useful for identifying routing problems

A downside to this method is that data is sometimes big, so they clog up the network because the whole data has to be transmitted from one stop to another. The solution to this is to chop up the data into many small pieces called **Packets**. Each packet contains a destination address defined by the *internet protocol* (IP). Every computer connected to a network gets one.

The name for this routing approach is called **Packet switching**

