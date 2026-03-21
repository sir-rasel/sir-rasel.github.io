---
title: "DevOps - Step By Step Learning : Part 9 (Linux Package, User Permission, System Process Management)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-21T00:00:00Z"
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
    image: "img/blogs/132-devops-linux-process.jfif"
    caption: "DevOps Linux Package, User, Process Management"
    alt: "DevOps Linux Package, User, Process Management"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 8:** [DevOps - Step By Step Learning : Part 8 (Linux Command for File, Directory and Text Manipulation)]({{< ref "blogs/131-devops-linux-file-command.md" >}})
---

{{< figure
    src="/img/blogs/132-devops-linux-process.jfif"
    caption="DevOps Linux Package, User, Process Management (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel already learned commands to manage files, directories, and contents in them without needing any UI and only via CLI. To run an application (maybe frontend, backend, database, or any other program), we need to install many dependencies like other software/applications, packages, or libraries. So Rasel now needs to learn to manage packages via command. Also, for safety, security, and operational purposes, user and permission management is another mission-critical task, so you need to learn this as well. To make operational life easy, efficient, and robust, Linux process and system management is a very important part that should be learned at any cost as a DevOps professional. Rasel wanted to explore all these topics and did so.

* * *

## Linux Package Management:

In linux ecosystem, package manager helps to install, uninstall, update and remove software. From the high level linux package manager can be 2 type. They are:

1.  **.DEB** based (DPKG/APT/APT-GET): Ubuntu, Debian, linux Mint
2.  **.RPM** based (YUM): Red hat enterprise linux, Centos, Fedora

### Some important commands of .DEB based package manager are:

```bash
apt install [package name]
```
This install the the given named package.

```bash
apt update
```
This update the package list.

```bash
apt upgrade
```
This upgrade all the package in list.

```bash
apt remove [package name]
```
This remove or uninstall the given named package.

```bash
apt list
```
This gives the package list.

```bash
apt search [package name]
```
This search the given name package in the list.

Example:
```bash
apt update                # Update package list
apt install nginx         # Install nginx
apt remove nginx      # Uninstall nginx
apt upgrade               # Upgrade all packages        
```

### Some important commands of .RPM based package manager are:

```bash
yum install [package name]
```
This install the the given named package.

```bash
yum update
```
This update the package list.

```bash
yum upgrade
```
This upgrade all the package in list.

```bash
yum remove [package name]
```
This remove or uninstall the given named package.

```bash
yum repolist
```
This gives the package list.

Example:
```bash
yum update                # Update package list
yum install nginx         # Install nginx
yum remove nginx      # Uninstall nginx
yum upgrade               # Upgrade all packages        
```

* * *

## Linux User and Permission Management:

Linux prioritize the security and separation of concern by default. That's why it gives commands to create, manage user, user group and manage permission between them. By default, linux has a super user who called root user and able to perform all kinds of operation without any restriction.

### Super user command:

```bash
sudo [other commands]
```
This perform the given command as root user. Means when we add prefix sudo, then it tells linux perform super (s) user (u) do.

### Commands for create user and group:

```bash
adduser [username]
```
This creates a new user with given name.

```bash
userdel [username]
```
This delete the user with given name.

```bash
groupadd [group name]
```
This creates a group with given name.

```bash
usermod -aG [group name] [username]
```
This attach the given user into given group name.

Example:
```bash
sudo adduser devopsuser        # Add a new user
sudo userdel devopsuser        # Delete a user
sudo groupadd devopsteam       # Add a group
sudo usermod -aG devopsteam devopsuser  # Add user to group        
```

### Commands for manage file permissions:

Linux file permission has 3 kinds: Read (r), Write (w) and Execute (x). So we need to assign these 3 type of permission separately.

```bash
chmod [permissions] [file name]
```
This set permissions to the file with given name.

```bash
chown [owner]:[group] [file name]
```
This change owner and group with given name for the given named file.

Example:
```bash
ls -l file.txt # show file description with permission info
# Output: -rw-r--r-- 1 user group ...

chmod 755 script.sh            # Owner: rwx, Group: rx, Others: rx
chmod +x script.sh             # Make script executable
chown root:root file.txt       # Change owner and group        
```

* * *

## Linux System Process Management:

1.  A process is an instance of a running program. It's the active state of a program, rather than the program itself, which is a collection of instructions stored on disk.
2.  System processes are the background tasks that keep the operating system running smoothly. They include things like daemons, which provide essential services, and kernel threads, which are part of the kernel.
3.  User processes are the applications and commands that you initiate through a terminal or graphical interface.
4.  Processes can exist in various states, such as running, sleeping, stopped, or zombie, each representing a different stage of execution.

### Commands for process management:

```bash
ps aux 
```
This gives list of all process.

```bash
top
```
This works as the real-time process viewer.

```bash
htop
```
This like top but more interactive viewer. But need to install separately.

```bash
ps aux | grep [process name]
```
This list the process but only with the given process name.

```bash
kill [process id]
```
This kill the process with given id.

```bash
kill -9 [process id]
```
This forcefully kill the process with given id.

```bash
pkill [process name]
```
This kill the process with given name.

```bash
[sh file] &
```
This runs the sh or script file as background task.

```bash
jobs
```
This gives list of all background process.

```bash
fg %1
```
This bring job 1 to foreground.

Example:
```bash
ps aux                         # List all processes
top                            # Real-time process viewer
htop                           # Enhanced interactive viewer (install separately)
ps aux | grep nginx            # Find nginx processes
./script.sh &                  # Run in background
jobs                           # Show background jobs
fg %1                          # Bring job 1 to foreground        
```

* * *

## Summary:

Linux package management helps you install, update, and remove software easily using tools like **apt** or **yum**. Managing users and permissions is important for security and you can create users, groups, and set file access rights using commands like **adduser**, **chmod**, **chown**. This ensures only the right people can access or modify files. Process management lets you view and control running programs on your system using tools like **ps**, **top**, **kill**. These tools help you monitor system performance and stop unresponsive tasks.