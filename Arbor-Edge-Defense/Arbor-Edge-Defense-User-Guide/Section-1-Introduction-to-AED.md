# Section 1: Introduction to AED

## Table of contents

- [Section 1: Introduction to AED](#section-1-introduction-to-aed)
  - [Table of contents](#table-of-contents)
  - [About AED](#about-aed)
    - [Key features](#key-features)
    - [Focus on the customer edge](#focus-on-the-customer-edge)
    - [Application availability](#application-availability)
    - [Immediate protection](#immediate-protection)
    - [Complete DDoS protection](#complete-ddos-protection)
    - [Advanced DDoS blocking](#advanced-ddos-blocking)
    - [Prevention of volumetric DDoS attacks](#prevention-of-volumetric-ddos-attacks)
    - [Prevention of emerging botnet and application-layer attacks](#prevention-of-emerging-botnet-and-application-layer-attacks)
    - [Traffic forensics and reporting](#traffic-forensics-and-reporting)
  - [What You Can Do with AED](#what-you-can-do-with-aed)
    - [Key Task](#key-task)
  - [About the AED Appliance](#about-the-aed-appliance)
    - [Deployment best practices](#deployment-best-practices)
  - [View System Information](#view-system-information)
    - [Viewing the system information for an AED device](#viewing-the-system-information-for-an-aed-device)
    - [About the throughput information on the About page](#about-the-throughput-information-on-the-about-page)
    - [Viewing license limit alerts](#viewing-license-limit-alerts)
  - [About the AED User Interfaces](#about-the-aed-user-interfaces)
    - [About the UI](#about-the-ui)
    - [About the CLI](#about-the-cli)
  - [Using the AED API](#using-the-aed-api)
    - [How to view the AED API documentation](#how-to-view-the-aed-api-documentation)
    - [Generating an API token](#generating-an-api-token)


## About AED

- Secures the internet data center edge from threats against availability  (application-layer, DDoS attacks,..)

### Key features

- Focuses on the customer edge
- Ensures application availability
- Provides immediate protection from threats
- Provides complete DDoS protection within a single user interface.
- Provides advanced DDoS blocking.
- Prevents volumetric DDoS attacks by signaling upstream ISPs (Internet Service
- Providers) and MSSPs (Managed Security Service Providers)
- Prevents emerging botnet and application-layer attacks.
- Provides real-time and historical traffic forensics and reports

### Focus on the customer edge

- AED has complete visibility into packet-level data.
- Deploying close to the customer edge => AED can focus on newer and better detection methods without performance constraints of the service provider level
- Allow AED to detect and block the low-bandwidth attacks that target the enterprise infrastructure

### Application availability

- The users of data center and cloud services expect those services to be highly available 

### Immediate protection

- Just need a minium amount of initial setup to AED can monitor and mitigate your network traffic immediately
- No learning period is required for  effective protection 

### Complete DDoS protection

- Providing both customer-edge mitigation of application-layer attacks an upstream mitigation of volumetric attacks.

### Advanced DDoS blocking

- Include TCP stack attacks, host or pipe flooding, fragmentation attacks, resource exhaustion, connection state attacks, botnet attacks, and vulnerability exploits
- Can customize settings to provide more directed protection for specific groups of hosts.

### Prevention of volumetric DDoS attacks

- Cloud Signaling:
  - When attacks traffic exceeds a specified threshold, AED can request and receive cloud-based mitigation of volumetric attacks in real time from an upstream cloud service provider

### Prevention of emerging botnet and application-layer attacks

- Use AIF (ATLAS Intelligence Feed) to detect and stop emerging threats against the data center's infrastructure and services

### Traffic forensics and reporting

- AED reports traffic statistics in real time (both at summary level abd details levels)

## What You Can Do with AED

### Key Task

- Automatically protect against attacks by using behavior-based protection setting
- Automatically protect againse by using signature-based protection settings
- Protect a specific host or group of host 
- Refine the protection settings
- Automate specific settings 
- Monitor the systems's operations
- Mitigate an attack
- Adjust the level of protection when traffic is normal and when you are under attack
- Signal to a cloud service provider for help with mitigating volumetric attacks
- View information about your network's traffic
- Use third-party monitoring systems to poll AED for management information
- Extend AED functionality for your own use
- Manage multiple AED devices from AEM

## About the AED Appliance

- Deploy at ingress points to detect, block and report on key categories of DDoS Attacks
- Able to bypass: can configure AED to fail open (bypass) or fail closed (disconnect) if a power failure, hardware failure, or software failure occurs.
  - By default, hardware bypass is set to fail open and software bypass is enabled
- Available in several models and license options
  - `License Options` determine the throughput limit for AED

### Deployment best practices

- Deploy at the data center's premises, on the internet edge of the data center's network
- Ensure that the AED is external to all of the additional security devices (firewall, IPS, level balancing systems)- Deploy in an inline deployment without associating an IP address with either the inbound interface or the outbound interface
- Deploy the AED appliance inline or out-of-line through a span port or network tap (monitor mode)
  - Inline mode: Monitors and mitigates the traffic
  - Monitor mode: Use to a trial implementation or for monitoring purposes
- Deploy upstream or downstream from the router
- To ensure Cloud Signaling: Provide a separate, out-of-band management network between the data center and the could service provider.


## View System Information

### Viewing the system information for an AED device

- Page `About` 
  - `System Information`: 
    - Through limit, installed software, hardware
    - Model number, serial number, license expiration date
  - `License`
  - `Associated licenses`
  - `GPL based software licenses`: click the **arbor-support@netscout.com** link to email a request for copies of additional licenses that are based on the General Public License (GPL)

### About the throughput information on the About page

- `Throughput for Clean Traffic`: 
  - Graph - the amount of clean traffic that AED forwarded over the previous week

### Viewing license limit alerts

- If the amount of clean traffic that AED forwards exceeds 90 percent of its license limit, then alerts appear on the Summary page and System Alerts page

## About the AED User Interfaces

### About the UI

- Provides a web view of AED
- Can use to configure system settings, view reports, and detect and mitigate attacks
- Uses a self signed SSL certificate for connections to the UI
- Can upload a custom certificate and its certificate authority (CA) file

### About the CLI

- Can enter commands and navigate through the directories on the AED appliance
- Use to install and upgrade the software and to complete the initial configuration


## Using the AED API

- Allow to access AED functionality and extend it for your own use
- Included with the AED appliance

### How to view the AED API documentation

`https://IP_address_of_your_AED/api/aed/doc/v3/endpoints.html`

### Generating an API token

- `Token-based authentication`: mus include `X-Arbux-APIToken` key and the API token 
- To generate an API token
  - Login to the CLI with administrator account
  - Enter:
    -  `/ service aaa local apitoken generate`
    -  `userName“tokenDescription”`
  - Result: `Added token: 4wtwfuxgaRyA0rGcpbTGLzKy4_j7iQmRJeTdyIBN`
  - Save: `/ config write`
  - To view the generated API token: `/ service aaa local apitoken show`


