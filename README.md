## Cloning TekTutor Openshift Training Repository (RPS Cloud Linux Machine Terminal )
```
cd ~
git clone https://github.com/tektutor/openshift-tekton-june2024.git
cd openshift-3june-2024
```

## About our lab environment
- OnPrem - Production grade Red Hat OpenShift setup 
- System Configuration
  - 89 virtual CPU cores
  - 755 GB RAM
  - 17 TB HDD Storage
- CentOS 7.9.2009 64-bit OS
- KVM Hypervisor
- 7 Virtual machines
  - Master 1 with RHEL Core OS ( 16 Cores, 128GB RAM, 500 GB HDD )
  - Master 2 with RHEL Core OS ( 16 Cores, 128GB RAM, 500 GB HDD )
  - Master 3 with RHEL Core OS ( 16 Cores, 128GB RAM, 500 GB HDD )
  - Worker 1 with RHEL Core OS ( 8 Cores, 128GB RAM, 500 GB HDD )
  - Worker 2 with RHEL Core OS ( 8 Cores, 128GB RAM, 500 GB HDD )
  - HAProxy Load Balancer Virtual Machine
  - One more VM is created and destroyed during Openshift installation (BootStrap Virtual Machine)
- Linux Server 1 ( 192.168.1.22 ) - Openshift cluster 1 ( 7 participants - user01 thru user07 )
- Linux Server 2 ( 192.168.1.23 ) - Openshift cluster 2 ( 7 participants - user08 thru user14 )
- Linux Server 3 ( 192.168.1.24 ) - openshift cluster 3 ( 7 participants - user15 thru user21 )
