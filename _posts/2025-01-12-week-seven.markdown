---
layout: post
title: "Installing Virtualization Software & Windows Server 2012"
date: 2025-01-12
---

During Week 7, I began the implementation phase of the IAP network project by setting up the virtual environment on my host machine. I selected VMware Workstation 17 Player as the virtualization software due to its lightweight interface and compatibility with Windows-based server environments.

The first virtual machine I created was the Domain Controller, running Windows Server 2012 R2. I named the VM IAP-DC01, assigned it a static IP address of 192.168.100.100, and set the default gateway to 192.168.100.1. This machine was configured to host the Active Directory Domain Services (AD DS) role and was promoted to a domain controller for the domain iap.local.

During the setup, I encountered an issue where IAP-DC01 could not access the internet after the static IP configuration. After troubleshooting the network settings, I identified that the problem was due to the virtual network adapter being set to NAT mode, which restricts external communication for VMs using custom IP settings. The issue was resolved by switching the network adapter to “Bridged” mode, allowing the virtual machine to connect directly to the physical network and successfully regain internet access.

This week provided valuable hands-on experience in domain controller deployment, IP addressing, and virtual network configuration, reinforcing how vital correct network adapter settings are in a virtualized infrastructure.
