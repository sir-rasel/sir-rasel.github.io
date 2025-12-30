---
title: "Fundamental of Computer Networking and Data Communication : Part 3 (Important Protocols and How They Work)"
description: "Let's learn the fundamentals of networking and data communication!"
date: "2025-12-27T02:00:00Z"
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
    image: "img/blogs/80-networking-protocol.png"
    caption: "Networking Protocols"
    alt: "Networking Protocols"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [Fundamental of Computer Networking and Data Communication : Part 2 (How Data Moves Through the Internet)]({{< ref "blogs/79-computer-networking-data-movement-osi.md" >}})
- **Part 4:** [Fundamental of Computer Networking and Data Communication : Part 4 (Brief Description of Some Networking Concepts)]({{< ref "blogs/81-computer-networking-buzzwords.md" >}})
---

{{< figure
    src="/img/blogs/80-networking-protocol.png"
    caption="Networking Protocols (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the fundamentals of computer networking and data communication. We will try to learn the different computer networking and data communication aspects one by one. In this part, we try to explore some of the important networking protocols.

So let's get started...

---

## Application Layer Protocols
From the previous part we already know that, Application Layer in TCP/IP model provides network services directly to end-user applications (e.g., HTTP, FTP). Some application layer protocols are:

### HTTP (Hypertext Transfer Protocol)
- **Function**: Transfers web pages from a server to a client (web browser).
- **How it works**: A client sends an HTTP request to the server. The server processes the request and sends back an HTTP response with the requested content. The content is typically HTML, but can include images, videos, and other resources. Some well-defined and structured headers are also used in both the request and response ends. Port 80/8080 is used in general.
- **Example**: When you type a URL into your web browser, an HTTP request is sent to the server hosting the web page.

### HTTPS (Hypertext Transfer Protocol Secure)
- **Function**: Secure version of HTTP, encrypts data for secure communication.
- **How it works**: Uses SSL/TLS protocols to establish a secure connection. Ensures data confidentiality and integrity by encrypting the data exchanged between client and server. Prevents eavesdropping and tampering. Port 443 is used in general.
- **Example**: Accessing a banking website where sensitive information needs to be protected.

### FTP (File Transfer Protocol)
- **Function**: Transfers files between client and server.
- **How it works**: Establishes a control connection on port 21 and data connection on port 20. Client can upload, download, delete, or list files on the server.
- **Example**: Uploading a website's files to a web server.

### SMTP (Simple Mail Transfer Protocol)
- **Function**: Sends emails from clients to servers and between servers.
- **How it works**: Client sends an email to an SMTP server. SMTP server forwards the email to the recipient's mail server. Relies on DNS to resolve domain names to IP addresses for mail delivery.
- **Example**: Sending an email from your email client to another person's email address.

### IMAP (Internet Message Access Protocol)
- **Function**: Retrieves emails from a mail server, allows online and offline access.
- **How it works**: Client connects to the mail server and synchronizes messages. Supports multiple mailboxes and allows server-side search and management of emails.
- **Example**: Accessing your email account from multiple devices and keeping them in sync.


### POP3 (Post Office Protocol 3)
- **Function**: Retrieves emails from a mail server.
- **How it works**: Client downloads emails from the server to the local device. Typically removes the email from the server after downloading.
- **Example**: Downloading all your emails to a single device and deleting them from the server.

### DNS (Domain Name System)
- **Function**: Translates domain names into IP addresses.
- **How it works**: Client sends a DNS query to a DNS server. DNS server responds with the corresponding IP address.
- **Example**: Translating "www.abcd.com" into its corresponding IP address to connect to the website.

### DHCP (Dynamic Host Configuration Protocol)
- **Function**: Assigns IP addresses to devices on a network automatically.
- **How it works**: Client sends a DHCPDISCOVER message to locate DHCP servers. DHCP server responds with a DHCPOFFER message. Client sends a DHCPREQUEST message to request the offered address. DHCP server sends a DHCPACK message to acknowledge and complete the process. This process is known as **DORA** process.
- **Example**: Automatically assigning an IP address to your laptop when it connects to a Wi-Fi network.

---

## Transport Layer Protocols
From the previous part we already know that, Transport Layer in TCP/IP model ensures reliable or fast data transfer with protocols like TCP and UDP. Some of transport layer protocols are:

### TCP (Transmission Control Protocol)
**Function**: Provides reliable, ordered, and error-checked delivery of data.
**How it works**: Establishes a connection using a three-way handshake (SYN, SYN-ACK, ACK). Segments data into packets and ensures all packets arrive and are reassembled in order. Provides error checking, flow control, and retransmission of lost packets. This called TCP handshaking.
**Example**: Loading a web page where all elements need to be correctly received and reassembled.

### UDP (User Datagram Protocol)
**Function**: Provides a simpler, connectionless communication model.
**How it works**: Sends packets (datagrams) without establishing a connection. Does not guarantee delivery, order, or error checking.
**Example**: Streaming video or online gaming where speed is prioritized over reliability.

---

## Network/Internet Layer Protocols
From the previous part we already know that, Network/Internet Layer in TCP/IP model handles logical addressing and routing of data packets (e.g., IP). Some of internet layer protocols are:

### IP (Internet Protocol)
- **Function**: Responsible for addressing and routing packets of data.
- **How it works**: Assigns unique IP addresses to devices. Routes packets from the source IP address to the destination IP address using routing tables.
- **Example**: Sending data from your computer to a remote server.

### ICMP (Internet Control Message Protocol)
- **Function**: Used for diagnostic and error messages.
- **How it works**: Sends error messages (e.g., destination unreachable) and operational information (e.g. ping response). Helps in troubleshooting network issues.
- **Example**: Using the ping command to check if a server is reachable.

---

## Link/Network Access Layer Protocols
From the previous part we already know that, Link/Network Access Layer in TCP/IP model manages physical network hardware and media access (e.g., Ethernet, Wi-Fi). Some of link layer protocols are:

### Ethernet
- **Function**: A family of networking technologies for local area networks (LANs).
- **How it works**: Uses MAC addresses to identify devices on the same network. Provides error checking and frame synchronization.
- **Example**: Connecting devices in a home or office network using Ethernet cables.

### PPP (Point-to-Point Protocol)
- **Function**: Provides direct communication between two network nodes.
- **How it works**: Establishes a connection, encapsulates network layer packets, and transports them over a point-to-point link. Performs authentication, encryption, and compression.
- **Example**: Dial-up internet connections or direct connections between two computers.

---

## Others
There are some other important protocols that take part in data communication through the internet. Some of them are:

### ARP (Address Resolution Protocol)
- **Function**: Resolves IP addresses to MAC addresses.
- **How it works**: Broadcasts an ARP request to all devices on the network asking for the MAC address corresponding to a specific IP address. The device with the matching IP address responds with its MAC address. Then this MAC address to IP address mapping manage in a table called ARP cache.
- **Example**: Ensuring data packets are correctly delivered to the destination device on a local network.

### NTP (Network Time Protocol)
- **Function**: Synchronizes clocks of computer systems.
- **How it works**: Client requests the current time from an NTP server. NTP server responds with the current time, allowing the client to adjust its clock.
- **Example**: Ensuring all devices on a network have the same accurate time.

### SSH (Secure Shell)
- **Function**: Provides a secure channel over an unsecured network.
- **How it works**: Establishes an encrypted connection between client and server. Allows secure remote login, command execution, and file transfer.
- **Example**: Securely accessing and managing a remote server over the internet.

---

## Routing and MAC Address Table Resolution:

### Routing
It is the process of selecting a path for traffic in a network or between networks. Routers use routing tables and protocols to determine the best path for data packets to travel from the source to the destination.

***1. Key Concepts in Routing***

- **Routing Table**:

A routing table is a data table stored in a router or a networked computer that lists the routes to particular network destinations. Each entry typically includes the destination IP address, subnet mask, next-hop address (the IP address of the next router), and the interface to be used.

- **Routing Protocols:**

-- **Static Routing**: Manually configured routes. Simple but not scalable for large networks.
-- **Dynamic Routing**: Automatically adjusts routes based on current network conditions using routing protocols. Examples include: 
- *RIP (Routing Information Protocol)*: Uses hop count as a metric, suitable for small networks.
- *OSPF (Open Shortest Path First)*: Uses link state routing, suitable for larger and more complex networks.
- *EIGRP (Enhanced Interior Gateway Routing Protocol)*: Combines features of both distance vector and link state protocols.
- *BGP (Border Gateway Protocol)*: Used for routing between autonomous systems on the internet.


***2. Routing Process:***

- **Packet Creation**: A data packet is created at the source device with source and destination IP addresses.
- **Initial Routing Decision**: The packet is sent to the first router, typically the default gateway.
- **Path Selection**: The router examines its routing table to determine the next hop towards the destination. It uses the destination IP address to look up the best route.
- **Forwarding**: The packet is forwarded to the next hop router based on the routing table entry.
- **Repeat**: Steps 3 and 4 are repeated at each router until the packet reaches the destination network.
- **Final Delivery**: The packet is delivered to the destination device once it reaches the destination network.

### MAC Table Resolution
It involves mapping IP addresses to MAC (Media Access Control) addresses so that data can be correctly delivered within a local network.

***1. Key Concepts in MAC Address Table Resolution***

- **MAC Address**:

A unique identifier assigned to network interfaces for communications on the physical network segment. Usually a 48-bit address represented in hexadecimal format (e.g., 00:1A:2B:3C:4D:5E).

- **ARP (Address Resolution Protocol)**:

Resolves IP addresses to MAC addresses. Essential for communication within the same local network or subnet.



***2. MAC Address Resolution Process***

- **ARP Request**:

When a device wants to send data to another device on the same local network, it needs to know the MAC address of the destination device. The source device sends an ARP request as a broadcast message to all devices on the local network, asking "Who has IP address X.X.X.X? Tell MAC address Y.Y.Y.Y."

- **ARP Reply**:

The device with the matching IP address responds with an ARP reply, providing its MAC address.
This reply is sent directly to the requesting device, not as a broadcast.

- **MAC Address Table**:

Network devices, such as switches, maintain a MAC address table (also known as a CAM table) that maps MAC addresses to specific ports. When a switch receives a frame, it looks up the destination MAC address in its MAC address table to determine the correct port to forward the frame to.

- **Frame Forwarding**:

Once the source device has the destination MAC address, it encapsulates the data packet in an Ethernet frame with the destination MAC address. The frame is sent to the local network, where switches use their MAC address tables to forward the frame to the correct port, ultimately reaching the destination device.

- **Caching and Timeouts**:

ARP entries are cached for a short duration (usually a few minutes) to reduce the need for repeated ARP requests. Entries that are not used within this time are removed from the cache.

---

## Summary
These protocols work together across different layers to facilitate various aspects of network communication, ensuring data is correctly transmitted, received, and processed across the internet and other networks. So its crucial to understand how they work and collaborate together for effective data transmission.

## Learning Resources:
- [Network Fundamentals](https://www.youtube.com/playlist?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi)
- [Subnetting](https://www.youtube.com/playlist?list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE)
- [Basic Concepts](https://www.youtube.com/watch?v=IPvYjXCsTg8)

---

*Insha Allah, we will try to explore some of the protocols working procedure in depth in future.*
