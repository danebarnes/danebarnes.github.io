---
layout: post
title: "Implementing Role-Based Access Control with Active Directory & Samba"
date: 2025-03-02
---

This week we focused on enhancing the network’s file access security through the creation and implementation of Active Directory security groups and configuring role-based access control on the Linux file server.

Using Active Directory Users and Computers (ADUC), I created four security groups under the “IAP Users” organizational unit. These groups were: HR, IT_Admin, Finance, and Sales. The respective users were added to their appropriate groups to align with their departmental roles.

On the Linux file server (iap-fileserver), I restructured the Samba file share configuration to now include four shared directories instead of just one. These included:

- public – accessible by all authenticated users

- hr – accessible only by the HR group

- finance – accessible only by the Finance group

- sales – accessible only by the Sales group

Samba configuration:

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

The IT_Admin group was granted access to all directories, ensuring they could provide administrative oversight and support where necessary.

This exercise solidified my understanding of Active Directory group management, as well as Samba configuration and integration with AD security groups to enforce folder-level permissions. It was also a practical experience in applying least privilege principles and departmental segregation of data access—a common security best practice in enterprise environments.
