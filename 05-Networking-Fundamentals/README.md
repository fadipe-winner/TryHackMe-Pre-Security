# Module 5 — Networking Fundamentals

Networking is one of the foundations of cybersecurity. Before I can properly
understand suspicious network activity, I first need to understand how devices
normally communicate.

In this module, I learned about IP and MAC addresses, network topologies,
switches and routers, ARP, DHCP, the OSI and TCP/IP models, TCP and UDP,
common ports and protocols, firewalls, and VPNs.

My main goal was not just to memorize definitions, but to understand how these
concepts connect together and how they can help during a security investigation.

---

# 1. Understanding Networks

A **network** is a group of connected devices that can communicate and share
resources.

These devices can include:

- Computers
- Servers
- Phones
- Printers
- Routers
- Switches
- IoT devices

Networks can be small, such as devices connected inside a home, or much larger,
such as networks connecting offices in different locations.

## The Internet

The Internet can be thought of as a massive **network of networks**.

Instead of every device being connected directly to every other device, smaller
networks are interconnected through networking infrastructure such as routers
and Internet service providers.

For these devices to communicate successfully, they need addressing systems and
protocols that define how information should be exchanged.

---

# 2. Identifying Devices on a Network

Two important identifiers I learned about are:

- **IP addresses**
- **MAC addresses**

They are both used in networking, but they serve different purposes.

## IP Addresses

An **IP (Internet Protocol) address** is a logical address used to identify a
device/interface and allow data to be routed across IP networks.

An IPv4 address looks like:

```text
192.168.1.25
```

IPv4 addresses contain four decimal numbers called **octets**, separated by
periods.

Each octet ranges from:

```text
0 - 255
```

This is because each octet represents 8 bits, giving IPv4 a total size of
32 bits.

### Private vs Public IP Addresses

I also learned the difference between private and public IP addresses.

**Private IP addresses** are used inside local networks and are not directly
routed across the public Internet.

The main private IPv4 ranges are:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

**Public IP addresses** are globally routable addresses used for communication
across the Internet.

A useful distinction for security analysis is:

```text
192.168.1.20  → likely an internal/private address
8.8.8.8       → public address
```

Knowing whether an IP address is internal or external can provide useful context
when investigating network traffic.

### IPv6

IPv4 has a limited address space, so **IPv6** was developed to provide a much
larger number of addresses.

IPv6 uses 128-bit addresses rather than IPv4's 32-bit addresses.

An IPv6 address may look like:

```text
2001:db8::1
```

At this stage, my main takeaway is understanding **why IPv6 exists and being
able to recognize an IPv6 address when I see one**.

---

## MAC Addresses

A **MAC (Media Access Control) address** is an identifier associated with a
network interface and is mainly used for communication on the local network at
the Data Link layer.

A MAC address can look like:

```text
00:1A:2B:3C:4D:5E
```

A MAC address is 48 bits and is normally represented as six hexadecimal pairs.

### IP vs MAC

A simple way I currently think about them is:

| Address | Main Purpose |
|---|---|
| IP address | Logical addressing and routing between networks |
| MAC address | Local network/interface identification and frame delivery |

This distinction becomes more important when understanding technologies such
as ARP and Ethernet.

---

# 3. Testing Connectivity with Ping

`ping` is a simple but useful networking tool for testing whether another host
can be reached.

For example:

```bash
ping 192.168.1.1
```

Ping commonly uses **ICMP (Internet Control Message Protocol)** Echo Request
and Echo Reply messages.

It can help answer questions such as:

- Can I reach the destination?
- Is the destination responding?
- Approximately how long are responses taking?

However, a failed ping does **not automatically mean that a host is offline**.
ICMP traffic can be filtered or blocked by firewalls.

That was an important distinction for me: one tool alone does not always give
the complete picture.

---

# 4. LAN Topologies

A **network topology** describes how devices in a network are arranged or
connected.

## Star Topology

In a star topology, devices connect through a central networking device,
commonly a switch.

```text
        PC
         |
PC ---- Switch ---- Server
         |
      Printer
```

This is common in modern Ethernet LANs.

One advantage is that individual devices can generally be added or removed
without affecting every other connection.

However, the central device is important because problems with it can affect
many connected devices.

## Bus Topology

In a traditional bus topology, devices share a common backbone cable.

This design is much less common in modern Ethernet networks.

Learning about different topologies helped me understand how the physical or
logical design of a network can affect communication and reliability.

---

# 5. Switches and Routers

I initially found switches and routers easy to mix up, so this distinction was
important.

## Switch

A **switch** connects devices within a LAN.

Traditional Ethernet switches primarily operate at **OSI Layer 2** and use MAC
addresses to decide where Ethernet frames should be forwarded.

For example:

```text
PC ───┐
      │
PC ─── Switch ─── Server
      │
Printer┘
```

Some switches can also perform Layer 3 functions, but understanding Layer 2
switching is the important foundation.

## Router

A **router** connects different IP networks and forwards packets between them.

Routers primarily make forwarding decisions using IP addresses at **OSI
Layer 3 — the Network layer**.

For example:

```text
Home LAN
   |
 Router
   |
Internet
```

### The distinction I remember

```text
Switch → connects devices within a LAN
Router → connects different networks
```

---

# 6. Subnetting Basics

Subnetting is used to divide an IP network into smaller logical networks.

An IP address contains information relating to both:

- The **network**
- The **host**

A subnet mask or CIDR prefix helps determine which part represents the network.

For example:

```text
192.168.1.25/24
```

For a `/24` network, the first 24 bits identify the network portion.

The corresponding subnet mask is:

```text
255.255.255.0
```

At this stage, I am focusing on understanding the purpose of subnetting before
trying to become fast at subnet calculations.

### Why this matters for security

Subnet information can help me understand whether two devices belong to the
same network and how a network may be segmented.

Network segmentation is important in security because organizations can
separate systems and restrict communication between different parts of the
environment.

---

# 7. Default Gateway

A **default gateway** is the device a host normally sends traffic to when the
destination is outside its local network.

In many small networks, the router acts as the default gateway.

For example:

```text
PC
192.168.1.25
      |
      v
Default Gateway
192.168.1.1
      |
      v
Other Networks / Internet
```

This helped me understand how a computer knows where to send traffic that is
not intended for another device on its own local network.

---

# 8. ARP

**ARP (Address Resolution Protocol)** is used in IPv4 local networks to map an
IP address to a MAC address.

For example, a computer may know:

```text
Destination IP: 192.168.1.10
```

but need the destination MAC address to deliver an Ethernet frame on the local
network.

ARP helps resolve that relationship.

A simplified process is:

```text
ARP Request:
"Who has 192.168.1.10?"

ARP Reply:
"192.168.1.10 is at 00:1A:2B:3C:4D:5E"
```

The result can then be stored temporarily in the system's ARP cache.

### Security Relevance

ARP assumes a level of trust on the local network and can be abused through
techniques such as ARP spoofing/poisoning.

For now, the important thing for me is understanding **what ARP normally does**
before learning how attackers abuse it.

---

# 9. DHCP

**DHCP (Dynamic Host Configuration Protocol)** allows devices to automatically
receive network configuration instead of requiring everything to be configured
manually.

DHCP can provide information such as:

- IP address
- Subnet mask
- Default gateway
- DNS server

A common DHCP process can be remembered as **DORA**:

```text
Discover
Offer
Request
Acknowledge
```

### D — Discover

The client searches for an available DHCP server.

### O — Offer

The DHCP server offers network configuration to the client.

### R — Request

The client requests the offered configuration.

### A — Acknowledge

The server confirms the lease/configuration.

This explains how a laptop can join many networks and automatically receive the
information it needs to communicate.

---

# 10. The OSI Model

The **OSI (Open Systems Interconnection) model** divides network communication
into seven conceptual layers.

| Layer | Name | Basic Role |
|---:|---|---|
| 7 | Application | Network services used by applications |
| 6 | Presentation | Data formatting, encoding and encryption concepts |
| 5 | Session | Managing communication sessions |
| 4 | Transport | End-to-end transport using protocols such as TCP/UDP |
| 3 | Network | IP addressing and routing |
| 2 | Data Link | Frames and local MAC-based communication |
| 1 | Physical | Transmission of bits through physical media/signals |

A mnemonic I can use to remember the layers from Layer 7 to Layer 1 is:

> **All People Seem To Need Data Processing**

The OSI model does not mean that I will always see networking separated neatly
into seven pieces in real life. Instead, it gives me a framework for thinking
about **where different networking technologies operate and where problems may
occur**.

---

# 11. TCP and UDP

At the Transport layer, two protocols I need to understand are **TCP and UDP**.

## TCP

**TCP (Transmission Control Protocol)** is connection-oriented and designed to
provide reliable, ordered delivery of data.

Before normal communication begins, TCP commonly establishes a connection using
the **three-way handshake**:

```text
Client                  Server

  SYN  ------------------>
       <--------------- SYN-ACK
  ACK  ------------------>
```

I remember this as:

```text
SYN      → "Can we establish a connection?"
SYN-ACK  → "Yes, I received your request."
ACK      → "Acknowledged."
```

TCP uses mechanisms such as acknowledgements, sequence information and
retransmissions to provide reliable communication.

Protocols such as HTTP(S) and SSH commonly use TCP.

## UDP

**UDP (User Datagram Protocol)** is connectionless and has much less protocol
overhead than TCP.

UDP does not provide the same delivery and ordering guarantees as TCP.

This makes it useful for situations where low overhead or speed is more
important than built-in reliable delivery.

### TCP vs UDP

| TCP | UDP |
|---|---|
| Connection-oriented | Connectionless |
| Reliable delivery mechanisms | No built-in delivery guarantee |
| Ordered byte stream | Datagram-based |
| More overhead | Lower overhead |
| Uses acknowledgements/retransmission | Does not provide TCP-style acknowledgements |

Understanding TCP and UDP is important because security tools frequently show
which transport protocol was used in a network connection.

---

# 12. Packets and Frames

One concept I wanted to make clearer was the difference between a **packet**
and a **frame**.

In simplified OSI terminology:

```text
Layer 3 → Packet
Layer 2 → Frame
```

As data moves down the networking stack, each layer can add information needed
for communication. This process is called **encapsulation**.

A simplified view is:

```text
Application Data
      ↓
TCP/UDP information
      ↓
IP Packet
      ↓
Ethernet Frame
      ↓
Bits transmitted
```

At the receiving device, this process is reversed.

Understanding this gives me a better foundation for eventually analysing
packet captures in tools such as Wireshark.

---

# 13. TCP/IP Model

The TCP/IP model is another way of organizing network communication.

A common four-layer representation is:

| TCP/IP Layer | Examples |
|---|---|
| Application | HTTP, HTTPS, DNS, SSH |
| Transport | TCP, UDP |
| Internet | IP, ICMP |
| Network Access | Ethernet, Wi-Fi |

The OSI model is useful for learning and troubleshooting concepts, while the
TCP/IP model more closely reflects the protocol suite used by modern IP
networks.

---

# 14. DNS

**DNS (Domain Name System)** translates domain names into information needed to
locate network services, most commonly IP addresses.

For example, instead of users having to remember an IP address, they can use a
domain name.

Conceptually:

```text
example.com
     ↓
    DNS
     ↓
IP address
```

### Security Relevance

DNS activity can provide useful information during investigations because it can
show which domain names a system attempted to resolve.

Unexpected or suspicious domain lookups can provide useful context when
investigating an alert.

---

# 15. Ports and Common Protocols

IP addresses help identify hosts, while **port numbers** help identify network
services or application endpoints.

Some common ports I want to become comfortable recognizing are:

| Port | Protocol/Service | Purpose |
|---:|---|---|
| 21 | FTP | File transfer control |
| 22 | SSH | Secure remote administration |
| 53 | DNS | Name resolution |
| 80 | HTTP | Web traffic |
| 443 | HTTPS | Encrypted web traffic |
| 3389 | RDP | Windows Remote Desktop |

I do not want to memorize hundreds of ports at once. My goal is to become
comfortable with common ports naturally as I encounter them in labs and
investigations.

### Important Security Lesson

A port number alone does **not** prove what traffic is actually doing.

For example:

```text
Destination Port: 443
```

suggests HTTPS is commonly associated with the connection, but malicious
traffic can also use common ports.

The port is therefore one piece of evidence rather than a final conclusion.

---

# 16. Firewalls

A **firewall** controls network traffic according to configured security rules.

Depending on the firewall and its capabilities, decisions can be based on
information such as:

- Source IP
- Destination IP
- Source/destination port
- Protocol
- Connection state
- Application or other higher-level information

A simplified firewall rule could conceptually say:

```text
Allow TCP traffic to destination port 443
```

Firewalls are important for reducing unauthorized or unnecessary communication
between systems and networks.

### SOC Relevance

Firewall logs can provide valuable information during investigations.

For example:

```text
Source:       192.168.1.25
Destination:  203.0.113.50
Protocol:     TCP
Port:         443
Action:       ALLOW
```

From this information I can begin asking:

- Which device generated the traffic?
- Where was it going?
- Was the destination expected?
- Was the traffic allowed or blocked?
- Is this behaviour normal for this device?
- Is there other evidence related to the connection?

---

# 17. VPN Basics

A **VPN (Virtual Private Network)** can create an encrypted tunnel across an
untrusted network such as the Internet.

Organizations commonly use VPNs to provide secure remote connectivity between
users or networks.

A simplified example is:

```text
Remote User
     |
Encrypted VPN Tunnel
     |
Internet
     |
Company Network
```

VPNs are important in cybersecurity because remote-access activity can appear
in authentication and network logs and may need to be investigated when
unusual behaviour occurs.

---

# 18. Putting Everything Together

One of the most useful things I learned from this module was how these concepts
connect.

For example, when a computer accesses a website:

```text
User enters a domain name
        ↓
DNS helps resolve the name
        ↓
The destination IP becomes known
        ↓
The host determines whether the destination is local or remote
        ↓
If remote, traffic is normally sent toward the default gateway
        ↓
ARP may be used to resolve the local next-hop IPv4 address to a MAC address
        ↓
TCP may establish a connection
        ↓
HTTP/HTTPS application communication takes place
        ↓
Switches forward local Ethernet frames
        ↓
Routers forward IP packets between networks
```

The exact process can vary, but seeing the concepts together helped me move
beyond memorizing individual definitions.

---

# SOC Analyst Perspective

Networking fundamentals are especially important for the SOC/Blue Team path I
am working toward.

A security alert may contain information such as:

```text
Source IP:        192.168.1.42
Destination IP:   203.0.113.10
Destination Port: 443
Protocol:         TCP
Action:           ALLOWED
```

I should be able to interpret the basics before deciding whether something is
suspicious:

- `192.168.1.42` is in a private IPv4 range.
- The destination represents another IP address outside that private range.
- TCP was used.
- Port `443` is commonly associated with HTTPS.
- The connection was allowed.

But none of those facts alone prove whether the activity is legitimate or
malicious.

The next step would be adding context: identifying the device/user, examining
the destination, looking at DNS or proxy activity where available, checking
related alerts, and comparing the behaviour with what is expected.

That is one of my biggest lessons from networking so far:

> **Understand normal communication first, then investigate what looks unusual.**

---

# Key Takeaway

This module gave me a much clearer picture of how devices communicate across a
network. I now better understand the roles of IP and MAC addresses, switches,
routers, ARP, DHCP, DNS, TCP/UDP, ports, firewalls, VPNs, and the OSI/TCP-IP
models.

More importantly, I am beginning to connect these fundamentals to security
analysis. Instead of only seeing an IP address, port, or protocol as a
definition to memorize, I am learning to ask what that information tells me
about the communication taking place.

These are foundational skills that I plan to build on as I move toward packet
analysis, network monitoring, SIEM investigations, and SOC-focused labs.
