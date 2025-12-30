---
title: "Fundamental of Computer Networking and Data Communication : Part 4 (Brief Description of Some Networking Concepts)"
description: "Let's learn the fundamentals of networking and data communication!"
date: "2025-12-29T02:00:00Z"
tags: ["computer-networking", "data-communication"]
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
    image: "img/blogs/81-network-buzzwords.jfif"
    caption: "Networking Buzzwords"
    alt: "Networking Buzzwords"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 3:** [Fundamental of Computer Networking and Data Communication : Part 3 (Important Protocols and How They Work)]({{< ref "blogs/80-computer-networking-protocols.md" >}})
- **Part 5:** [Fundamental of Computer Networking and Data Communication : Part 5 (Important Network Configurations)]({{< ref "blogs/82-computer-networking-configurations.md" >}})
---

{{< figure
    src="/img/blogs/81-network-buzzwords.jfif"
    caption="Networking Buzzwords (Photo Credit: Google)"
    align=center
>}}

In this series, we try to explore the fundamentals of computer networking and data communication. We will try to learn the different computer networking and data communication aspects one by one. In this part, we try to explore some of the most important networking concepts briefly.

So let's get started...

---

### IP (Internet Protocol):
It is the set of rules governing the format of data sent via the internet or local network. In essence, IP addresses are the identifiers that allow information to be sent between devices on a network: they contain location information and make devices accessible for communication.

### IP Address:
An IP address is a string of numbers separated by periods. IP addresses are expressed as a set of four numbers; an example address might be 192.158.1.38. Each number in the set can range from 0 to 255. So, the full IP addressing range goes from 0.0.0.0 to 255.255.255.255.

### TCP/IP: 
Transmission Control Protocol/Internet Protocol (TCP/IP) is a set of protocols that govern communication over the internet. It is responsible for establishing and maintaining connections between devices on the internet. TCP provides a reliable, connection-oriented service, while IP provides an unreliable, connectionless service.

### TCP handshaking:
{{< figure
    src="/img/blogs/81-tcp-handshake.jpg"
    caption="TCP Handshaking (Photo Credit: work@tech)"
    align=center
>}}
TCP handshaking is a three-way process that is used to establish a connection between two devices over a network. The three steps in the process are:
- **SYN**: The device that wants to establish a connection sends a SYN (synchronize) message to the other device, indicating that it wants to start a connection.
- **SYN-ACK**: The other device responds with a SYN-ACK (synchronize-acknowledge) message, indicating that it has received the SYN message and is willing to establish a connection.
- **ACK**: The device that initiated the connection sends an ACK (acknowledge) message, indicating that it has received the SYN-ACK message and the connection is now established.

### NIC (network interface card):
A network interface card (NIC) is a hardware component that connects a computer to a network. The NIC is responsible for converting data from the computer into a format that can be transmitted over the network and for receiving data from the network and converting it back into a format that the computer can understand. Overall, NIC is an essential component for connecting a computer to a network.

### Firewall: 
A network security device that monitors and filters incoming and outgoing network traffic based on an organization's previously established security policies.

### NAT (Network Address Translation):
It is a technique used in networking to allow devices on a local network to share a single public IP address to access the internet. NAT works by translating private IP addresses used on the local network into a public IP address that can be used on the internet. This private IP to public IP translation is known as NATting.

### AES (Autonomous System):
It is a concept in computer networking that refers to a collection of networks that are managed and controlled by a single organization or entity, known as an Autonomous System. Each autonomous system is assigned a unique identifier, known as an Autonomous System Number (ASN), which is used to identify the network in the global routing table. 

### DHCP (Dynamic Host Configuration Protocol):
It is a network protocol used to dynamically assign IP addresses and other network configuration information to devices on a network. The DHCP server is responsible for assigning IP addresses to devices and also provides information such as subnet masks, default gateways, and DNS server addresses. When a device connects to a network, it sends out a request to the DHCP server, which then responds with an available IP address and other configuration information.

Here are the basic steps involved in the **DHCP process**:
- **DHCP Discover**: The client sends out a broadcast message to the network, asking for a DHCP server to respond. The broadcast message contains a request for an IP address and other network configuration information.
- **DHCP Offer**: When the DHCP server receives the broadcast message, it responds with a message offering an available IP address and other configuration information. The offer is sent to the client's MAC address.
- **DHCP Request**: The client responds to the DHCP offer by sending a request to the server, confirming that it wants to use the offered IP address and network configuration information.
- **DHCP Acknowledge**: Once the server receives the request from the client, it sends a final message acknowledging the request and confirming that the IP address and other configuration information have been assigned to the client.

### CIDR (Classless Inter-Domain Routing) notation:
CIDR notation is a method used to express the size of a network and the associated subnet mask. It is used to allocate IP addresses efficiently and conserve the available address space.

CIDR notation uses a combination of an IP address and a prefix length, separated by a forward slash (/). The prefix length represents the number of bits in the subnet mask that are set to 1.

For example, the IP address 192.168.1.1 with a subnet mask of 255.255.255.0 can be represented in CIDR notation as 192.168.1.1/24. The prefix length of /24 indicates that the first 24 bits of the IP address are used to identify the network, and the remaining 8 bits are used to identify the hosts on the network.

### Subnet Mask:
A subnet mask is a 32-bit number that is used to identify the network portion and the host portion of an IP address. It is used to divide an IP address into a network address and a host address.

The subnet mask consists of a series of contiguous 1 bits followed by a series of contiguous 0 bits. The number of 1 bits in the subnet mask determines the size of the network portion of the IP address. The remaining bits represent the host portion of the IP address.

### User Space and Kernel Space:
User space and kernel space are two distinct memory spaces in an operating system. User space is the memory space where user applications run, while kernel space is the memory space where the operating system kernel runs.

### CAM Table:
A CAM table, also known as a Content Addressable Memory table or MAC address table, is a table used in Ethernet networking to store the MAC addresses of devices connected to a network.

### Network Gateway:
A network gateway is a device that connects two or more different networks together and allows them to communicate with each other. It serves as an entry point for traffic entering a network from outside and an exit point for traffic leaving the network to reach other networks.

The gateway acts as a translator between two different types of networks and can perform various functions such as routing, switching, and protocol conversion. It is often used to connect a private network, such as a LAN, to a public network, such as the Internet, and provides access to resources outside of the private network.

### ARP (Address Resolution Protocol):
It is used in local network to translate an IP address into a MAC address so that data can be delivered at the physical layer. While applications and routing logic rely on IP addresses, the actual transmission of frames on Ethernet or Wi-Fi requires MAC addresses. When a device wants to communicate with another device in the same subnet, it broadcasts an ARP request asking which device owns a specific IP address. The device with that IP responds with its MAC address, and the sender stores this information temporarily in its ARP cache.

### DNS (Domain Name System): 
It is a distributed, hierarchical naming system that translates human-readable domain names into IP addresses so clients can locate servers on a network. Instead of remembering numeric IP addresses, users and applications rely on DNS to resolve names such as example.com into an IP address that can be routed over the internet. When a client performs a DNS lookup, it queries a DNS server, which may respond from cache or recursively consult other DNS servers until the correct IP is found.