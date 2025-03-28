---
layout: post
title: "Enabling Remote Access on Windows Server 2012 R2"
date: 2025-03-22
---

Today, I successfully enabled Remote Desktop (RDP) on the domain controller, IAP-DC01, to facilitate remote management. I accessed the domain controller directly and used Server Manager under the Local Server section to enable RDP.

Under the local server section, I located the Remote Desktop option, which was initially set to Disabled, and configured it to allow remote connections. For added security, I ensured that the option Allow connections only from computers running Remote Desktop with Network Level Authentication was enabled. After making these changes, I saved the configuration by clicking Apply and OK.

To address potential connectivity issues related to Windows Firewall, I navigated to System and Security > Windows Firewall settings on IAP-DC01 and selected Allow an app or feature through Windows Firewall. I enabled Remote Desktop by checking both the Private and Public options, ensuring the necessary firewall rules were in place.

After completing the setup on the domain controller, I transitioned to a virtual Windows 10 client to test the RDP connection. Before connecting, I used Group Policy Editor on the client machine to ensure compatibility. I pressed Win + R, typed gpedit.msc, and navigated to Computer Configuration → Administrative Templates → System → Credentials Delegation. I enabled the policy Encryption Oracle Remediation, set the protection level to Vulnerable, applied the settings, and ran in Command Prompt to update the policy.

Finally, I tested the RDP connection from the Windows 10 client. Using the Remote Desktop Connection (mstsc) tool, I entered the server's IP address, 192.168.100.212, along with the administrator credentials in the format IAP\Administrator. The connection was successful, confirming that RDP was correctly enabled and functional on IAP-DC01.

<figure>
    <video width="640" height="360" controls>
        <source src="{{ '/assets/videos/demo_remote.mp4' | relative_url }}" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <figcaption>Demonstration of Remote Desktop.</figcaption>
</figure>

This process not only facilitated remote management of the server but also emphasized the importance of integrating security best practices, such as enabling Network Level Authentication and ensuring compatibility through group policy configuration. Following structured procedures for setup and testing proved to be an effective approach
