---
title: "DevOps - Step By Step Learning : Part 10 (Linux Networking, Compression and Little Scripting for Automation)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-22T00:00:00Z"
tags: ["devops" , "linux"]
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
    image: "img/blogs/133-devops-linux-networking.jfif"
    caption: "DevOps Linux Networking"
    alt: "DevOps Linux Networking"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 9:** [DevOps - Step By Step Learning : Part 9 (Linux Package, User Permission, System Process Management)]({{< ref "blogs/132-devops-linux-package-user-process.md" >}})
---

{{< figure
    src="/img/blogs/133-devops-linux-networking.jfif"
    caption="DevOps Linux Networking (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel learned some of the basic and necessary things of linux. Now he wanted to finish his initial linux learning with one of the most important topics like linux networking and service manager. As devOps is heavily related to networking and service management and linux networking commands and systemctl command are essential for them. After that, he wanted to practice his learning with writing a little script.

* * *

## Linux Networking:

As Linux is heavily used in server side, so managing and debugging the service to service connectivity is essential. And Linux networking related commands helps here to easily manage and operate those tasks.

```bash
ip a
```
This command show all network interfaces and IPs.

```bash
ifconfig
```
This is also do the same, but older command (may need to install).

```bash
ping google.com (or) ping 192.168.1.1
```
This check if the system can reach Google domain name, also can use ip directly.

```bash
telnet example.com 80
```
This check if port 80 is open, and it is older and insecure command for testing connectivity.

```bash
ss -tuln
```
This show listening ports and services.

```bash
netstat -tuln
```
This also do this but older alternative (install if needed).

```bash
nslookup a.com
```
This shows IP and DNS info,

```bash
dig a.com
```
This show more detailed DNS query (install dig if needed).

```bash
ssh user@192.168.1.100
```
This is used to log in to remote server.

```bash
ssh -i key.pem user@host
```
This use SSH key to connect or log in.

```bash
ssh-keygen –t rsa
```
This is used to generate a key pair.

```bash
ssh-copy-id user@remote\_host
```
This copies your local key to remote.

```bash
scp file.txt user@host:/home/user/
```
This securely copy file to another remote server.

```bash
scp user@host:/path/file.txt .
```
This securely download file from remote.

Example:
```bash
ip a             # Show all network interfaces and IP addresses
ifconfig         # Older command, might need installation

ping google.com        # Check internet connectivity
ping 192.168.1.1       # Ping a specific device (e.g., your router)
telnet example.com 80               # Check if port 80 is open

nslookup example.com   # Simple DNS lookup
dig example.com        # Detailed DNS info (may need install)

ss -tuln               # Show listening ports and services
netstat -tuln          # Older alternative (install if needed)

ssh user@192.168.1.100              # Log in to remote server
ssh -i key.pem user@host            # Use SSH key to connect

ssh-copy-id user@remote_host        # Copies your local key to remote
ssh-keygen –t rsa                       # Generate a key pair

scp file.txt user@host:/path/       # Copy file to remote machine
scp user@host:/path/file.txt .      # Download file from remote        
```

* * *

## Compression and Archiving:

Sometimes we need to compress and archive files, folders to reduce its original size before move from local to remote server. It saves bandwidth and perform file transfer faster. Linux gives us many ways to do so.

```bash
tar -czvf archive.tar.gz folder/
```
This compress folder.

```bash
tar -xzvf archive.tar.gz 
```
This do the opposite and extract contents.

```bash
zip myfile.zip file.txt 
```
This create zip.

```bash
unzip myfile.zip
```
This extract zip.

```bash
gzip file.txt
```
This compress.

```bash
gunzip file.txt.gz
```
This decompress.

Example:
```bash
tar -czvf archive.tar.gz folder/     # Compress folder
tar -xzvf archive.tar.gz             # Extract contents

zip myfile.zip file.txt              # Create zip
unzip myfile.zip                     # Extract zip

gzip file.txt                        # Compress (file.txt → file.txt.gz)
gunzip file.txt.gz                   # Decompress        
```

* * *

## System / Service Manager:

In server we deployed or install services. And its natural that we need to start, stop, enable auto start on startup and know their running status. Linux systemctl commands helps us to easily do that.

```bash
sudo systemctl start nginx
```
This start a service.

```bash
sudo systemctl stop nginx
```
This stop a running service.

```bash
sudo systemctl restart nginx
```
This restart a stopped service.

```bash
sudo systemctl status nginx
```
This gives the service status.

```bash
sudo systemctl enable nginx
```
This enables a service auto start on boot.

```bash
sudo systemctl disable nginx
```
This disables a service auto start on boot.

```bash
systemctl list-units --type=service
```
This gives list of all service.

Example:
```bash
sudo systemctl start nginx           # Start a service
sudo systemctl stop nginx            # Stop it
sudo systemctl restart nginx         # Restart it
sudo systemctl status nginx          # Show status

sudo systemctl enable nginx          # Auto-start on boot
sudo systemctl disable nginx         # Disable auto-start

systemctl list-units --type=service  # List all services        
```

* * *

## Little Scripting:

Scripting is the way of combining multiple commands in a single file (generally a bash file) and executes all the command at all. It helps to automate repetitive task and command to execute at once.

Like below we create a simple script that will create a file, add some text and print a hello message.

Step 1 (create a bash file):
```bash
cat simple_script.sh
```

Step 2 (Add the commands):
```bash
#!/bin/bash
cat text.txt
echo "Add text to file" >> text.txt
echo "Hello, DevOps!"        
```

Step 3 (Make it executables):
```bash
chmod +x simple\_script.sh
```

Step 4 (Run it):
```bash
./simple_script.sh
```

* * *

## Summary:

Linux networking tools like ip, ping and ss help you check connections, IPs, and open ports. Commands like ssh helps to remote login and telnet is useful for check connectivity. For moving files between systems, scp is useful. Compression tools like tar, zip, gzip let you package and reduce file sizes. systemctl is used to manage services like web servers (e.g., start, stop, enable on boot). Finally, with basic shell scripting using bash, you can combine multiple commands together to automate repetitive tasks.