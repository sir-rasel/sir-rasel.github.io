---
title: "DevOps - Step By Step Learning : Part 18 (NAT, PAT For Inner Private with Outer Public Network Handshaking)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-03-03T00:00:00Z"
tags: ["devops" , "networking", "nat", "pat"]
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
    image: "img/blogs/142-devops-networking-nat-pat.jfif"
    caption: "DevOps Networking NAT & PAT"
    alt: "DevOps Networking NAT & PAT"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 17:** [DevOps - Step By Step Learning : Part 17 (ARP Is The Bridge Between Data Link and Network Layer)]({{< ref "blogs/141-devops-networking-arp.md" >}})
---

{{< figure
    src="/img/blogs/142-devops-networking-nat-pat.jfif"
    caption="DevOps Networking NAT & PAT (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel found that the one and only unique need to communicate with each other throughout the internet is an IP address. Every host/device needs a universally unique IP address so that routing can be possible from source to destination. Also, while Rasel played with packet tracing and IP addresses, he observed that the inner and outer IPs were not the same. When a packet passes through the router to the internet, then an IP change happens. Besides this, the most used IP address scheme is IPv4, which has 4 bytes or 32 bits, and the universally unique IP can be 2^32 or ~4.2 billion IP addresses. But as the Internet grew in popularity, the industry realized there would one day be more hosts on the Internet than there were IP addresses available. So IPv6 was created, but it is complex and not mostly used. So Rasel wanted to know the magic behind this IP changing.

* * *

## What Is an IP Address?

An IP address is a **unique identifier** for a device on a network (like 192.168.1.5 or 8.8.8.8).

### Private IPs (Reusable)

*   Not routable on the internet.
*   Used **inside local** networks.
*   Can be reused in many networks.
*   Defined by [RFC 1918]: **10.0.0.0 – 10.255.255.255** for Large private networks, **172.16.0.0 – 172.31.255.255** for Medium networks, **192.168.0.0 – 192.168.255.255** for Small/home networks.

Example: Your laptop at home may have 192.168.0.5.

### Public IPs (Unique)

*   Routable on the internet.
*   Assigned by **ISPs** or cloud providers.
*   Must be **globally unique**.

Example: Google DNS has a public IP: 8.8.8.8.

* * *

NAT (Network Address Translation)
---------------------------------

### What Is NAT?

NAT (Network Address Translation) is a technique used to **translate IP addresses** between private and public networks. Means it only manipulates the Network Layer / L3 header.

### Why We Need NAT

*   IPv4 addresses are limited.
*   Protects internal network structure (security).
*   Allows **internet access** for private IP devices.

### How NAT Works (Basic)

1.  A device with private IP (e.g., 192.168.1.10) sends a request to the internet.
2.  NAT device (router/firewall/load balancer/server) **translates** it to public IP (e.g., 203.0.11.1) and keeps a record.
3.  Response from the internet is **translated back** to private IP (e.g., 192.168.1.10) using the record.

### Static NAT

**What Is It?**: It is *One-to-One* mapping between a private IP and a public IP.

**Use Case**: Hosting internal services (like a web server) that need *fixed public access*.

**Example**: Map 192.168.10.5 to 203.10.3.5 for web hosting.

**How It Works**: Admin configures the mapping and incoming or outgoing traffic is always used the same mapping.

### Dynamic NAT

**What Is It?**: It is *Many-to-Many* mapping between private IPs and a pool of public IPs.

**Use Case**: For temporary internet access when you have *multiple public IPs*.

**Example**:

*   Pool: 203.0.113.10 - 203.0.113.14.
*   User 192.168.1.11 gets assigned 203.0.113.11.
*   Next user gets the next free public IP

**How It Works**: Admin configures the pool of public IPs and incoming or outgoing traffic is always used this pool.

**Limitation**: When the public pool is full, *new connections are blocked*.

* * *

PAT (Port Address Translation)
------------------------------

### What Is PAT?

PAT (Port Address Translation) is a **Many-to-One** mapping, that is many private IPs share a **single public IP**, distinguished by **port numbers**. Means it manipulates both the Network Layer / L3 header and Transport Layer / L4 header.

### Why We Need PAT

*   Home networks, offices, cloud VPCs etc. need many host but limited Public IPs.
*   Most common NAT type used in todays world.

### How PAT Works (Basic)

*   A device with private IP (e.g., 192.168.1.10) and specific port (e.g., 3333) sends a request to the internet.
*   NAT/PAT device (router/firewall/load balancer/server) **translates** it to public IP (e.g., 203.0.11.1) and a port (e.g., 33) and keeps a record.
*   Response from the internet is **translated back** to private IP (e.g., 192.168.1.10) with specific port (e.g., 3333) using the record.
*   The router tracks source port to IP/port mapping.

### Static PAT

**What Is It?**: It is *One-to-One* mapping of IP:Port to IP:Port.

**Use Case**: Hosting multiple services (e.g., HTTP, SSH) on *one public IP*.

**Example**:

*   203.0.113.5:80 → 192.168.1.10:8080
*   203.0.113.5:22 → 192.168.1.11:22

**How It Works**: Admin maps specific ports for public access.

### Dynamic PAT

**What Is It?**: It is like static PAT, but *assigns public ports dynamically* from a pool.

**Use Case**:

*   Large office network with a single public IP.
*   Clients access internet using *dynamic port mappings*.

**Example**:

*   192.168.1.100:56789 → 203.0.113.5:45000
*   Router manages these entries in NAT table.

**How It Works**: Admin configures the subnet of private IPs to public IPs and incoming or outgoing traffic is used ports dynamically.

* * *

### Policy NAT (Conditional NAT)

*   NAT translation based on *specific rules or match conditions* (like source IP, destination IP, port).
*   Used in firewalls and complex enterprise networks.

Example:

*   Translate only if going to a specific destination:

> If source = 10.1.1.0/24 and destination = 8.8.8.8 → apply NAT

### Twice NAT (Double NAT)

*   Both *source and destination* addresses are translated.
*   Used in VPNs, B2B networks, overlapping IPs.

Example:

*   10.1.1.10 → 192.168.1.10
*   172.16.1.20 → 10.10.10.20

***Used when:***

*   Both companies use 10.0.0.0/8
*   You rewrite both sides to avoid collision

* * *

### Further Readings:
- https://www.practicalnetworking.net/series/nat/nat/

* * *

## Summary:

NAT is the process of used private IP internally but also published those host to the internet via public IP. Static NAT is 1:1 mapping and often use for hosting internal services. Dynamic NAT is Many:Many mapping and generally use for temporary external access. PAT is Many:1 with Ports mapping and usually use for general internet access. Static PAT is IP:Port → IP:Port mapping and use for port-based services on one public IP. Dynamic PAT leverage dynamic ports used Many internal → One public IP.

Policy NAT is a conditional NAT and gives ability to apply custom rules. Twice NAT apply NAT on both src/dst IP and resolve IP overlap issues.