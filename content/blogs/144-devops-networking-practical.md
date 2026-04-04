---
title: "DevOps - Step By Step Learning : Part 20 (Hands On Networking Commands, Practically Connect The Theory)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-03-05T00:00:00Z"
tags: ["devops" , "networking", "practical"]
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
    image: "img/blogs/144-devops-networking-practical.jfif"
    caption: "DevOps Networking Practical"
    alt: "DevOps Networking Practical"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 19:** [DevOps - Step By Step Learning : Part 19 (TCP and UDP Are The Backbone of Transport Layer)]({{< ref "blogs/143-devops-networking-tcp-udp.md" >}})
---

{{< figure
    src="/img/blogs/144-devops-networking-practical.jfif"
    caption="DevOps Networking Practical (Photo Credit: Unsplash)"
    align=center
>}}

### Story:

Rasel now wanted to explore and practice the learned theoretical data communication and networking concepts hands-on. He wanted to practically capture as much information as possible about host-to-host packet transfer of each layer of the OSI model using Linux commands. From the high level, Rasel started from the below point:

1.  How to see the source IP and destination IP resolution using DHCP and DNS in the application layer?
2.  How to check this translation and NAT/PAT table?
3.  How to check the TCP segment and UDP datagram?
4.  How to check the routing table that is working at the network layer?
5.  How to check the MAC address table that is working at the data link layer?
6.  How to check the ARP table, the mapping of IP addresses and MAC addresses, and also the bridge between layer 2 and layer 3?

Understanding and practicing those networking commands will help to troubleshoot networking/connection problems effectively.

* * *

Application Layer: DHCP Negotiation and DNS Resolution
------------------------------------------------------

### DHCP Negotiation Process

**Command:**
```bash
dhclient -v
```

**Explanation:**

- -v shows verbose output of DHCP negotiation.

**Sample Output:**

```bash
DHCPDISCOVER on eth0 to 255.255.255.255 port 67
DHCPOFFER from 192.168.1.1
DHCPREQUEST on eth0 to 255.255.255.255
DHCPACK from 192.168.1.1
bound to 192.168.1.10 -- renewal in 3600 seconds.        
```

**What it shows:**

*   DHCPDISCOVER broadcast a request for a DHCP server IP
*   DHCPOFFER shows the DHCP server IP which will offer an IP address
*   DHCPREQUEST accept and request to assign the offered IP address
*   DHCPACK acknowledge request and contains your assigned IP, subnet mask, gateway, DNS server
*   get a bound IP and valid until renewal time

### DNS Resolution

**Command:**

```bash
dig google.com
nslookup google.com
host google.com
whois google.com        
```

**Explanation:**

- google.com is the domain that IP will be resolve.

**Sample Output (dig):**

```bash
; <<>> DiG 9.16.23-RH <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12295
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             267     IN      A       172.217.24.14

;; Query time: 246 msec
;; SERVER: 10.0.2.3#53(10.0.2.3)
;; WHEN: Fri Jun 20 13:48:10 UTC 2025
;; MSG SIZE  rcvd: 55        
```

**What it shows:**

*   You asked DNS: "What's [google.com](https://www.google.com/)’s IP?"
*   DNS replied: 172.217.24.14
*   Application-layer DNS protocol used UDP port 53

* * *

Application/Presentation/Session Layer: Check Application Connection
--------------------------------------------------------------------

### Check Host Availability

**Command:**

```bash
ping google.com
ping 217.160.0.201
nmap -sP 217.160.0.201        
```

**Explanation:**

- google.com domain or 217.160.0.201 IP that availability check.

**Sample Output:**

```bash
PING goole.com (217.160.0.201) 56(84) bytes of data.
64 bytes from 217-160-0-201.elastic-ssl.ui-r.com (217.160.0.201): icmp_seq=1 ttl=45 time=204 ms
64 bytes from 217-160-0-201.elastic-ssl.ui-r.com (217.160.0.201): icmp_seq=2 ttl=45 time=206 ms
64 bytes from 217-160-0-201.elastic-ssl.ui-r.com (217.160.0.201): icmp_seq=3 ttl=45 time=199 ms
64 bytes from 217-160-0-201.elastic-ssl.ui-r.com (217.160.0.201): icmp_seq=5 ttl=45 time=198 ms        
```

**What it shows:**

*   Its pinging the 217.160.0.201 which is google.com
*   Send ICMP echo request
*   Get ICMP echo response
*   Also shows ttl, icmp sequence number and round trip time

### Check Application Status and Port Connection

**Command:**

```bash
ss -tuln | grep :80
netstat -antpl | grep :80
telnet google.com 80
openssl s_client -connect example.com:443 # inspect TLS handshake manually        
```

**Explanation:**

- 80 is the port where check application running and connection status.

**Sample Output (ss):**

```bash
LISTEN 0 128 :::80 :::*
```

**What it shows:**

*   Its confirming port 80 is listening

* * *

Transport Layer: Analyze TCP Segment and UDP Datagram
-----------------------------------------------------

### Capture Segment/Datagram Details

**Command:**

```bash
tcpdump -i eth0 port 80
nc -zv google.com 80 # Test TCP connectivity (port scanner)        
```

**Explanation:**

- 80 is the port and etho is the interface where we check the inbound segment data.

**Sample Output:**

```bash
IP 192.168.0.10.50544 > 172.217.3.110.443: Flags [S], seq 0, win 29200, length 0        
```

**What it shows:**

*   Hop information means src and dst IP
*   Flags [S] – SYN packet (start of 3-way handshake)
*   seq – Sequence number
*   win – Window size (flow control)

* * *

Network Layer: IP and Routing
-----------------------------

### IP Address Checking

**Command:**

```bash
ip addr show
ifconfig
iwconfig        
```

**Explanation:**

- Show the IP address both ethernet and wireless connection IP.

**Sample Output (ip addr):**

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e4:ec:85 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86368sec preferred_lft 86368sec
    inet6 fe80::a00:27ff:fee4:ec85/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:68:ad:c9 brd ff:ff:ff:ff:ff:ff
    inet 192.168.33.10/24 brd 192.168.33.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe68:adc9/64 scope link
       valid_lft forever preferred_lft forever        
```

**What it shows:**

*   IP addresses with subnet mask in CIDR notation
*   Also shows the interfaces
*   Mac address and broadcast/gateway address

### Routing and Path Checking

**Command:**

```bash
route
ip route show
tracepath -T google.com
mtr google.com
traceroute google.com        
```

**Explanation:**

- Show the route table and tracing of path or route.

**Sample Output (route):**

```bash
default         _gateway        0.0.0.0         UG    100    0        0 enp0s3
default         _gateway        0.0.0.0         UG    102    0        0 enp0s9
10.0.2.0        0.0.0.0         255.255.255.0   U     100    0        0 enp0s3
192.168.0.0     0.0.0.0         255.255.255.0   U     102    0        0 enp0s9
192.168.33.0    0.0.0.0         255.255.255.0   U     101    0        0 enp0s8        
```

**What it shows:**

*   Routing entry with gateway, masking and interface

**Sample Output (traceroute):**

```bash
traceroute to google.com (172.217.24.14), 30 hops max, 60 byte packets
 1  _gateway (10.0.2.2)  1.918 ms  1.029 ms *
 2  tsa01s07-in-f14.1e100.net (172.217.24.14)  31.136 ms  30.616 ms  30.465 ms        
```

**What it shows:**

*   Hop in route to google.com with roundtrip time it takes

* * *

## Transport and Network Layer: NAT/PAT Check

**Command:**

```bash
conntrack -L
```

**Explanation:**

- Show the flow entries of address translation. But you must need to run this on NAT device like router/firewall.

**Sample Output (ss):**

```bash
tcp  6 431999 ESTABLISHED src=192.168.0.10 dst=172.217.3.110 sport=50544 dport=443 [UNREPLIED]
    src=172.217.3.110 dst=203.0.113.55 sport=443 dport=50544        
```

**What it shows:**

*   Your private IP 192.168.0.10 maps to public IP 203.0.113.55
*   sport/dport: source and destination ports — PAT
*   NAT replaces internal IP/port with public IP/port

* * *

Data Link Layer: MAC Address
----------------------------

### Check Mac Address

**Command:**

```bash
ip link show
bridge fdb show        
```

**Explanation:**

- Show the mac address of network interface and mac address table.

**Sample Output (ip link):**

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:e4:ec:85 brd ff:ff:ff:ff:ff:ff
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:68:ad:c9 brd ff:ff:ff:ff:ff:ff
4: enp0s9: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:b1:b0:ad brd ff:ff:ff:ff:ff:ff        
```

**What it shows:**

*   link/ether shows the mac address

**Sample Output (bridge):**

```bash
33:33:ff:e4:ec:85 dev enp0s3 self permanent
01:00:5e:00:00:01 dev enp0s8 self permanent        
```

**What it shows:**

*   mac address table entry

* * *

## ARP Table: Bridging Layer 2 & 3

**Command:**

```bash
arp -n
ip neigh
```

**Explanation:**

- Show the ip to mac mapping entry list.

**Sample Output (ss):**

```bash
Address          HWtype  HWaddress           Flags Mask Iface
192.168.1.1      ether   00:11:22:33:44:55   C           eth0        
```

**What it shows:**

*   Shows IP-to-MAC mapping
*   Used when sending IP packets on Ethernet

* * *

### Summary:

- Check DNS IP of a Domain

```bash
dig example.com
nslookup example.com        
```

- Inspect DHCP Negotiation

```bash
dhclient -v
```

- Capture HTTP Request

```bash
tcpdump -i eth0 port 80
```

- Check if Application is Listening on a Port

```bash
ss -tuln
```

- Diagnose Routing Issues (Hops to Destination)

```bash
traceroute <host> (e.g., traceroute 8.8.8.8)        
```

- Verify NAT Translation

```bash
conntrack -L | grep <IP>
```

- View ARP Table (IP ↔ MAC Mapping)

```bash
arp -n
ip neigh
```

- Check Network IP, Route, Interface Status and MAC Address

```bash
ip link show
ip addr show
ip route show
bridge fdb show        
```
