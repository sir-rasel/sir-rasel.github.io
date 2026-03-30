---
title: "DevOps - Step By Step Learning : Part 14 (Why Need Networking, What Theoretical and Practical Knowledge Should Know)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-27T00:00:00Z"
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
    image: "img/blogs/138-devops-networking.jfif"
    caption: "DevOps Networking Knowledge"
    alt: "DevOps Networking Knowledge"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 21:** [DevOps - Step By Step Learning : Part 21 (Shell Scripting - Tool For Automation Repetitive Task)]({{< ref "blogs/137-devops-shell-scripting.md" >}})
- **Part 15:** [DevOps - Step By Step Learning : Part 15 (Learn Fundamental Networking Theoretical Knowledge)]({{< ref "blogs/139-devops-networking-theoretical-knowledge.md" >}})
---

{{< figure
    src="/img/blogs/138-devops-networking.jfif"
    caption="DevOps Networking Knowledge (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel heard and saw network engineering a lot more times when exploring and studying DevOps. He began to realize that practically every tool used in DevOps had some sort of connection to networking. Rasel therefore made a decision to understand the significance and essence of networking before moving forward, and he took action accordingly.

* * *

## Why Networking Is Essential in DevOps?

*   ***Everything Runs on a Network***

Whether it's a container, VM, microservice, database, or cloud function - **they all communicate over networks**. If the network fails, your entire application can break.

*   ***Infrastructure as Code (IaC) Requires Network Design***

When using tools like Terraform you provision: VPCs, Subnets, Route tables, Security groups & firewalls, Load balancers, NAT gateways etc. So You **must understand how these work** to design, troubleshoot, and automate infrastructure.

*   ***Containers & Kubernetes Rely Heavily on Networking***

In containerized environments: Containers must communicate within a pod, across pods, across nodes. You manage service discovery, DNS, ports, and network policies. In Kubernetes, network plugins (CNI) control communication. So without networking knowledge you can't troubleshoot **connection** or **reachability** issues in containers.

*   ***Cloud Environments Are Software-Defined Networks***

Cloud platforms like AWS, GCP, Azure are **built around virtual networking** and topics need to know like: Public/private subnets, Firewalls (security groups, NACLs), Elastic IPs and DNS zones, Peering, VPNs, Transit Gateways etc. So Misconfigured VPC tends to no access to app, broken CI/CD, or open security hole.

*   ***Security and Compliance Need Networking Controls***

DevOps engineers are also responsible for **securing infrastructure**, which involves: Restricting traffic using firewalls, Enforcing zero-trust networking, Managing SSL/TLS certificates, Applying network policies in Kubernetes.

*   ***Monitoring, Logging, and Debugging Require Network Insight***

Many DevOps issues are network-related, and solving them needs: Tools like curl, ping, telnet, traceroute, tcpdump, wireshark, netstat, ss. DNS resolution checks, Firewall and port analysis is also needed. Hard reality is, 90% of the time, when "the app doesn't work," it's a **network misconfiguration**.

*   ***CI/CD, GitOps, Remote Access - All Over the Network***

GitOps tools pull manifests over the internet. CI/CD pipelines push artifacts to remote registries. SSH and VPN are used to access cloud instances. Understanding how these connect, authenticate, and secure data is crucial.

> **Bottom Line**: Without networking knowledge, a DevOps engineer can't effectively build, deploy, or secure modern infrastructure.

* * *

## Theoretical Knowledge

*   **Goal**: Build strong conceptual understanding to reason about real-world networking problems.

***Core Concept:***

*   **Networking Basics** - Types of network, Network topology, Networking devices, Transmission media and communication model.
*   **OSI & TCP/IP Models** - Layer functions, data flow through internet.
*   **Ports & Protocols** - TCP vs UDP, Ports (22, 80, 443, etc.), HTTP/HTTPS/DNS/DHCP/SSH etc.
*   **IP Addressing** - IPv4, IPv6, CIDR, Subnetting, Subnet masking, loop back IP, broadcast IP.
*   **Routing** - Routing tables, static vs dynamic routing, default gateway.
*   **NIC, NAT & ARP** - Network interface, MAC address table, Network IP translation, ARP table/cache.
*   **Firewall Basics** - Request controlling, rule evaluation, ingress/egress filtering.
*   **Linux Namespace** - How the network space segregation work.

***DevOps Focused Concept:***

*   **Cloud Networking** - VPC, Subnets, Gateways, Security Groups, Route Tables.
*   **Load Balancing** - L4 (TCP) NLB vs L7 (HTTP) ALB, NGINX, HAProxy.
*   **Service Discovery** - DNS-based discovery, internal DNS, Consul.
*   **Kubernetes Networking** - Cluster IP, NodePort, LoadBalancer, Ingress, CNI.
*   **TLS/SSL & Encryption** - HTTPS, certs, handshake, CA, mTLS.
*   **Zero Trust & Network Security** - Basic principles of secure networking.

* * *

## Practical Knowledge

*   **Goal**: Gain real-world hands-on experience to troubleshoot, build, and manage networks as a DevOps engineer.

***Networking CLI Tools:***

*   ping, traceroute - Test connectivity and route.
*   dig, nslookup - DNS resolution & troubleshooting.
*   curl, wget - HTTP testing & headers.
*   netstat, ss, lsof - Port monitoring & open sockets.
*   tcpdump, wireshark - Packet capture & analysis.

* * *

## Summary:

Networking is very important in DevOps because everything runs over a network. Applications, containers, databases, and cloud services all need to communicate with each other, and networking makes that possible. In the cloud, you must set up virtual networks, subnets, gateways, and firewalls, which are all part of networking. Tools like Docker and Kubernetes also rely heavily on networking to connect services, route traffic, and enforce access rules. Security depends on controlling who can connect to what, using firewalls, ports, and network policies. CI/CD pipelines send and receive data over the internet, so understanding networking helps keep them running smoothly. When things break, DevOps engineers often use tools like ping, curl, dig, and tcpdump to find and fix network problems. In short, without networking knowledge, it’s very hard to build, deploy, secure, or manage systems in DevOps.