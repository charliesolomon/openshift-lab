# openshift-lab
_OpenShift 3 virtual lab_

## Goals:
- [ ] Set up a Platform as a Service (PaaS) environment on a single laptop, using a virtual network of connected virtual machines
- [ ] Demonstrate a development/deployment workflow using the PaaS environment
- [ ] Demonstrate an Operational Management feature which monitors resources in the PaaS environment and lists all applications/services deployed in containers
- [ ] Use the experience gained from this lab to create a proposed architecture that can be used to build a PaaS environment in a corporate network

## Platform:
- Dell Precision M4800 laptop, Windows 10 64bit, 32GB RAM, Intel i7 2.80GHz, ~900GB SATA HDD

## Software needed:
- VirtualBox 5.0 (virtualbox.org, free)
- RedHat Enterprise Linux 7.1 (RHEL) (redhat.com, not free... requires redhat.com account and eval or valid license)
- RedHat OpenShift Enterprise 3.0 (redhat.com, not free)

## PaaS environment set up

### Creating a base virtual machine
1. Install VirtualBox 5.0
2. Create a new RedHat 64 bit virtual machine
  - 4GB RAM
  - 2 CPU Cores
  - 20GB HDD (for OS)
  - 100GB HDD (will be used for Docker repository)
  - ![Base VM Configuration](images/base-min-setup.png)
  - 2 Network Adapters (one for internet access through host laptop, one for internal networking between multiple VMs)
  - Optional: Set up a port forwarding rule on adapter 1 for the SSH protocol (so that SSH can be used from host to guest VMs)
  - ![Base VM Adapter 2 Config](images/base-min-neta-config.png)
  - ![Base VM Adapter 1 Config](images/base-min-nat-config.png)
3. Download the RHEL 7.1 install image (iso file), attach it to the VM's optical drive and start the VM.
  - ![Base VM Attach RHEL 7.1 ISO](images/base-min-attach-rhel-install-iso.png)
4. Follow the directions on-screen to install a minimum RHEL 7.1 server.
  - Select the 20GB hard drive as the install destination
  - Select "minimum install" under software configuration (optional: if you want to include a desktop GUI or other options, select those options during install)
  - Configure the two network adapters:
    - eth0: DHCP (Automatic), uses the host's network connection for internet
    - eth1: Manual, IP=192.168.2.20, Mask=255.255.255.0, GW=192.168.2.1, No DNS, No Routing
  - Set up the root password and a user account
  - Finish the install, and reboot
  - ![Base VM First Boot](images/base-min-first-boot.png)
