# Day 1

## What is Hypevisor?
- virtualization technology
- we can run multiple OS on the same laptop/desktop/workstation/server
- there are 2 types of hypervisors
  - Type 1 - aka Bare Metal Hypervisors (Used in wokstation/servers )
    - Examples - VMWare vSphere/vCenter
  - Type 2 - Laptop/Desktop/Workstation
    - Examples
      - VMWare Fusion (Mac OS-X)
      - VMWare Workstation - Linux & Windows
      - Oracle VirtualBox ( Mac, Linux & Windows ) - Free
      - Parallels (Mac OS-X)
      - KVM - Opensource ( Linux )
  - heavy weight virtualization
  - each Virtual Machine has to allocated with dedicated hardware resources
    - CPU Cores 
    - RAM
    - Storage
    - Network (virtual)
    - Graphics (virtual)
  - each VM represents 1 Operating System
  
## Processor
- Processor Packaging
  1. SCM ( Single Chip Module )
  - In 1 IC only 1 Processor will be there  
  2. MCM ( Multiple Chip Module )
  - In 1 IC 2/4/8 Processors will be there

## Multi-core Processors
- Server grade Processors supports 128/256/512 CPU cores per Processor

## What is Hyperthreading?
- each Physical CPU Core supports running 2 parallel threads simultaneously
- each Physical is seen as 2 virtual core by the hypervisor software
- Examples
- Assume we have a server with 8 Processor Sockets
- Assume we have installed a MCM Processor on each Processor Socket
- Assume the MCM supports 4 Processor/IC
- Assume each Processors supports 256 CPU Cores
- Assume each Physical core supports 2 virtual cores
- Total Processors - 32 Processors
- Total Physical CPU Cores - 32 x 256 = 8192
- Total Virtual CPU Cores = 8192 x 2 = 16384 virtual Cores
  
## What is the minimal number of servers to support 1000 Virtual Machines?
1


- 
## Why do you think Developers/QA require so many virtual machines or Operating System?
- Let's assume the developing team is working a software product and source is code cross-platform
- the same product is supported in Windows, Mac and several Linux Distributions
- the same product is supported in 32/64 bit OS

## Containerization
- light weight virtualization technology
- containers running on the same servers shares the hardwares resources on the underlying host os
- containers are not Operating System
- container does not have OS Kernel
- container has one application and its dependent libraries
- application virtualization technology
- each container represents one application process
- the reason why many of us tend to compare a container with a virtual machine
  - just like virtual machine acquire one or more IP addresses, containers also gets its own dedicated IP address
  - just like virtual machine has file system, containers also has its own file system
  - just like virtual machine with linux distributions supports package managers, linux containers also has their own package managers ( apt/apt-get,rpm,yum,dnf )
