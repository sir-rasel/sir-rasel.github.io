---
title: "DevOps - Step By Step Learning : Part 12 (Dissection Important Part of Vagrantfile)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-24T00:00:00Z"
tags: ["devops" , "vm", "virtualization", "vagrant"]
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
    image: "img/blogs/135-devops-vagrant.jfif"
    caption: "DevOps Vagrant"
    alt: "DevOps Vagrant"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 11:** [DevOps - Step By Step Learning : Part 11 (Virtualization, VM, and Automation VM Using Vagrant)]({{< ref "blogs/134-devops-vm-vagrant.md" >}})
---

{{< figure
    src="/img/blogs/135-devops-vagrant.jfif"
    caption="DevOps Vagrant (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel explored the virtualization and virtual machine. First he learned to create a virtual machine in a manual manner using VirtualBox, where all the machine configuration was done manually by installing a user interface. Secondly, he learned a way to create and configure virtual machines automatically using a tool called Vagrant. But now Rasel wants to earn the efficiency and understand the Vagrantfile details so that he can use it consciously, not blindly.

* * *

## What is a Vagrantfile?

A **Vagrantfile** is a Ruby-based configuration file that tells Vagrant how to set up and manage a virtual machine. It includes the box to use, network settings, resources, provisioning scripts, and more.

* * *

## Different Section of Vagrantfile with Use Case:

### Vagrant.configure("2") do |config|

*   This is the starting point and defines the Vagrant configuration version.

```bash
Vagrant.configure("2") do |config|        
```

*   Example: Use Vagrant version 2.X.X.
*   Use Case: Required for compatibility with the latest Vagrant features.

### config.vm.box + config.vm.box_version

*   Specifies which base image (box) to use for the VM. And the other indicates the box or image version.

```bash
config.vm.box = "eurolinux-vagrant/centos-stream-9"
config.vm.box_version = "9.0.48"        
```

*   Example: Use CentOS 9 Linux distro.
*   Use Case: Ensures everyone on your team uses the same OS and environment.

### config.vm.network

*   Configures networking options like port forwarding or private IPs or public IPs.

```bash
config.vm.network "private_network", ip: "192.168.56.10"
config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
config.vm.network "public_network"        
```

*   Example: Run a web server inside the VM and access it via http://localhost:8080.
*   Use Case: Simulate production networking, test APIs locally, or run multiple services.

### config.vm.provider

*   Defines VM resources like RAM, CPU, and provider-specific settings.

```bash
config.vm.provider "virtualbox" do |vb|
  vb.name = "devops_vm"
  vb.memory = "1024"
  vb.cpus = 2
end        
```

*   Example: Allocate 1 GB RAM and 2 CPU cores for performance testing.
*   Use Case: Optimize resource usage for different environments (testing, CI/CD, etc.).

### config.vm.provision

*   Automates provisioning (setup scripts), like installing packages or running commands.

```bash
config.vm.provision "shell", inline: <<-SHELL
  yum update
  yum install -y nginx
SHELL        
```

*   Example: Automatically install Nginx when the VM starts.
*   Use Case: Create repeatable environments with pre-installed tools, great for onboarding or CI.

### Synced Folders (config.vm.synced_folder)

*   Syncs a folder from your host to the VM.

```bash
config.vm.synced_folder "./app", "/home/vagrant/app"        
```

*   Example: Edit code on your host (e.g., VSCode), run it inside the VM.
*   Use Case: Live-reload web development, shared logs/configs, or test scripts.

* * *

### ✅ Full Example: Web Server Setup for Testing

```bash
Vagrant.configure("2") do |config|
  config.vm.box = "eurolinux-vagrant/centos-stream-9"
  config.vm.box_version = "9.0.48"
  
  
  config.vm.network "private_network", ip: "192.168.56.10"
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum update
    yum install -y nginx
  SHELL
end        
```

> ***Real-Life Use Case***: A DevOps engineer wants a repeatable test environment to develop and debug web applications before deploying them to production. Instead of setting it up manually each time, they use this Vagrantfile.

* * *

## Multi-VM Setup with Vagrant

We can define multiple virtual machines in a single Vagrantfile. Each VM will have its own name, configuration, and purpose. All controlled in one place using a single Vagrantfile.

Scenario: Suppose we need a setup like a web-server will be accessed a external database and the server will be accessed via a load balancer. The web-server and load balancer will be used centos but database will be used ubuntu. Also they will be used different set of resources.

```bash
Vagrant.configure("2") do |config|

  # Web Server VM
  config.vm.define "web" do |web|
    config.vm.box = "eurolinux-vagrant/centos-stream-9"
    config.vm.box_version = "9.0.48"

    web.vm.hostname = "web.local"
    web.vm.network "private_network", ip: "192.168.56.11"

    web.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 2
    end

    web.vm.provision "shell", inline: <<-SHELL
      yum update
      yum install -y nginx
    SHELL
  end

  # Database VM
  config.vm.define "db" do |db|
    db.vm.box = "ubuntu/bionic64"

    db.vm.hostname = "db.local"
    db.vm.network "private_network", ip: "192.168.56.12"

    db.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
    end

    db.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y mysql-server
    SHELL
  end

  # Load Balancer VM
  config.vm.define "lb" do |lb|
    config.vm.box = "eurolinux-vagrant/centos-stream-9"
    config.vm.box_version = "9.0.48"

    lb.vm.hostname = "lb.local"
    lb.vm.network "private_network", ip: "192.168.56.13"

    lb.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
    end

    lb.vm.provision "shell", inline: <<-SHELL
      yum update
      yum install -y haproxy
    SHELL
  end

end        
```

### How to Use This Multi-VM Setup

*   Start All VMs:

```bash
vagrant up
```

*   SSH into a Specific VM:

```bash
vagrant ssh web
vagrant ssh db
vagrant ssh lb        
```

*   Then halt and destroy

```bash
vagrant halt
vagrant destroy --force        
```

### Real-Life Use Case (DevOps Style)

As a DevOps engineer, you want to simulate a full-stack application:

*   A web server serves content.
*   A database stores user data.
*   A load balancer distributes traffic across future multiple web servers.

Using this setup:

*   You can test deployments, configurations, and load balancing.
*   You can try provisioning with Ansible or Docker later.
*   All your team members can spin up the same environment with one command.

* * *

## Summary:

A Vagrantfile is a script that tells Vagrant how to build your virtual machine. It defines which OS to use, how much RAM/CPU to give, what network settings to apply, and what software to install on create which called provisioning. It helps developers and DevOps teams automate setup so they can build and test in the same environment every time. Means no more "it works on my machine" issues!