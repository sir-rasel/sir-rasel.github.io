---
title: "DevOps - Step By Step Learning : Part 11 (Virtualization, VM, and Automation VM Using Vagrant)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-23T00:00:00Z"
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
    image: "img/blogs/134-devops-vm.jfif"
    caption: "DevOps Vitualization"
    alt: "DevOps Vitualization"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 10:** [DevOps - Step By Step Learning : Part 10 (Linux Networking, Compression and Little Scripting for Automation)]({{< ref "blogs/133-devops-linux-networking.md" >}})
- **Part 12:** [DevOps - Step By Step Learning : Part 12 (Dissection Important Part of Vagrantfile)]({{< ref "blogs/135-devops-vagrant.md" >}})
---

{{< figure
    src="/img/blogs/134-devops-vm.jfif"
    caption="DevOps Vitualization (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel was a professional .NET (C#) developer thus an avid user of the Windows ecosystem, as we already know. He therefore dual boots his computer with Linux and Windows in order to work, study and practice Linux. However, He discovered that it was challenging and troublesome to practice and work by jumping between OSs. Furthermore, it is not a sensible method of server management. He thus explored and discovered the virtualization process. It provides appropriate isolation and helps in running different operating systems on a single machine. He then made an effort to understand how to manage virtualization in a better, simpler, and more effective manner.

* * *

## Prerequisites:

*   Install [VirtualBox](https://www.virtualbox.org) (or other providers)
*   Install [Vagrant](https://developer.hashicorp.com/vagrant)

* * *

## What is Virtualization?

**Virtualization** is the technology that lets you run multiple operating systems (like Linux, Windows) on a single physical machine by using virtual machines.

*   Think of it like running different computers inside your main computer.
*   It's powered by a software called hypervisor, which manages and runs these virtual machines.

## How Does It Work?

1.  A **hypervisor** is special software that controls virtualization. It sits between your hardware and your virtual machines. The hypervisor’s job is to divide and manage system resources like CPU, RAM, disk, and network among the VMs.
2.  A VM is a virtual computer that runs inside your real computer. Each VM has its own virtual CPU, RAM, disk, and network adapter. The hypervisor assigns a portion of your actual hardware to each VM.
3.  Each VM can run a different OS from your host (e.g., Linux VM on Windows host). You can run multiple VMs at once, each isolated and independent. The hypervisor keeps things fair: It makes sure VMs don’t interfere with each other, It handles scheduling of CPU and memory allocation.
4.  Each VM is isolated from the others and has its own IP. If one VM crashes or gets infected, the others are not affected. This is great for testing software safely.

## Types of Hypervisors:

*   Type 1 (**bare-metal**): Runs directly on hardware (e.g., VMware ESXi, Microsoft Hyper-V).
*   Type 2 (**hosted**): Runs on top of an OS (e.g., VirtualBox, VMware Workstation).

{{< figure
    src="/img/blogs/134-vm-type.png"
    caption="VM Type (Photo Credit: Tecadmin)"
    align=center
>}}

## What is a Virtual Machine (VM)?

A VM is a software-based computer with its own CPU, memory, storage, and OS.

*   You can install Ubuntu on a VM while using Windows on your real machine.
*   Each VM is isolated, so it's safe to test deployments or run services.

Example Use Cases:

*   Testing different OS environments.
*   Running server stacks (web server + DB) without affecting your main system.
*   Simulating production environments for DevOps pipelines.

{{< figure
    src="/img/blogs/134-vm-structure.png"
    caption="VM Structure (Photo Credit: SUSE)"
    align=center
>}}

So, in a single word, virtualization is a technique that allows run multiple operations systems known as guest operating system in a single machine on top of main operating system known as host operating system. And hypervisor manage, allows and conducts those communication between host and guest OS.

* * *

## Virtual Machine Manually

Manual VMs Management basically can done in 4 steps after installing the hypervisor software like Oracle VM VirtualBox:

1.  Create a virtual machine with hostname, cpu, ram, hard disk etc necessary settings.
2.  Download and install a guest operating system like Linux ubuntu or centos.
3.  Tuning the network settings like bridge network and any others settings.
4.  Start, SSH / Use, Save State and Stop as per necessary.

For more info:
- https://docs.oracle.com/cd/E26217_01/E26796/html/qs-create-vm.html
- https://www.youtube.com/watch?v=VskAnHHr3xc
- https://www.youtube.com/watch?v=nvdnQX9UkMY

* * *

## Automating VMs with Vagrant

Vagrant is a tool to automate the creation and configuration of virtual machines.

*   It works with **VirtualBox**, VMware, Hyper-V, etc.
*   It uses a **Vagrantfile** to define how the VM should be built.

### Basic Vagrant Workflow

**Step 1: Initialize a New Project**

```bash
mkdir my-vm && cd my-vm 
vagrant init ubuntu/bionic64  # Creates a default Vagrantfile        
```

**Step 2: Customize the Vagrantfile**

```bash
Vagrant.configure("2") do |config| 
    config.vm.box = "ubuntu/bionic64" # Use Ubuntu 18.04   
    config.vm.hostname = "devops-vm" 
    config.vm.network "private_network", ip: "192.168.56.10" 
    config.vm.provider "virtualbox" do |vb| 
        vb.memory = "2048" 
        vb.cpus = 2 
    end 
end        
```

**Step 3: Start the VM**

```bash
vagrant up  # Downloads the box and starts the VM
vagrant status # Check the status
vagrant box list # list of all vagrant virtual box        
```

**Step 4: Access the VM**

```bash
vagrant ssh # SSH into the virtual machine        
```

**Step 5: Stop or Destroy**

```bash
vagrant halt # Shut down the VM 
vagrant destroy # Delete the VM completely        
```

### Why Use Vagrant?

*   Automates repeatable environments (great for DevOps/testing).
*   Version control your environments via **Vagrantfile**.
*   Works on any OS, your team can all use the same setup.

* * *

## Summary:

Virtualization lets you run multiple virtual computers on one real computer with the help of a software called Hypervisor. These virtual machines (VMs) are useful for testing and development without breaking your main system. Vagrant makes it easy to create and manage VMs using code, so you can build the same environment every time, helpful for DevOps automation, testing, and consistency across teams.