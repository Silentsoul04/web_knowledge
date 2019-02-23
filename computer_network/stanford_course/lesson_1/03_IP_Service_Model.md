## Network Layer
* It is Internet (Internet Protocol).
* Provide a service which includes the routing to the destination.


## IP
<img src="../assets/the_internet_protocol.png">


## IP Service Model
<img src="../assets/ip_service_model.png">

## Properties
1. datagram
2. unreliable
3. best effort
4. Connectionless (no order)


### Datagram
| data | IP SA | IP DA |
* IP SA: IP source addresss
* IP DA: IP destination address
* Router will forward datagram by its forwarding table
 * it dose not know the whole path, just use the IP DA to index the forwarding table to find the next router. (hop by hop)

 ### Unreliable
 * No promise that packets will be delivered
   * late
   * out of sequence
   * never delivered
   * packet may be duplicated

### Beset Effort
 1. Drop
   * IP do not drop datagram arbitrarily
   * Drop Scenario
    * packet queue in a router has congestion, which forcing the router to drop the next arriving packet.
   * Don't resend data and do not inform sender (end-host) that the datagram is dropped.
 2. Faulty Routing
   * send packet to wrong destination
   * duplicate packet by mistake

### Connectionless
 * No order for packets

## Why is the IP service so simple ?
1. Simple, dumb, minimal: Faster, more streamlined and lower cost to build and maintain.
 * A lot of routers scatter over the world, it should not be updated often.
 * Just for data delivery.

2. The end-to-end principle: Where possible, implement features in the end hosts.
 * Easy to evolve and improve.
 * In the case of the Internet, it was decided that features such as reliable
communications and controlling congestion should be done at the end points – by the
source and destination computers.

3. Allows a variety of reliable (or unreliable) services to be built on top.
 * Example: real time chat app (skype), if IP retransmit some dropped datagram, the datagram will be useless because it is not real time. The skype may just want to put blank pixel or use the pixels from previous frame.

4. Works over any link layer: IP makes very few assumptions about the link layer below.


## The IP Service Model (Details)
1. Tries to prevent packets looping forever.
 * how does it happen: Forwarding table or router are changing
 * how to prevent: datagram header has hop-count field which called TimeToLive (TTL) field. It start out a number like 128 and is decremented by every router it passes. If it reaches zero, IP catch it and delete it.

2. Will fragment packets if they are too long.
 * Ethernet can only carry packets that are shorter than 1,500 bytes long
 * Example: LinkA -> Router -> LinkB
  * LinkA: transmit data that shorter than 1,500 bytes
  * LinkB: transmit data that shorter than 1,000 bytes
  * The router will shorter data to fit into LinkB based on the IP header field.

3. Uses a header checksum to reduce chances of delivering datagram to wrong destination.

4. Allows for new versions of IP
 * Currently IPv4 with 32 bit addresses
 * And IPv6 with 128 bit addresses

5. Allows for new options to be added to header.
 * Benefit: fAdd new stuff in header
 * Drawback: creak the simple principle of IP.


## IPv4 Datagram
* Protocol ID: tell hardware what is inside the data field.
 * Indicate how data is encoded and help end host to send the data to correct code to decode it.
 * Example: Protocol ID === 6 => means dat contains a TCP Segment, so we should pass the datagram to the TCPParser.
  *  The Internet Assigned Numbers Authority (IANA) defines over 140 different values of Protocol ID,   
* Version: tell which version of IP
 * IPv4 or IPv6
* Total Packet Length
  * up to 64k Bytes
  * include header and data
* Time to Live (TTL)
 * prevent packets accidentally looping in the network forever.
 * Every router is required to decrement the TTL field. If it reaches zero, the router should drop the packet.
* Packet ID + Flags + Fragment Offset:
 * help routers to fragment IP packets into smaller
self-contained packets if need-be.

* The Type Of service
 *  gives a hint to routers about how important this packet is.

* The Header Length
 * Length of header

* checksum
  * is calculated over the whole header so just in case the header is corrupted, we are not likely to deliver a packet to the wrong destination by mistake.


<img width="60%" src="../assets/ip4_datagram.png">
