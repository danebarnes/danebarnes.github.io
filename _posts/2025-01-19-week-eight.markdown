---
layout: post
title: "Setting Up Windows Server 2012 R2 - DNS & DHCP"
date: 2025-01-19
---

In Week 8, I continued configuring IAP-DC01, the Windows Server 2012 virtual machine serving as the domain controller for iap.local, by setting up two key network roles: DNS and DHCP.

The DNS role was already installed during the Active Directory setup. To verify its functionality, I created a Windows 10 client VM, connected it to the same network, and configured it to automatically obtain an IP address via DHCP. Once online, I used the `nslookup` command to test DNS resolution. Commands like `nslookup iap.local` confirmed that the server could resolve the domain name (forward lookup), and querying the server’s IP address returned the correct hostname (reverse lookup), validating that both forward and reverse zones were working as expected.

Next, I configured the DHCP role on the same server. I created a scope with a distribution range from 192.168.100.100 to 192.168.100.200, and set an exclusion range from 192.168.100.100 to 192.168.100.105 to reserve IPs for servers and infrastructure devices. After authorizing the DHCP server in Active Directory and activating the scope, I rebooted the Windows 10 client. It automatically received an IP address from the scope and the correct DNS and gateway settings.

There was an initial issue when attempting to join the client to the domain—the domain controller wasn’t found. I confirmed the IP configuration was correct, then flushed the DNS cache using `ipconfig /flushdns` and restarted the client. After this, the domain join to iap.local was successful.

This week gave me practical experience in DNS and DHCP configuration, nslookup diagnostics, and resolving domain connectivity issues, which are foundational skills in managing Windows-based networks.
