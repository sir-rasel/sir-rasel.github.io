---
title: "Fundamental of Computer Networking and Data Communication : Part 1 (Backbone Basic Terms Everybody Should Know)"
description: "Let's learn the fundamentals of networking and data communication!"
date: "2025-12-27T00:00:00Z"
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
    image: "img/blogs/79-networking-basic.png"
    caption: "Computer Networking and Data Communication"
    alt: "Computer Networking and Data Communication"
    relative: true
    hidden: true
---

{{< figure
    src="/img/blogs/79-networking-basic.png"
    caption="Computer Networking and Data Communication (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the fundamentals of computer networking and data communication. We will try to learn the different computer networking and data communication aspects one by one. In this part, we try to explore the backbone basic terms that everybody should know.

So let's get started...

---

## Story
Rasel heard and saw network engineering a lot more times when exploring and studying computer scince specially in DevOps. He began to realize that practically every tool used in data communication had some sort of connection to networking. Rasel therefore made a decision to understand the significance and essence of networking before moving forward, and he took action accordingly.

---

## Networking:
**Networking** is nothing but a collection of devices (computers, servers, routers, switches) connected to share data. So the main purpose of networking is: connect devices (computers, servers, routers, switches) so that they can share resources and information. 

Networking encompasses the design, implementation, and management of network infrastructure, which includes hardware (like routers, switches, and cabling) and software (such as network protocols and operating systems).

## Data Communication:
**Data Communication** refers to the process of transmitting data between two or more devices. It involves the exchange of data through a transmission medium (wired or wireless) and ensures that the data is correctly received and understood by the receiving device.

---

## Types of Networks
Based on the size and the area, computer networks can be classified into the following types:

{{< figure
    src="/img/blogs/79-network-type.jfif"
    caption="Types of Network (Photo Credit: LightOptics)"
    align=center
>}}

- **LAN (Local Area Network)**: A network that spans a small geographical area, such as a single building or campus, allowing devices within close proximity to connect and share resources.
- **WAN (Wide Area Network)**: A network that covers a large geographical area, often consisting of multiple LANs connected together. The internet is the largest WAN.
- **MAN (Metropolitan Area Network)**: A network that spans a city or metropolitan area, larger than a LAN but smaller than a WAN.
- **PAN (Personal Area Network)**: A network for personal devices, typically within a range of a few meters, such as connecting a smartphone to a computer via Bluetooth.
- **SAN (Storage Area Network)**: A specialized network that provides access to consolidated data storage, primarily used in data centers.
- **Wireless Local Area Network (WLAN)**: A type of LAN that uses wireless technology, such as Wi-Fi.
- **Virtual Private Network (VPN)**: Creates a secure, encrypted connection over the Internet, allowing users to access a remote network securely.

## Types of Network Topology
Topology in networking means how devices will be connected and their orientation. Based on their connection mechanism, they can be the following types:

{{< figure
    src="/img/blogs/79-network-topology.png"
    caption="Network Topology (Photo Credit: TechTarget)"
    align=center
>}}

- **Star Topology**: All devices are connected to a central hub or switch. If the central device fails, the entire network is affected.
- **Ring Topology**: Each device is connected to two other devices, forming a circular pathway. Data travels in one direction (or both in a dual-ring topology).
- **Bus Topology**: All devices share a common communication line (bus). If the bus fails, the entire network is affected.
- **Mesh Topology**: Every device is connected to every other device, providing multiple pathways for data and high redundancy.
- **Tree Topology**: A combination of star and bus topologies, with groups of star-configured devices connected to a linear bus backbone.
- **Hybrid Topology**: A mix of two or more different types of topologies to leverage the advantages of each.

## Types of Data Communication
Based on data flow direction and timing, data communication can be the following types:

{{< figure
    src="/img/blogs/79-data-communication.webp"
    caption="Data Communication Types (Photo Credit: top10electrical)"
    align=center
>}}

- **Analog Communication**: Transmits data in the form of continuous signals, varying in amplitude or frequency. Example: telephone calls.
- **Digital Communication**: Transmits data in binary form (0s and 1s) using digital signals. Example: internet data transfer.
- **Simplex Communication**: Data transmission in one direction only, like a keyboard sending data to a computer.
- **Half-Duplex Communication**: Data transmission in both directions, but not simultaneously. Example: walkie-talkies.
- **Full-Duplex Communication**: Data transmission in both directions simultaneously, like a phone call.

---

## Networking Devices:
For building a proper computer network, which means connecting multiple computers so that they can share data, we need some networking devices as well. Some of the important networing devices are:

{{< figure
    src="/img/blogs/79-network-devices.png"
    caption="Networking Devices (Photo Credit: Medium)"
    align=center
>}}

- **Repeater**: Amplifies, repeats, regenerates, and extends the range of a network signal or data bits.
- **Hub**: A basic device that connects multiple devices in a network, forwarding data to all connected devices. It can be considered a multiport repeater.
- **Bridge**: Connects multiple hubs and directs data packets between them.
- **Switch**: Connects devices within a single network, using MAC addresses to forward data to the correct destination. It communicates data **within** a network.
- **Router**: Connects multiple networks and directs data packets between them. It communicates data **between** networks.
- **Modem**: Modulates and demodulates signals for data transmission over telephone lines or cable. "Modulates" and "demodulates" mean to convert a signal from analog to digital and from digital to analog.
- **Access Point**: Allows wireless devices to connect to a wired network using Wi-Fi.
- **Firewall**: Monitors and controls incoming and outgoing network traffic based on security rules.
- **NIC (Network Interface Card)**: Hardware that connects a computer to a network.

## Network Security Concepts:
The network is an open place for performing fraud. So proper security and prevention are needed for creating a safe network for everyone. Some of the common techniques are:
- **Authentication**: Verifying the identity of users or devices on a network.
- **Authorization**: Granting access rights and permissions to authenticated users or devices.
- **Encryption**: Encoding data to prevent unauthorized access.
- **Firewall**: Filtering traffic to protect against unauthorized access and attacks.
- **VPN (Virtual Private Network)**: Creating a secure, encrypted connection over a less secure network, such as the Internet.
- **Intrusion Detection System (IDS)**: Monitors network traffic for suspicious activity and alerts administrators.
- **Intrusion Prevention System (IPS)**: Actively blocks or prevents detected threats.

## Transmission Media:
A network generally consists of two important parts. One is **Node**, which is the device that participates in the network, and another one is **Link**, which is the connection or transmission medium. Generally the following transmission media are commonly used:

{{< figure
    src="/img/blogs/79-transmission-media.png"
    caption="Transmission Media (Photo Credit: ResearchGate)"
    align=center
>}}

- **Twisted Pair Cable**: Consists of pairs of wires twisted together to reduce electromagnetic interference. Used in telephony and Ethernet networks.
- **Coaxial Cable**: Contains a central conductor, insulating layer, metallic shield, and outer insulating layer, used for cable television and broadband internet.
- **Fiber Optic Cable**: Uses light to transmit data at high speeds over long distances, offering higher bandwidth and immunity to electromagnetic interference.
- **Wireless Media**: Transmits data through the air using radio waves, microwaves, or infrared signals, used in Wi-Fi, cellular networks, and satellite communications.

---

## Simplified Communication Model:
{{< figure
    src="/img/blogs/79-data-communication-model.png"
    caption="Data Communication Model (Photo Credit: Medium)"
    align=center
>}}

- **Source**: The originator of the data. It's also known as Host.
- **Transmitter**: Converts data into a transmittable format. Network devices come into play at this stage.
- **Transmission Medium**: The physical path or channel over which data is transmitted. It can be wired or wireless.
- **Receiver**: Converts received signals back into data. Again, network devices work here.
- **Destination**: The final recipient of the data. It is also known as a server.

## Conclusion:
Understanding data communication and networking is crucial for engineers and IT professionals. Key foundational concepts include networking basics, data communication processes, and the variety of network types and topologies that dictate how devices connect and interact.

Networking devices, including routers, switches, hubs, modems, and access points, play vital roles in building and maintaining network infrastructures. Network security concepts, such as encryption, firewalls, VPNs, and IDS/IPS, are critical for protecting data integrity and preventing unauthorized access.

Transmission media, including twisted pair cables, coaxial cables, fiber optics, and wireless options, offer various means of data transmission, each with its advantages and applications. The simplified communication model illustrates the fundamental process of data transfer from source to destination.

---

*In the next part, we will try to explore how data moves through the internet using a structured framework called the **OSI** model and the **TCP/IP** model.*