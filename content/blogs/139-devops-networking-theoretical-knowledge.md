---
title: "DevOps - Step By Step Learning : Part 15 (Learn Fundamental Networking Theoretical Knowledge)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-28T00:00:00Z"
tags: ["devops" , "networking"]
draft: false
showtoc: false
tocOpen: false
hidemeta: false
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
cover:
    image: "img/blogs/139-devops-networking-theory.jfif"
    caption: "DevOps Networking Theoretical Knowledge"
    alt: "DevOps Networking Theoretical Knowledge"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 14:** [DevOps - Step By Step Learning : Part 14 (Why Need Networking, What Theoretical and Practical Knowledge Should Know)]({{< ref "blogs/138-devops-networking-knowledge.md" >}})
---

{{< figure
    src="/img/blogs/139-devops-networking-theory.jfif"
    caption="DevOps Networking Theoretical Knowledge (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel found out why networking is **essential** in DevOps and overall software engineering. He breaks down the concepts into two categories: one is **theoretical**, and the other is **practical**. So he decided to start learning with the theoretical concepts. Because a strong understanding and clarity about these concepts is a must and important before starting any further. And Rasel started as planned...

* * *

## Fundamental Networking Theoretical Concepts

### Networking Basics

*   **Types of network**: LAN (Local Area Network), WAN (Wide Area Network), MAN (Metropolitan Area Network), PAN (Personal Area Network), SAN (Storage Area Network), WLAN (Wireless Local Area Network), VPN (Virtual Private Network).
*   **Network topology**: Star topology, Ring topology, Bus topology, Mesh topology, Tree topology, Hybrid topology.
*   **Networking devices**: NIC, Modem, Repeater, Hub, Switch, Router, Bridge, Gateway.
*   **Types of data communication**: Analog, Digital, Simplex, Half duplex, Full duplex.
*   **Transmission media**: Coaxial cable, Twisted Pair cable, Fiber optic, Radio wave/Wireless.
*   **Communication model**: Simplified communication model with source, transmitter, medium, receiver, destination.

I had written a brief blog post previously titled:

- [***Fundamental of Computer Networking and Data Communication : Part 1 (Backbone Basic Terms Everybody Should Know)***]({{< ref "blogs/78-computer-networking-intro.md" >}}), 

where tried to explain all these concept. So please read it if you are genuinely interested.

### OSI & TCP/IP Models

*   **Layer functions**: Application Layer (Layer 7), Presentation Layer (Layer 6), Session Layer (Layer 5), Transport Layer (Layer 4), Network Layer (Layer 3), Data Link Layer (Layer 2), Physical Layer (Layer 1).
*   **Data flow through internet**: How data move from host/source to host/destination in low level.

I had written a brief blog post previously titled:

- [***Fundamental of Computer Networking and Data Communication : Part 2 (How Data Moves Through the Internet)***]({{< ref "blogs/79-computer-networking-data-movement-osi.md" >}}), 

where tried to explain all these concept. So please read it if you are genuinely interested.

### IP Addressing. Ports & Protocols

*   **IP Address**: Unique signature / ID or address that is used for identify a device/host in internet. 2 types of IP variation available and they are IPv4 (32 bit) & IPv6 (128 bits).
*   **Loop back IP**: It is basically the localhost. Means when a computer need to route himself that IP is used.
*   **Broadcast IP**: It is also a dedicated IP in a network which used to be a gateway to talk with internet or other network.
*   **Ports**: It is the granular point which point to a application. In OS a application is run on a port and in networking some ports are dedicated for special purpose.
*   **CIDR/Subnetting**: CIDR is a notation for defining a network block and Subnetting means split a network into multiple network blocks.
*   **Protocols**: It is essential sets of rules that dictate how data is formatted, transmitted, and received between devices on a network. Some well known protocols are: TCP/ UDP/ HTTP/ HTTPS/ DNS/ DHCP/ SSH etc.

I had written 3 brief blog post previously titled:

- [***Fundamental of Computer Networking and Data Communication : Part 3 (Important Protocols and How They Work)***]({{< ref "blogs/80-computer-networking-protocols.md" >}})
- [***Fundamental of Computer Networking and Data Communication : Part 4 (Brief Description of Some Networking Concepts)***]({{< ref "blogs/81-computer-networking-buzzwords.md" >}})
- [***Fundamental of Computer Networking and Data Communication : Part 5 (Important Network Configurations)***]({{< ref "blogs/82-computer-networking-configurations.md" >}}), 

where tried to explain all these concept. So please read it if you are genuinely interested.

### NIC, NAT, ARP & Routing

*   **Network interface card**: It is the connection point between the device/host with the internet/network. NIC maps device mac id with host IP address.
*   **MAC address table**: Network devices, such as switches, maintain a MAC address table (also known as a CAM table) that maps MAC addresses to specific ports.
*   **Network IP address translation**: NATing is the process to translate private IP to a public IP so that can connect to outside internet.
*   **ARP table/ ARP cache**: Resolves IP addresses to MAC addresses.
*   **Routing tables**: A routing table is a data table stored in a router or a networked computer that lists the routes to particular network destinations.
*   **Static vs Dynamic routing**: Manually configured routes. Simple but not scalable for large networks.
*   **Default gateway**: Automatically adjusts routes based on current network conditions using routing protocols.

I had written 3 brief blog post previously titled:

- [***Fundamental of Computer Networking and Data Communication : Part 3 (Important Protocols and How They Work)***]({{< ref "blogs/80-computer-networking-protocols.md" >}})
- [***Fundamental of Computer Networking and Data Communication : Part 4 (Brief Description of Some Networking Concepts)***]({{< ref "blogs/81-computer-networking-buzzwords.md" >}})
- [***Fundamental of Computer Networking and Data Communication : Part 5 (Important Network Configurations)***]({{< ref "blogs/82-computer-networking-configurations.md" >}}), 

where tried to explain all these concept. So please read it if you are genuinely interested.

* * *

## Summary:

Networking involves connecting computers, devices, and systems to share resources and information. And data communication refers to the process of transmitting data between two or more devices. This data transmission process involves many individual but important components like: host (source and destination devices), networking device like NIC (for connect to network), switch (for inner networking), router (for outer networking), IP addresses, MAC addresses, Protocols like (DNS, DHCP, ARP, HTTPS, TCP, UDP etc.), CIDR and Subnetting. To understand the data flow from one host to other, every layer and its operation is necessary to understand too.

* * *

## Further Readings:

1.  https://www.practicalnetworking.net/index/ccna/ (This is something every body should read and understand)
2.  **BOOK** - Computer Networking: A Top-Down Approach" by Kurose & Ross