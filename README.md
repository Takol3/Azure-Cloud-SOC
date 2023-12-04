# Building a SOC + Honeynet in Azure (Live Traffic)
![Overlay](https://github.com/Takol3/Azure-Cloud-SOC/assets/152481497/b093b7b4-54d6-424c-9d74-6cec84df11f5)
 

## Introduction

In this advanced cybersecurity initiative, I have orchestrated the development and deployment of a sophisticated mini honeynet within the Azure cloud environment. This project involved a strategic integration of diverse log sources into a centralized Log Analytics workspace. The pivotal utilization of Microsoft Sentinel in this framework has enabled the creation of dynamic attack maps, the efficient triggering of security alerts, and the formulation of comprehensive security incidents.

A crucial aspect of this project was the meticulous evaluation of various security metrics over a 24-hour period in an initially unsecured environment. Subsequent to this assessment, I implemented a series of robust security controls aimed at fortifying the system's defenses. Another round of metric analysis was conducted post-hardening for a comparative 24-hour duration. The results of these analyses are presented herein.

The metrics showcased in this study encompass a broad spectrum of security indicators, including:

- SecurityEvent: This metric reflects the data captured from Windows Event Logs, providing insights into the activities and potential vulnerabilities within the Windows operating system environment.
- Syslog: Representing Linux Event Logs, this metric offers a comprehensive overview of the events and anomalies detected in Linux-based systems.
- SecurityAlert: Derived from Log Analytics Alerts, this metric highlights the triggered alerts that signify potential security threats or breaches.
- SecurityIncident: These metrics are generated by Sentinel and represent the incidents that have been identified and cataloged, underscoring the efficacy of the Sentinel system in real-time threat detection and management.
- AzureNetworkAnalytics_CL: A critical metric indicating the malicious network flows permitted within our honeynet, providing invaluable data on potential external threats and intrusion attempts.

This project represents a significant stride in the realm of cybersecurity, demonstrating an innovative approach to threat detection, system hardening, and security analytics in a cloud-based environment.


## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet, expertly crafted within the Azure ecosystem, comprises a robust and intricately designed array of components, each serving a critical role in ensuring the integrity and security of the network. This state-of-the-art architecture includes:

- Virtual Network (VNet): The foundational backbone of the honeynet, the VNet serves as the primary conduit for internal network communications and external connectivity.
- Network Security Group (NSG): A pivotal component, the NSG acts as a firewall for virtual network resources, regulating inbound and outbound network traffic according to specified security rules.
- Virtual Machines: The honeynet features a trio of virtual machines, including two Windows-based and one Linux-based, each serving as a potential target for simulated attacks.
- Log Analytics Workspace: This component functions as a centralized repository for collecting, analyzing, and interpreting log data, crucial for identifying and responding to potential security incidents.
- Azure Key Vault: A secure module for managing cryptographic keys, secrets, and other sensitive information, ensuring robust security and compliance.
- Azure Storage Account: This element provides highly available, secure, and scalable cloud storage, essential for maintaining data integrity and accessibility.
- Microsoft Sentinel: A cutting-edge security information and event management (SIEM) system, Sentinel plays a crucial role in threat detection, response, and infrastructure protection.

Pre-Security Hardening Metrics ("BEFORE"):
Initially, the honeynet's resources were deployed with full exposure to the internet. The virtual machines, operating with fully open Network Security Groups and disabled built-in firewalls, presented an intentionally vulnerable profile. Additionally, all other resources were deployed with public endpoints, rendering them directly accessible from the internet – a scenario devoid of any use of Private Endpoints, to simulate a high-risk environment.

Post-Security Hardening Metrics ("AFTER"):
In the subsequent phase, a comprehensive hardening strategy was employed. Network Security Groups were meticulously configured to block all traffic, with the sole exception of a designated admin workstation, significantly enhancing the security posture. Additionally, all resources were fortified with their built-in firewalls and the strategic implementation of Private Endpoints, thereby establishing a robust, secure network environment resistant to unauthorized access and potential threats.


## Attack Maps Before Hardening / Security Controls
![Before -windows-rdp-auth-fail](https://github.com/Takol3/Azure-Cloud-SOC/assets/152481497/5283c09b-04e0-4838-9be9-7e3e75e5993e)
<br>
![Before -nsg-malicious-allowed-in](https://github.com/Takol3/Azure-Cloud-SOC/assets/152481497/30dd41be-558e-4dd4-8388-57e11006e9ff)
<br>
![Before -linux-ssh-auth-fail](https://github.com/Takol3/Azure-Cloud-SOC/assets/152481497/ff7bcd8a-9050-4127-a2e8-a8c0d3bedfcb)
<br>


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-11-30T20:28:21.6191213Z
Stop Time 2023-12-01T20:28:21.6191213Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8831
| Syslog                   | 233
| SecurityAlert            | 1
| SecurityIncident         | 133
| AzureNetworkAnalytics_CL | 0

## Attack Maps After Hardening / Security Controls
![After -windows-rdp-auth-fail](https://github.com/Takol3/Azure-Cloud-SOC/assets/152481497/7f65e259-a8d8-4734-bd31-70b18a71568c)
![After -linux-ssh-auth-fail](https://github.com/Takol3/Azure-Cloud-SOC/assets/152481497/69688445-cf81-40fe-b4cb-b5b95bb4331a)


```The rest of the map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 12/3/2023 5:29:46
Stop Time	12/4/2023 5:29:46

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4
| Syslog                   | 12
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

The culmination of this project marks a significant milestone in the realm of cybersecurity within the cloud computing environment. A sophisticated mini honeynet was meticulously constructed within Microsoft Azure, exemplifying the integration of multiple log sources into a Log Analytics workspace. This initiative was further enhanced by the strategic deployment of Microsoft Sentinel, which played a pivotal role in the generation of alerts and the creation of incidents, derived from the diligently ingested log data.

A critical element of this project was the comparative analysis of security metrics, conducted in two distinct phases. The initial phase involved measuring these metrics in an environment deliberately left insecure, followed by a subsequent phase where the environment was fortified with robust security controls. The results were telling: a significant reduction in the number of security events and incidents was observed post-implementation of these controls, underscoring their effectiveness in enhancing the security posture of the network.

An important observation to consider is the potential impact of regular user activity within the network. Had the network resources been subject to extensive utilization by regular users, it is conceivable that a greater number of security events and alerts might have been generated in the 24-hour period following the implementation of the security measures. This insight underscores the dynamic nature of cybersecurity, where user interaction plays a crucial role in shaping the security landscape. 

In conclusion, this project not only demonstrates the efficacy of well-implemented security controls in a cloud environment but also highlights the importance of continuous monitoring and adaptation in response to user activity and evolving threat landscapes.

