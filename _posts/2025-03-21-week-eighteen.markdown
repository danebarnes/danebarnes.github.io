---
layout: post
title: "Installing Exchange Server 2016 & Deploying IIS-Based Web Services"
date: 2025-03-21
---

Following previous challenges with installing Microsoft Exchange Server 2016, this week I successfully deployed the server on a different host machine—my assigned work laptop—which had sufficient RAM to meet the system requirements. With the upgraded hardware, installation was completed without issues. To streamline the process and avoid the repetitive manual configuration from earlier attempts, I created a PowerShell script to automate the installation of several Exchange prerequisites. The script is included below:

```
# Function to log output
function Log {
    param ([string]$Message)
    $Timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    $LogMessage = "$Timestamp : $Message"
    Add-Content -Path "C:\Temp\InstallFeaturesLog.txt" -Value $LogMessage
    Write-Output $LogMessage
}

# List of commands to run
$Commands = @(
    "Install-WindowsFeature RPC-over-HTTP-proxy",
    "Install-WindowsFeature RSAT-Clustering",
    "Install-WindowsFeature RSAT-Clustering-CmdInterface",
    "Install-WindowsFeature RSAT-Clustering-Mgmt",
    "Install-WindowsFeature RSAT-Clustering-PowerShell",
    "Install-WindowsFeature WAS-Process-Model",
    "Install-WindowsFeature Web-Asp-Net45",
    "Install-WindowsFeature Web-Basic-Auth",
    "Install-WindowsFeature Web-Client-Auth",
    "Install-WindowsFeature Web-Digest-Auth",
    "Install-WindowsFeature Web-Dir-Browsing",
    "Install-WindowsFeature Web-Dyn-Compression",
    "Install-WindowsFeature Web-Http-Errors",
    "Install-WindowsFeature Web-Http-Logging",
    "Install-WindowsFeature Web-Http-Redirect",
    "Install-WindowsFeature Web-Http-Tracing",
    "Install-WindowsFeature Web-ISAPI-Ext",
    "Install-WindowsFeature Web-ISAPI-Filter",
    "Install-WindowsFeature Web-Lgcy-Mgmt-Console",
    "Install-WindowsFeature Web-Metabase",
    "Install-WindowsFeature Web-Mgmt-Console",
    "Install-WindowsFeature Web-Mgmt-Service",
    "Install-WindowsFeature Web-Net-Ext45",
    "Install-WindowsFeature Web-Request-Monitor",
    "Install-WindowsFeature Web-Server",
    "Install-WindowsFeature Web-Stat-Compression",
    "Install-WindowsFeature Web-Static-Content",
    "Install-WindowsFeature Web-Windows-Auth",
    "Install-WindowsFeature Web-WMI",
    "Install-WindowsFeature Windows-Identity-Foundation",
    "Install-WindowsFeature RSAT-ADDS"
)

# Execute each command
foreach ($Command in $Commands) {
    Log "Starting: $Command"
    try {
        Invoke-Expression $Command
        Log "Successfully executed: $Command"
    } catch {
        $ErrorMessage = $_.Exception.Message
        Log "Failed to execute $Command. Error: $ErrorMessage"
    }
}
Log "Script completed. Check the log file for details."
```

This made the setup more efficient and repeatable. After completing the server setup, I accessed the Exchange Admin Center to create mailboxes for users who had been previously created in Active Directory (AD). Once the mailboxes were configured, I tested the functionality by using Outlook Web App (OWA) to send and receive emails between two domain-joined user accounts on a client machine. The successful exchange of emails confirmed that the integration was fully operational.
In addition to Exchange, I installed and configured Microsoft IIS (Internet Information Services) on two separate servers—one for the internal intranet and the other for the public-facing website. This was done to simulate a real-world network architecture, with clear segmentation for improved security. The intranet server was assigned the IP 192.168.100.103, and the external web server used 192.168.100.104.

To ensure proper name resolution, custom DNS entries were created on the Domain Controller (DC). A new Forward Lookup Zone named iap.com was created for the external website, and a Host (A) record for www.iap.com was added, pointing to 192.168.100.104 with a corresponding PTR record. For the intranet, a Host (A) record named intranet.iap.local was added under the existing iap.local zone, pointing to 192.168.100.103. These configurations allowed users to access services seamlessly using standard and easy-to-remember URLs.

With these DNS configurations in place and mailboxes set up, users on the domain could now access web and intranet services via the appropriate URLs—www.iap.com for the public website and intranet.iap.local for the internal portal. This enhanced usability and mirrored real-world enterprise environments.
