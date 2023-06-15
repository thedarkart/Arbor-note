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
    - [Automate Cloud-based Mitigation Requests](#automate-cloud-based-mitigation-requests)
    - [Targeted Destination Settings](#targeted-destination-settings)
    - [Configuring Proxy Server for the Handshake](#configuring-proxy-server-for-the-handshake)
    - [Cloud Signaling Configured](#cloud-signaling-configured)
    - [Cloud Signaling Handshake](#cloud-signaling-handshake)
  - [GRE Tunnel](#gre-tunnel)
    - [GRE Tunneling for Cloud Signaling](#gre-tunneling-for-cloud-signaling)
    - [Configure GRE Tunneling for Cloud Signaling](#configure-gre-tunneling-for-cloud-signaling)
    - [GRE Tunnel Termination Notes](#gre-tunnel-termination-notes)
    - [GRE Tunnel Termination Configuration](#gre-tunnel-termination-configuration)
  - [Targeted Cloud Signaling](#targeted-cloud-signaling)
    - [Targeted Destination Cloud Signaling](#targeted-destination-cloud-signaling)
    - [Automatic Targeted Cloud Signaling](#automatic-targeted-cloud-signaling)
    - [Active Cloud Signaling Requests Page](#active-cloud-signaling-requests-page)
    - [Targeted Cloud Signaling Workflow](#targeted-cloud-signaling-workflow)
  - [Manual Targeted Cloud Signaling](#manual-targeted-cloud-signaling)
    - [Manual Configuration of Targeted Prefixes](#manual-configuration-of-targeted-prefixes)
    - [Active Cloud Signaling Requests Page](#active-cloud-signaling-requests-page-1)
    - [Active Cloud Signaling Request Page Operation](#active-cloud-signaling-request-page-operation)
    - [Manual Targeted Prefix Cloud Signaling](#manual-targeted-prefix-cloud-signaling)
    - [Manual Targeted Cloud Signaling Request](#manual-targeted-cloud-signaling-request)
  - [Cloud Signal Widget](#cloud-signal-widget)
    - [Cloud Signaling Widget](#cloud-signaling-widget)
    - [Tasks to Perform with the Cloud Signaling Widget](#tasks-to-perform-with-the-cloud-signaling-widget)
    - [Manually Requesting Cloud-based Mitigation](#manually-requesting-cloud-based-mitigation)
    - [Mitigation Requested versus Mitigation Activated Status](#mitigation-requested-versus-mitigation-activated-status)
    - [Manually Deactivating Cloud-based Mitigation](#manually-deactivating-cloud-based-mitigation)
    - [Automatically Requesting Cloud-based Mitigation](#automatically-requesting-cloud-based-mitigation)
    - [Automatic Triggers - Cloud Provider Activated](#automatic-triggers---cloud-provider-activated)
    - [Cloud Mitigation Blocked Traffic Graphs](#cloud-mitigation-blocked-traffic-graphs)

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
    - Arbitrarily selects 1000 URLs from the blacklist if more than 1000 URLs

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

Checking alerts which are problems with the server

### Using Arbor Cloud?

Enable if using `Arbor Cloud DDoS Protection Server` which automatically whitelist of proxy server 

### Service Provider Management Portal

URL for Cloud service provider portal

### About Sharing Inbound Black/Whitelists

- Send the lists when it connects to the `Cloud Signaling server`
- Resend the blacklists and whitelist to the `Cloud Signaling server`
- Change are made to the either inbound black/whitelists
- Automatically resends the lists every 12 hours
- Update the lists any time sending the blacklists and whitelist

### Automate Cloud-based Mitigation Requests

- Automate cloud-based mitigation global requests 
- `bps` and `pps` threshold 
- Interval time to automatic start/stop delay timer

### Targeted Destination Settings

### Configuring Proxy Server for the Handshake

- Add the proxy server IP address or hostname and specify the port number
- The user name and the password required to access the proxy server
- Authentication can be selected if AED is unable
to detect it via the Automatic option

### Cloud Signaling Configured

- Connection status
- Cloud mitigation widget displays when last signal received

### Cloud Signaling Handshake

Connection error messages

## GRE Tunnel

### GRE Tunneling for Cloud Signaling

- Provide a destination for cleaned traffic that the provider routes back to the network
- Not re-inspect the traffic

### Configure GRE Tunneling for Cloud Signaling

- GRE tunnel endpoint must be a public IP
- No support for:
  - IPv6 GRE tunnels
  - IPv6 traffic
  - Encapsulated inside IPv4 tunnels

### GRE Tunnel Termination Notes

- Trafic is immediately forwarded to `Next Hop` 
- Not inspected by `protection groups`
- `GRE` over `LACP` is not supported
- Specify a `GRE tunnel destination` that is downstream of AED
- Cannot specify a `GRE tunnel` destination if `vAED` in `Layer 3 mode`
- Use the `IP address` of the external interface as the tunnel destination

### GRE Tunnel Termination Configuration

![](https://i.ibb.co/sqrmJq0/Screenshot-2023-05-19-084859.png)

## Targeted Cloud Signaling

### Targeted Destination Cloud Signaling

- Request `cloud-based` mitigation for any `IPv4 prefixes` on which traffic exceeds one of the specified thresholds
- Must also enable `Top Sources` and `Destinations`

### Automatic Targeted Cloud Signaling

- Start when:
  - Traffic exceeds the `Global Cloud Signal Threshold`
  - One or more `IPv4 prefixes` exceeds a targeted destination threshold
- Replace all prefixes in the global cloud mitigation with the targeted `IPv4 prefixes`

### Active Cloud Signaling Requests Page

- Targeted hosts
- Duration of `cloud-based` mitigation
- Rate which triggered mitigation
- Automatic mitigations cannot be manually removed

### Targeted Cloud Signaling Workflow

- After the attack traffic rate falls below the `25 Mbps` threshold, the mitigation stop
- AED removes the prefix and creates a change log entry

## Manual Targeted Cloud Signaling

### Manual Configuration of Targeted Prefixes

- Can add additional prefixes
- Added to the mitigation request when traffic exceeds the defined threshold

### Active Cloud Signaling Requests Page

Lists all prefixes included in a targeted `Cloud Signaling Request`

### Active Cloud Signaling Request Page Operation

Add/remove targeted IPs:
- Use commas to separate multiple entries
- Can enter one or more prefixes

### Manual Targeted Prefix Cloud Signaling

`Active Cloud Signaling Requests` page displays all prefixes that are included in a request for targeted Cloud Signaling

### Manual Targeted Cloud Signaling Request

- No active requests: AED sends a targeted prefix
request
- Active targeted request: AED adds the prefix to the
request
- Active global request: Global request must be
deactivated before AED can send a targeted request

## Cloud Signal Widget

### Cloud Signaling Widget

- Automatically updates `Cloud Signaling` status
- Provides manual control of mitigation requests

### Tasks to Perform with the Cloud Signaling Widget

- Request or stop a global cloudm mitigation 
- Request or stop mitigation for a specific IPv4 PG
- Open the Configure Cloud Signaling settings page
- Open your cloud service provider's management portal

### Manually Requesting Cloud-based Mitigation

- Automatic threshold signaling is disabled or no threshold is configured
- The attack is too large to mitigate at the data center's premises but the traffic does not exceed
the configured threshold for activating Cloud Signaling
- If an attack overloads routers that are deployed upstream of the AED, then the AED cannot detect or mitigate that attack

### Mitigation Requested versus Mitigation Activated Status

![](https://i.ibb.co/25HzK46/Screenshot-2023-05-19-100816.png)

### Manually Deactivating Cloud-based Mitigation

- Deactivate an active mitigation request, only the current request is affected
- Deactivate Cloud Signaling for a protection group, and its traffic immediately exceeds the threshold again, AED re-activates `Cloud Signaling` for that protection group
- When a mitigation is requested automatically, it stops automatically unless stop it manually first

### Automatically Requesting Cloud-based Mitigation

- Configured `Global Threshold` was exceeded
- AED initiates cloud mitigation request to `Cloud Signaling provider network`

### Automatic Triggers - Cloud Provider Activated

- An event occurred in the Cloud Provider network `Cloud Signaling Server` triggered a mitigation
Information about mitigation is important to the AED
- Traffic statistics calculated into total traffic seen for `Automatic Cloud Signaling` trigger

### Cloud Mitigation Blocked Traffic Graphs

- `Widget mini-graph` shows amount of traffic blocked by cloud mitigation
- Larger graph in pop-in supply
  - Reports `traffic bps` blocked to the AED
  - Includes bps blocked by Cloud Mitigation in traffic totals




