---
layout: page
title: "Project: IAP"
permalink: /project-iap/
image: "assets/images/img_smg_head.png"
---

# Virtual Network Setup

**Vector Technology Institute**
**ICT Application Project — IAP Automotives**  
**Fictitious Company Network Upgrade Simulation**

## 🛠 Project Overview

As part of the ICT Application Project for the Associate Degree in Computer Systems Technology (ACST) at Vector Technology Institute, I was part of a team tasked with designing and implementing a virtual network for a fictitious company aiming to upgrade its infrastructure.

The project involved setting up a fully functional Windows domain environment, complete with servers, client machines, DNS, DHCP, web services, email, file sharing, and directory services. This setup was virtualized using **VMware Workstation Player 17**.

---

## 🧠 Project Objectives

- Implement a Windows-based domain environment
- Use a Linux-based file server for shared resources
- Configure DNS, DHCP, and ADDS on a domain controller
- Create web and intranet servers with custom URLs
- Set up a secure mail server using Exchange 2016
- Enable central authentication and group-based file sharing
- Simulate a real-world corporate network environment

---

## 🖥️ Server and Client Configuration

| **Device Name** | **Function**                      | **Operating System**   | **IP Address**  |
| --------------- | --------------------------------- | ---------------------- | --------------- |
| IAP-DC01        | Domain Controller (AD, DNS, DHCP) | Windows Server 2012 R2 | 192.168.100.100 |
| IAP-FILESERVER  | File Server                       | Ubuntu Server 22.04.5  | 192.168.100.101 |
| IAP-MAIL        | Mail Server (Exchange)            | Windows Server 2012 R2 | 192.168.100.102 |
| IAP-INTRA01     | Intranet Server                   | Windows Server 2012 R2 | 192.168.100.103 |
| IAP-WEB         | Public Web Server                 | Windows Server 2012 R2 | 192.168.100.104 |
| IAP01, IAP02    | Client Machines                   | Windows 10             | DHCP (Dynamic)  |

![Domain Controller]({{ site.baseurl }}/assets/images/img_dc.png "Server Manager on Domain Controller")
Server Manager on Domain Controller

---

## 🌐 Domain and Directory Services

- **Domain Name**: `iap.local`
- **Active Directory OU Created**: `IAP Users`
- **User Policy**: Password change required at first login
- **Security Groups Created**:
  - Finance
  - HR
  - IT_Admin
  - Sales

![Active Directory OU]({{ site.baseurl }}/assets/images/img_ou.png "IAP Organizational Unit")
IAP Organizational Unit

---

## 💻 DHCP & DNS Configuration

- **DHCP IP Range**: `192.168.100.100 - 192.168.100.200`
- **Excluded IPs**: `192.168.100.100 - 192.168.100.105` (reserved for servers)
- **DNS Forward Lookup Zones**:
  - `iap.local`
  - `iap.com` for custom web server URL resolution

![DHCP Scope]({{ site.baseurl }}/assets/images/img_dhcp_scope.png "DHCP Scope")
DHCP Scope

![DNS Zones]({{ site.baseurl }}/assets/images/img_dns_zones.png "DNS Zones")
DNS Zones

---

## 📧 Mail Server (Exchange Server 2016)

- **Mail Server**: `IAP-MAIL`
- **Platform**: Microsoft Exchange Server 2016
- **Functionality**: Fully functional internal mail routing, mailbox creation via Exchange Admin Center

<figure style="max-width: 100%; height: auto; text-align: center;">
    <video style="width: 100%; height: auto;" controls>
        <source src="{{ '/assets/videos/demo_email.mp4' | relative_url }}" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <figcaption>Demonstration of email functionality using Outlook Web App (OWA).</figcaption>
</figure>

---

## 🌍 Web and Intranet Services

- **Web Server URL**: `www.iap.com`
- **Intranet URL**: `intranet.iap.local`
- Hosted via IIS on Windows Server 2012 R2
- Configured in DNS for domain-based access

![Web Page]({{ site.baseurl }}/assets/images/img_website.png "IAP Public Web Page")
IAP Public Web Page

![Intranet]({{ site.baseurl }}/assets/images/img_intranet.png "IAP Intranet")
IAP Intranet

---

## 🗂 File Server and Shared Drives

- **OS**: Ubuntu Server 22.04.5
- **Hostname**: `IAP-FILESERVER`
- **Samba Installed**: For Windows-compatible file sharing
- **Active Directory Integration**: Linux joined to Windows domain
- **Shared Folders**:
  - HR
  - Finance
  - Sales
  - Public (accessible to all domain users)

```
[global]
    security = ads
    server role = member server

    log file = /var/log/samba/%m.log
    log level = 1

    winbind enum users = no
    winbind enum groups = no
    winbind use default domain = no
    winbind refresh tickets = yes
    winbind offline logon = yes

    dns forwarder = 192.168.100.100

    idmap config * : backend = tdb
    idmap config * : range = 10000-999999
    idmap config IAP : backend = rid
    idmap config IAP : range = 2000000-2999999
    kerberos method = secrets and keytab
    realm = IAP.LOCAL
    workgroup = IAP
    template shell = /bin/bash

[public]
    path = /srv/iap/public
    browseable = yes
    writable = yes
    guest ok = no
    create mask = 0664
    directory mask = 0775
    valid users = @"IAP\domain users"
    force group = "IAP\domain users"

[HR]
    path = /srv/iap/hr
    browseable = yes
    writable = yes
    create mask = 0770
    directory mask = 0770
    valid users = @"IAP\HR" @"IAP\IT_Admin"

[Finance]
    path = /srv/iap/finance
    browseable = yes
    writable = yes
    create mask = 0770
    directory mask = 0770
    valid users = @"IAP\Finance" @"IAP\IT_Admin"

[Sales]
    path = /srv/iap/sales
    browseable = yes
    writable = yes
    create mask = 0770
    directory mask = 0770
    valid users = @"IAP\Sales" @"IAP\IT_Admin"
```

![Shared Drives]({{ site.baseurl }}/assets/images/img_shared_drives.png "Shared Drives")
Shared Drives

---

## 🧪 Testing & Results

- All devices joined the domain `iap.local`
- Login and Group Policy functionality worked as expected
- Web and Intranet URLs resolved correctly
- Email routing functioned internally
- File server permissions aligned with AD security groups

---

## 📌 Conclusion

This project provided a hands-on experience with real-world IT infrastructure design and implementation. It strengthened my understanding of Windows Server, Linux integration, network services, and domain management — all of which are crucial for a future career in IT systems administration or network engineering.

---

**[← Back to Portfolio](/)**
