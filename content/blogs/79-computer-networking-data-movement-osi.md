---
title: "Fundamental of Computer Networking and Data Communication : Part 2 (How Data Moves Through the Internet)"
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
    image: "img/blogs/79-data-flow.gif"
    caption: "Data Movement Through The Internet"
    alt: "Data Movement Through The Internet"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [Fundamental of Computer Networking and Data Communication : Part 1 (Backbone Basic Terms Everybody Should Know)]({{< ref "blogs/78-computer-networking-intro.md" >}})
---

{{< figure
    src="/img/blogs/79-data-flow.gif"
    caption="Data Movement Through The Internet (Photo Credit: practicalnetworking.net)"
    align=center
>}}

In this series, we try to explore the fundamentals of computer networking and data communication. We will try to learn the different computer networking and data communication aspects one by one. In this part, we try to explore how data moves through the internet. We will try to understand the overall concept using 2 analogy.

So let's get started...

---

## Story 1:
Once upon a time, there were two powerful empires, the Ottoman Empire and the Mongol Empire. They frequently sent letters to pass news and data. As those letters were very confidential and important, they maintained a secure process for sending the letters from one palace to another. Here's how they did it:
1. First, the Ottoman king wrote/generated the content of the letter.
2. Then he asked his minister to take further actions. The minister changed the content to the Mongol's understandable language, encrypted the letter, and compressed it. Then he passed the encrypted letter to his secretary for further action.
3. The secretary called the Mongol palace's secretary and informed them that they were going to send a very important letter. Once they received it, they were requested to insure it. So, they created a session.
4. After that, the secretary of the Ottoman palace called the coordinator and instructed him to take further action. The coordinator segmented the letter into smaller chunks and assigned a sequence number to each chunk.
5. Then he gave the smaller chunks to the transport officer, who converted them into packets by adding the Mongol palace's address.
6. Next, the transport officer gave the packets to the network officer to send them to the Mongol palace by routing them into the best possible and fastest routes.
7. One of the data officers of the Mongol palace received the packets and added a uniquely identifiable address to each packet and made them frames. Then, he passed them to the Mongol king's personal assistant.
8. Finally, the Mongol king received the letter, and the secretary of the Mongol palace assured the secretary of the Ottoman palace that they received the letter and the session was completed.

In this story, we can see how a secure process was used for sending a confidential letter from the Ottoman place to the Mongol place.

## OSI Model:
The **OSI** model (Open Systems Interconnection model) is a conceptual framework used to describe the functions of a networking system. It consists of seven layers that define how data is transmitted over a network. Each layer provides a specific service that is independent of the others, and they work together to ensure that data is transmitted correctly and efficiently.

## Layers of the OSI Model:
The data transmission process from source to destination can be drawn by mentioning the layers of the OSI model. The data transmission process can be broken down into several steps, each of which involves one or more layers of the OSI model:

### 1. Application layer (Layer 7): 
The data transmission process begins with an application, such as a web browser, email client, or file transfer protocol (FTP) client, that generates data to be transmitted. The application layer prepares the data for transmission by encapsulating it in the appropriate protocol format.

For example, when you use a web browser to visit a website, the browser sends a request to the web server using the HTTP (Hypertext Transfer Protocol) protocol. The request typically includes the URL (Uniform Resource Locator) of the website you want to visit.

In the above story, the Ottoman king's letter is the application layer content.

### 2. Presentation layer (Layer 6): 
The presentation layer is responsible for data translation and encryption. It takes the data from the application layer and converts it into a format that can be understood by the receiving application. It also encrypts the data to ensure that it is secure during transmission.

For example, if the web browser is sending data in the form of a webpage, the presentation layer may convert the webpage into HTML (Hypertext Markup Language) format, which is a standardized format for creating webpages.

In the above story, the minister performs the presentation layer's responsibility.

### 3. Session layer (Layer 5): 
The session layer manages the communication between applications by establishing, maintaining, and terminating sessions. It allows multiple applications to share the same network connection.

For example, when you visit a website, the session layer establishes a session between your web browser and the web server. The session allows data to be transmitted between the two applications without interference from other applications on the network.

In the above story, the secretary performs the session layer responsibility.

### 4. Transport layer (Layer 4): 
The transport layer provides end-to-end communication between applications on different devices. It ensures that data is transmitted reliably and efficiently by breaking it up into smaller segments and reassembling them at the receiving end. It also provides error correction and flow control.

For example, the transport layer may break the data into smaller segments, add sequence numbers to the segments, and ensure that they are sent in the correct order. If a segment is lost during transmission, the transport layer can request that the segment be retransmitted.

In the above story, the coordinator performs the transport layer work.

### 5. Network layer (Layer 3): 
The network layer is responsible for the routing of data across multiple networks. It decides the best route for data to take based on the destination address and network conditions. Here segments are converted into packets by adding IP addresses.

For example, if you are sending data from your computer to a web server in another country, the network layer may route the data through multiple networks to reach its destination.

In the above story, the network officer performs the network layer responsibility.

### 6. Data link layer (Layer 2): 
The data link layer is responsible for the reliable transmission of data between two nodes on the same network. It ensures that data is transmitted without errors, and it provides error correction and flow control. Here packets are converted to the frame by adding the MAC address with the packets.

For example, the data link layer may use protocols such as Ethernet or Wi-Fi to transmit the data over the network.

In the above story, the data officer performs the data link layer's responsibility.

### 7. Physical layer (Layer 1): 
The physical layer deals with the physical transmission of data over the network, such as the cables, connectors, and other hardware. It defines the electrical and physical characteristics of the transmission medium, such as how data is transmitted and received. Here, a frame becomes a bit for transmission through the media.

For example, the physical layer may use copper or fiber-optic cables to transmit the data, or it may use wireless transmission methods such as radio waves or infrared signals.

In the above story, the Mongol king and his minister are part of the physical layer.

---

## Story 2:
Once upon a time in a bustling digital city, there were two computers — let's call them **Computer-A** and **Computer-B** — and they lived in different locations. Inside the Computer-A, there was some data in an email format. Let's call the data **Data-D**.

**Step 1**: One day Computer-A wanted to send the Data-D to Computer-B. Now to do so, Data-D needs the address of both computers; otherwise, there is a chance to lose the Data-D. So Data-D started his journey by resolving the **source** (where she came from) and **destination** (where she needed to go) computer address.

**Step 2**: Computer-A couldn't send Data-D directly to her destination. Instead, Data-D first had to visit a **neighborhood**. This neighborhood acted like a local post office. It checked Data-D's destination address and decided the best path for her to take.

**Step 3**: The neighborhood sent Data-D onto a super-fast highway **connecting cities** around the world. As Data-D traveled along this highway, she met **other neighbors** at various intersections. Each neighbor examined Data-D's address and forwarded her closer to her destination.

**Step 4**: Along the way, Data-D met **other friends** from different parts of the world. They all traveled together, guided by a special **formula**. This formula helped Data-D by ensuring she didn't get lost and that she arrived safely and in the correct order with her fellow friends.

**Step 5**: After a long journey, Data-D finally reached her destination, Computer-B. The Computer-B, eagerly waiting for Data-D, received her along with her fellow friends.

**Step 6**: Inside the Computer-B, Data-D and all his friends reassembled to form the complete email message. Data-D was proud to have completed her journey, ensuring the user could read the message just as it was sent.

## How Data Moves Through the Internet:
As you can understand from the above story, the journey of data from a source to a destination over the network is not a straightforward task and needs a guided rule for successful transmission.

The OSI model or TCP/IP model described previously is the guided rule for this. This gives us an organized and self-describing way for efficient data moving over the internet. Let's jump into the more detailed journey.

### Starting Point:
The journey of data begins with the **address resolution** of source and destination. This address is called an **IP address**. Basically, when an application like a web browser or email client of the source device, also known as the host device, wants data transmission, the OS resolves the destination address using a protocol called **DNS resolution** [I will cover details in the next part of this series]. So after resolving the destination IP address by DNS resolution and the source IP address by **DHCP (Dynamic Host Control Protocol)** [I will cover details in the next part of this series], the data is ready to move.

This process takes place in the Application Layer (Layer 7) of the OSI model. In the above story, Step-1 does this job.

### Translation and Securing Data:
As the internet is an open place to move, it means an open network, so anyone can move anywhere without any restriction. In this scenario, to protect our data, we need a secret secure format so that only the source and destination can understand that. So at the beginning of moving in the network, data needs to be converted into a machine format called **binary** format, and to secure it, it needs to be **encrypted**, and for faster delivery, it needs to be **compressed**.

This process takes place in the Presentation Layer (Layer 6) of the OSI model.

### Keep the Relation Alive:
In the real world, we introduce ourselves to someone and create a relationship. This relationship or personal networking helps us in the future if we need some help or future interaction with them. The network also works like this. If we talk, visit, or interact for data transmission with some other network/website/application, there is a possibility to create a relationship for future smooth interaction. This relationship in networking is called a **session**.

The session layer manages the communication between applications by establishing, maintaining, and terminating sessions. It allows multiple applications to share the same network connection. This process take place in the Session Layer (Layer 5) of the OSI model.

### Transporting and Service-to-Service Communication:
The channel or medium of a data transmission system, like wire or wireless, has some limitation or **bandwidth** for data transmission. So large data can't be transmitted at a time. That's why we need to **chunk** or **segment** large data into smaller parts so that data can be effectively transmitted through a channel or medium.

The transport layer provides **service-to-service** communication between applications. It ensures that data is transmitted reliably and efficiently by breaking it up into smaller segments and reassembling them at the receiving end. It also provides error correction and flow control. This whole process is handled by a rule called **TCP (transmission control protocol)** or **UDP (user datagram protocol)** [I will cover details in the next part of this series]. This process takes place in the Transport Layer (Layer 4) of the OSI model. In the above story, portions of steps 4, 5, and 6 do this job.

### Routing and End-to-End Communication:
For **end-to-end** communication, meaning **source-to-destination** communication, data needs to travel a long way. So data needs to find the best and shortest route to travel for faster and effective transmission. The network layer manages logical addressing and **routing** of data packets between networks (e.g., IP addresses). It works **end-to-end** and **packets** data with an L3 header.

The network layer is responsible for the routing of data across multiple networks. It decides the best route for data to take based on the destination address and network conditions. Here segments are converted into packets by adding IP addresses. This process takes place in the Network Layer (Layer 3) of the OSI model. In the above story, portions of steps 2 and 3 do this job.

### Linking and Hop-to-Hop Communication:
The Data Link Layer does not provide host-to-host delivery. Instead, there is hop-to-hop (node-to-node) delivery in the data link layer. **Hop-to-hop** delivery in the data link layer can be delivery of packets from the host’s network interface card (NIC) to the router’s interface, or it can be delivery of packets from one router’s interface to another router’s interface, or it can be delivery of packets from one router’s interface to the host’s network interface card (NIC). It does not directly deliver the packets from source to destination; instead, it delivers them from one hop (node) to another.

It ensures reliable data transfer across the physical network, managing MAC addresses and error detection. It works **hop-to-hop** and **frames** data with an L2 header.

The data link layer is responsible for the reliable transmission of data between two nodes on the same network. It ensures that data is transmitted without errors, and it provides error correction and flow control. Here packets are converted to the frame by adding the MAC address with the packets. This process takes place in the Data Link Layer (Layer 2) of the OSI model.

### Raw Data (bitstream) Transmission:
Finally, the last stage deals with the physical transmission of data over the network, such as the cables, connectors, and other hardware. It defines the electrical and physical characteristics of the transmission medium, such as how data is transmitted and received. Here the frame becomes a bitstream for transmission through the media.

For example, the physical layer may use copper or fiber-optic cables to transmit the data, or it may use wireless transmission methods such as radio waves or infrared signals. This process takes place in the Physical Layer (Layer 1) of the OSI model.

---

## Summary of OSI Model:
{{< figure
    src="/img/blogs/79-osi.png"
    caption="OSI Model (Photo Credit: Medium)"
    align=center
>}}

- **Layer 1 - Physical**: Handles the transmission of raw bitstreams over a physical medium (e.g., cables, radio waves).
- **Layer 2 - Data Link**: Ensures reliable data transfer across the physical network, managing MAC addresses and error detection. It works hop to hop and framing data with L3 header.
- **Layer 3 - Network**: Manages logical addressing and routing of data packets between networks (e.g., IP addresses). It works end to end and packeting data with L2 header.
- **Layer 4 - Transport**: Ensures complete and reliable data transfer with error checking and flow control (e.g., TCP, UDP). It works service to service and segmenting data.
- **Layer 5 - Session**: Manages sessions or connections between applications.
- **Layer 6 - Presentation**: Translates data between the application and network formats, including encryption and compression.
- **Layer 7 - Application**: Provides network services directly to end-user applications (e.g., HTTP, FTP).

---

## TCP/IP Model:
{{< figure
    src="/img/blogs/79-tcp-ip.png"
    caption="TCP/IP Model (Photo Credit: GeeksForGeeks)"
    align=center
>}}

- **Link Layer / Network Access Layer**: Manages physical network hardware and media access (e.g., Ethernet, Wi-Fi). As the diagram shows, it is almost similar to the OSI model layer 1 + layer 2.
- **Internet Layer**: Handles logical addressing and routing of data packets (e.g., IP). As the diagram shows, it is almost similar to OSI model layer 3.
- **Transport Layer**: Ensures reliable or fast data transfer with protocols like TCP and UDP. As the diagram shows, it is almost similar to OSI model layer 4.
- **Application Layer**: Provides application-specific network services and protocols (e.g., HTTP, FTP, DNS). As the diagram shows, it is almost similar to the OSI model layer 5 + layer 6 + layer 7.

---

## Conclusion:
In short data transmission or packet traveling performs according to the following mechanism:
- **Source Device**: Data is created and segmented into packets.
- **Local Router**: Packets are forwarded to the local router.
- **ISP Network**: ISP routes the packets towards the destination.
- **Internet Backbone**: Packets travel through various routers on the internet.
- **Destination ISP**: ISP forwards packets to the local network of the destination.
- **Destination Device**: Packets are reassembled and delivered to the application.

This process ensures reliable and efficient transmission of data from the source to the destination across the internet.