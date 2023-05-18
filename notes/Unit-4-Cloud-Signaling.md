# Unit 4: Cloud Signaling

## Table of contents

- [Unit 4: Cloud Signaling](#unit-4-cloud-signaling)
  - [Table of contents](#table-of-contents)
  - [Cloud Signaling For DDoS Protection](#cloud-signaling-for-ddos-protection)
    - [Issue](#issue)
    - [Mitigation Attempted](#mitigation-attempted)
    - [Engaging ISP to Mitigate DDoS Attack](#engaging-isp-to-mitigate-ddos-attack)
    - [How AED and Cloud Signaling Help](#how-aed-and-cloud-signaling-help)
    - [How Cloud Signaling Works](#how-cloud-signaling-works)
    - [Types of Cloud Mitigations](#types-of-cloud-mitigations)
      - [Global](#global)
      - [Group](#group)
      - [Targeted Prefix](#targeted-prefix)
    - [Cloud Signaling Considerations](#cloud-signaling-considerations)
    - [Additional Operational Considerations](#additional-operational-considerations)
    - [How AED Communicates with Cloud Signaling Servers](#how-aed-communicates-with-cloud-signaling-servers)
    - [About Handshake Requests](#about-handshake-requests)
    - [About Heartbeat Requests](#about-heartbeat-requests)
    - [Prefix Updates](#prefix-updates)
  - [Configuring Cloud Signaling](#configuring-cloud-signaling)
    - [Enabling Cloud Signaling](#enabling-cloud-signaling)
    - [Required Cloud Signaling Settings](#required-cloud-signaling-settings)
    - [Viewing Cloud Signaling Server Status](#viewing-cloud-signaling-server-status)
    - [Using Arbor Cloud?](#using-arbor-cloud)
    - [Service Provider Management Portal](#service-provider-management-portal)
    - [About Sharing Inbound Black/Whitelists](#about-sharing-inbound-blackwhitelists)

## Cloud Signaling For DDoS Protection

### Issue

- Best to mitigate `application-layer attacks` at the customer edge with
volumetric attacks upstream (hybrid DDoS protection)
- Required to handle VOLUMETRIC attacks that exceed the Data Center's uplink bandwidth capacity

### Mitigation Attempted

- AED reporting provides details of a `Volumetric attack` towards DNS server
Mitigation attempted
- `Bandwidth usage` remains high and links are saturated with no change or drop in traffic volume
- Users continue reporting server slow or down

### Engaging ISP to Mitigate DDoS Attack

- Requests `ISP` to block attack traffic to that Targeted IP or Group
- `ISP` researches from their perspective to determine traffic characteristics associated with the attack
- `ISP` blocks the `attack traffic` from reaching the `data center`
- Service restablished to the `server / data center`
- While the attack was mitigated, it took several steps and too long of time
to restore service

### How AED and Cloud Signaling Help

- `Cloud Signaling` is the process of requesting and receiving cloud-based mitigation `of volumetric attacks` in real time from an upstream service provider
- Reduces time to mitigate `DDoS attacks`

### How Cloud Signaling Works

- The service provider mitigates the attack, and then routes the cleaned traffic back to the network
- Shares the hosts, countries, and URLs on the `inbound blacklist` and the hosts on the `inbound whitelist`

### Types of Cloud Mitigations

Not support for IPv6 trafiic

#### Global

- All IPv4 prefixes
- Manual or automatic requests

#### Group

- Specific IPv4 protection groups
- Must be supported by mitigation provider
- Manually request
  
#### Targeted Prefix

- For a targeted prefix(es)
- Must be supported by mitigation provider
- Manual or automatic requests

### Cloud Signaling Considerations

- Support mitigation connectivity to only one upstream provider at a time
- Using `GRE tunneling` to route the cleaned traffic back to the network
  
### Additional Operational Considerations

- Not support `Cloud Signaling` for `IPv6 traffic` and `FIPS mode`(Federal Information Processing Standards)
- `CIDR` (Classless Inter-Domain Routing) blocks that are mapped to the country codes may differ between AED and cloud service provider
- Not share the following items on the blacklists and the whitelist:
    - IPv6 hosts
    - Domains on the inbound blacklist
    - Items that are not assigned to `All Protection Groups`
    — Arbitrarily selects 1000 URLs from the blacklist if more than 1000 URLs

### How AED Communicates with Cloud Signaling Servers

Sending the following requests to the `Cloud Signaling servers`:
- `Handshake` - determines if group mitigation (protection groups)
- `Heartbeat` - verifies that communication channels are open
- `Prefix Update` - sends list of the `IPv4 prefixes` to `Cloud Signaling servers` if group mitigation or group and targeted mitigations supported

### About Handshake Requests

- Initiates a `SSL-based handshake` with each `Cloud Signaling server(s)`
  - TCP port 443
  - When Cloud Signaling is enabled (settings saved)
  - Every 12 hours, automatically
- 3 modes:
  - Test Connection
  - Normal Connect
  - Disconnect 
- Negotiates heartbeat parameters
- `Cloud Signaling server` provider never initiates connection to `AED`

### About Heartbeat Requests

- Exchange heartbeat messages with the `Cloud Signaling servers` every minute
- Signals mitigation state and mitigation statistics
- `Asynchronous heartbeats` sent to UDP port 7550
- Not a request-response protocol

### Prefix Updates

- `Cloud Signaling provider` supports protection group-level mitigation 
- Sends a list of the protected host prefixes to the `Cloud Signaling Server` that are associated with each of protection group
- Use HTTPS with TCP port 443

## Configuring Cloud Signaling

### Enabling Cloud Signaling

Configure `NTP server` to avoid clock-related problems that might
interfere with communications to the `Cloud Signaling servers`

### Required Cloud Signaling Settings

Required `Cloud Signaling Server` and `APS ID` information provided by the `Cloud Signaling Provider`

### Viewing Cloud Signaling Server Status

### Using Arbor Cloud?

### Service Provider Management Portal

### About Sharing Inbound Black/Whitelists