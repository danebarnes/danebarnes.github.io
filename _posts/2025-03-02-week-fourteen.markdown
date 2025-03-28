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

The IT_Admin group was granted access to all directories, ensuring they could provide administrative oversight and support where necessary.

This exercise solidified my understanding of Active Directory group management, as well as Samba configuration and integration with AD security groups to enforce folder-level permissions. It was also a practical experience in applying least privilege principles and departmental segregation of data access—a common security best practice in enterprise environments.
