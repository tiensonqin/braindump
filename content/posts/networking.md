+++
title = "Computer Networking"
author = ["Jethro Kuan"]
lastmod = 2019-01-25T13:03:10+08:00
tags = ["networking"]
draft = false
math = true
+++

## Introduction {#introduction}


### What is the Internet? {#what-is-the-internet}

The internet is a computer network that interconnects hundreds of
millions of computing devices throughout the world.

End systems are connected together by a network of _communication links_
and _packet switches_. The common packet switches are routers and
link-layer switches. The sequence of communication links and packet
switches traversed by a packet from the sending end system to the
receiving end system is known as the route, or path through a network.

End systems access the internet through _Internet Service Providers
(ISPs)_. ISPs provide a variety of types of network access to the end
systems.

End systems, packet switches and other pieces of the Internet run
protocols that control the sending and receiving of information within
the internet. The Internet's principal protocols are the Transmission
Control Protocol (TCP) and the Internet Protocol (IP), known
collectively as TCP/IP.


### What is a protocol? {#what-is-a-protocol}

> A protocol defines the format and the order of messages exchanged
> between two or more communicating entities, as well as the actions
> taken on the transmission and/or receipt of a message or other event.


### The Network Edge {#the-network-edge}

The computers and other devices that are connected to the Internet are
often called end systems. This is because they sit at the edge of the
Internet. Each system are also referred to as hosts because they host
application programs such as the web browser, or a server. Hosts are
sometimes further divided into 2 categories: _clients_ and _servers_.

Access networks include the digital subscriber line (DSL), cable, and
fiber to the home (FTTH). Ethernet and WiFi access networks are now
common across enterprise, university campuses as well as in homes.
Wide-area wireless access such as 4G and LTE provide wireless access
to the Internet by sending and receiving packets through a base
station.


### Physical Mediums {#physical-mediums}

For reach transmitter-receiver pair, bits are interchanged. These bits
are sent by electromagnetic waves, or optical pulses across a physical
medium.

The least expensive and most commonly used transmission medium is the
twisted-pair copper wire. It consists of 2 insulated copper wires,
twisted togethter to reduce electrical interference from similar pairs
close by.

{{< figure src="/ox-hugo/UTP-Cable-Picture_2019-01-14_11-24-30.jpg" caption="Figure 1: A Unshielded-Twisted-Pair (UTP) cable" >}}

Coaxial cables consist of 2 copper conductors, but the two conductors
are concentric rather than parallel. These achieve high data
transmission rates, and can be used as a guided shared medium. They
are common in cable television systems.

{{< figure src="/ox-hugo/SW-33020-6_3_2019-01-14_11-25-43.jpg" caption="Figure 2: A Coaxial cable" >}}


### The Network Core {#the-network-core}


#### Packet Switching {#packet-switching}

In a network application, end systems exchange messages with each
other. Messages can contain anything the application designer wants.
To send a message from a source end system to a destination end
system, the source breaks long messages into smaller chunks of data
known as _packets_. Each packet travels through communication links and
packet switches. Packets are transmitted over each communication link
at a rate equal to the full transmission rate of the link. So if a
source end system or a packet switch is sending a packet of \\(L\\) bits
over a link with transmission rate \\(R\\) bits/sec, then the time to
transmit the packet is \\(\frac{L}{R}\\) seconds.

Most packet switches use _store-and-forward transmission_ at the inputs
to the links. This means that the packet switch must receive the
entire packet before it can begin to transmit the first bit of the
packet onto the outbound link.

Each packet switch has multiple links attached to it. For each
attached link, the packet switch has an _output buffer_, which stores
packets that the router is about to send into that link. If an
arriving packet needs to be transmitted onto a link but finds the link
busy with the transmission of another packet, the arriving packet must
wait in the output buffer. This results in output buffer _queuing
delays_. Packet loss will occur -- either the arriving packet or one of
the already-queued packets will be dropped.

How does a router determine which link it should forward the packet
onto? In the Internet, each end system is assigned an IP address. The
source end system includes the destination IP address in the packet's
header. Each router has a _forwarding table_ that maps destination
addresses to its outbound links.


#### Circuit Switching {#circuit-switching}

In circuit-switched networks, the resources needed along apath
(buffers, link transmission rate) to provide for communication between
end-systems are reserved for the duration of the communication session
between the end systems. Traditional telephone networks are examples
of such circuit-switched networks.

A circuit in a link is implemented with either _frequency-division
multiplexing (FDM)_ or _time-division multiplexing (TDM)_. With FDM, the
frequency spectrum of a link is divided up among the connections
established across the link. For a TDM link, time is divided into
frames of fixed duration, and each frame is divided into a fixed
number of time slots.

Packet switching is offers better sharing of transmission capacity
than circuit switching, and is simpler and more efficient. However,
circuit switching can be more suitable for real-time services.


### A Network of Networks {#a-network-of-networks}

A PoP is a group of one or more routers in the provider's network
where customer ISPs can connect into a provider ISP. For a customer
network to connect to a provider's PoP, it can lease a high-speed link
from a third-party telecommunications provider to directly connect one
of its routers to a router at the PoP. Any ISP may choose to
multi-home, that is, to connect to two or more provider ISPs.

{{< figure src="/ox-hugo/screenshot_2019-01-14_12-14-13.png" caption="Figure 3: Interconnection of ISPs" >}}


### Delays in Packet-Switched Networks {#delays-in-packet-switched-networks}

1.  Processing delay
    1.  Time needed to check bit-level errors in packet
2.  Queuing delay
    1.  Time spent waiting to be transmitted in the link
3.  Transmission delay
    1.  Equal to \\(L/R\\). Transmission delays are typically on the order
        of microseconds to milliseconds in practice.
4.  Propagation delay
    1.  The bit propagates at the propagation speed of the link,
        depending on the physical medium. This speed is roughly the
        speed of light.

Packet loss can occur when it arrives to find a full queue. The router
will drop the packet.

Given these delays, we can compute the end-to-end delay.

\begin{equation}
  d\_{\text{e2e}} = N(d\_{\text{proc}} + d\_{\text{trans}} + d\_{\text{prop}})
\end{equation}

This does not account for the average queuing delay of the node.


### Throughput {#throughput}

The instantaneous throughput at any instant of time is the rate (in
bits/sec) at which a host is receiving the file.


### Protocol Layers and Their Service Models {#protocol-layers-and-their-service-models}

The Internet Protocol stack consists of 5 layers: the physical link,
network, transport, and application layers. The OSI reference model
consists of 7 layers.

{{< figure src="/ox-hugo/screenshot_2019-01-14_12-23-06.png" caption="Figure 4: IP stack and ISO OSI reference model" >}}

Application layer
: network applications and application layer
    protocols reside here. These protocol include HTTP, SMUT and FTP.
    The packet of information at this layer is a **message**.

Transport Layer
: in the Internet there are 2 transport protocols:
    TCP and UDP, each with their own use-case. Each transport-layer
    packet is called a segment.

Network Layer
: responsible for moving packets known as **datagrams**
    from one host to another. It has many routing protocols.

Link Layer
: The network layer relies on this layer to deliver the
    datagram to the next node along the route. These
    services depend on the specific link-layer protocol
    employed for the link. For example, cable access
    networks may use the DOCSIS protocol. Link layer
    protocols include Ethernet and WiFi. Link-layer
    packets are referred to as **frames**.

Physical Layer
: responsible of moving individual bits across
    physical mediums.


## Application Layer {#application-layer}

Networking applications have application-layer protocols that define
the format and order of the messages exchanged between processes, as
well as define the actions taken on the transmission or receipt of a
message.

Example of application-layer protocols include:

1.  HTTP (HyperText Transfer Protocol [RFC 2616]), which defines how
    messages are passed between browser and web-server
2.  SMTP (Simple mail Transfer Protocol [RFC 821]), a protocol for mail
    exchange


### Client and Servers {#client-and-servers}

A network application protocol typically has 2 parts, a client side
and a server side. The host that initiates the session is often
labeled the client. A host can act as both a client and server at the
same time. As a concrete example, a mail server host runs the client
side of SMTP (for sending email), and the server side of SMTP (for
receiving email).


### Sockets {#sockets}

Applications communicate by sending messages over a socket. A
process's socket can be thought of as the process's door: it sends
messages into, and receives messages from the network through this
socket. It is the interface between the application layer and
transport layer within a host.

{{< figure src="/ox-hugo/screenshot_2019-01-25_10-53-43.png" caption="Figure 5: Application processes, sockets, and underlying transport protocol" >}}


### Addressing Processes {#addressing-processes}

In order for a process on one host to send a message to a process on
another host, the sending process must identify the receiving process.
To identify the receiving process, one must specify these 2 pieces of
information:

1.  The name or address of the host machine
2.  An identifier that specifies the identity of the receiving process
    on the destination host

In Internet applications, the destination host is specified by its IP
address. The **IP address** is a 32-bit quantity that uniquely identifies
the interface that connects to the internet. These need to be globally
unique. A receive-side **port number** serves the purpose of identifying
the correct process on the system.

The user agent is an interface between the user and the network
application. For example, user agents for browsing the Web include
Firefox and Chrome.


### Transmission Control Protocol (TCP) {#transmission-control-protocol--tcp}

The Internet makes available 2 transport protocols to applications,
namely UDP and TCP. When a developer creates a new application for the
Internet, they must choose between the two protocols. Each protocol
offers a different service model.

TCP includes a connection-oriented service and a reliable data
transfer service.

TCP has the client and server exchange transport-layer control
information with each other before the application-level messages
begin to flow. This hand-shaking procedure alerts the client and
server, and a TCP connection is said to exist between the sockets of
the 2 processes. When the application is done with sending messages,
it must tear down the connection.

The communicating processes can rely on TCP to deliver all data sent
without error, and in proper order. TCP also includes a
congestion-control mechanism. The mechanism throttles a process when
the network is congested, attempting to limit each TCP connection to
its fair share of network bandwidth. This control mechanism benefits
the Internet, rather than the direct benefit of the communicating
processes.

TCP does not provide:

1.  A guaranteed minimum transmission rate
2.  Any delay guarantees


### User Datagram Protocol (UDP) {#user-datagram-protocol--udp}

UDP is connectionless, so there is no handshaking before the 2
processes start to communicate. It provides an unreliable data
transfer service. Hence, it provides no guarantee that a message will
ever reach the receiving socket. Messages that do arrive may arrive
out-of-order.

On the other hand, UDP does not include a congestion-control
mechanism, so a sending process can pump data into a UDP socket at any
rate.

This protocol is largely used by real-time applications.


### HTTP {#http}

HTTP is implemented in 2 programs: a client program and a server
program. Clients and servers talk to each other by exchanging HTTP
messages. HTTP defines the structure of these messages.

HTTP use TCP as their underlying transport protocol. The HTTP client
first initiates a TCP connection with the server. Once the connection
is established, the browser and server processes access TCP through
their socket interfaces. The client sends HTTP request messages
through the socket interface, and receives HTTP response messages from
its socket interface.

HTTP can use both nonpersistent and persistent connections. The use of
persistent connections is the default mode for HTTP/1.1.

With non-persistent connections, each TCP connection is closed after
the server sends the object. T he response time for a new HTTP request
is 2 round-trip times plus the transmission time at the server of the
HTML file.

With persistent connections, the server leaves the TCP connection open
after sending a response. Subsequent requests and responses between
the same client and server can be sent over the same connection.

Here's an exmple of the HTTP Request message:

```text
GET /somedir/page.html HTTP/1.1
Host: www.someschool.edu
Connection: close
User-agent: Mozilla/4.0
Accept-language: fr
(extra carriage return, line feed)
```

The general form of a request message looks like this:

{{< figure src="/ox-hugo/screenshot_2019-01-25_11-21-44.png" caption="Figure 6: Format of a HTTP request message" >}}

The response message looks like this:

```text
HTTP/1.1 200 OK
Connection: close
Date: Thu, 06 Aug 1998 12:00:15 GMT
Server: Apache/1.3.0 (Unix)
Last-Modified: Mon, 22 Jun 1998 09:23:24 GMT
Content-Length: 6821
Content-Type: text/html

(data data ...)
```

{{< figure src="/ox-hugo/screenshot_2019-01-25_11-26-41.png" caption="Figure 7: Format of a HTTP response message" >}}


### User-server Interaction: Cookies {#user-server-interaction-cookies}

The HTTP server is stateless. This simplifies server design, and
permits engineers to develop high-performance web servers that can
handle thousands of simultaneous TCP connections. For a website to
identify users, HTTP uses cookies. Cookies, defined in [RFC 6265],
allows sites to keep track of users.

Cookie consists of 4 components:

1.  A cookie header line in the HTTP response message
2.  A cookie header line in the HTTP request message
3.  A cookie file kept on the user's end system, and is managed by the
    user's web browser
4.  A back-end database at the Web site

{{< figure src="/ox-hugo/screenshot_2019-01-25_11-29-28.png" caption="Figure 8: Keeping user state with cookies" >}}


### Web Caching {#web-caching}

A web cache -- also called a proxy server -- may satisfy HTTP requests
on behalf of an origin Web server.

<networking.bib>