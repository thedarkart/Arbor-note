# Unit 3: Layer 3, 4 Protection

## Table of contents

- [Unit 3: Layer 3, 4 Protection](#unit-3-layer-3-4-protection)
  - [Table of contents](#table-of-contents)
  - [Invalid packets category](#invalid-packets-category)
    - [Reasons](#reasons)
      - [IPv4](#ipv4)
      - [IPv6](#ipv6)
  - [Rate-based blocking](#rate-based-blocking)
  - [Payload regular expression](#payload-regular-expression)
    - [Payload regular expression](#payload-regular-expression-1)
    - [Enhanced Payload Regular Expression Control](#enhanced-payload-regular-expression-control)
    - [Payload Regular Expression Filters](#payload-regular-expression-filters)
    - [Example Payload Regular Expression](#example-payload-regular-expression)
    - [Use Packet Capture to Generate a Payload Regex](#use-packet-capture-to-generate-a-payload-regex)
    - [Add Payload Regex to Server Type](#add-payload-regex-to-server-type)
    - [Updated Server Type Payload Regex Settings](#updated-server-type-payload-regex-settings)
  - [TCP-based Floods](#tcp-based-floods)
    - [SYN Flood Attacks](#syn-flood-attacks)
    - [TCP SYN Handshake: Half-Open Connection](#tcp-syn-handshake-half-open-connection)
  - [TCP SYN Flood Detection](#tcp-syn-flood-detection)
    - [TCP SYN Flood Detection](#tcp-syn-flood-detection-1)
  - [Spoofed SYN Flood Prevention](#spoofed-syn-flood-prevention)
    - [Spoofed SYN Flood Prevention](#spoofed-syn-flood-prevention-1)
    - [Spoofed SYN Flood Prevention Automation](#spoofed-syn-flood-prevention-automation)
    - [TCP Handshake wih Spoofed SYN Flood Prevention](#tcp-handshake-wih-spoofed-syn-flood-prevention)
    - [TCP Handshake with Out-of-Sequence Authentication Selected](#tcp-handshake-with-out-of-sequence-authentication-selected)
    - [TCP Connection Limiting](#tcp-connection-limiting)
    - [TCP Connection Limiting Default Settings](#tcp-connection-limiting-default-settings)
  - [TCP Connection Reset](#tcp-connection-reset)
    - [TCP Connection Reset](#tcp-connection-reset-1)
    - [TCP Connection Reset Thresholds](#tcp-connection-reset-thresholds)
    - [TCP Connection Reset Additional Detection Criteria](#tcp-connection-reset-additional-detection-criteria)
  - [Traffic Shaping](#traffic-shaping)
    - [Protection - Traffic Shaping](#protection---traffic-shaping)
  - [TCP SYN Flood Detection](#tcp-syn-flood-detection-2)
  - [ICMP Flood Detection](#icmp-flood-detection)
    - [ICMP Flood Attack](#icmp-flood-attack)
    - [ICMP Flood Detection](#icmp-flood-detection-1)
  - [UDP Flood Detection](#udp-flood-detection)
    - [UDP Flood Attacks](#udp-flood-attacks)
    - [DNS Amplification Attacks](#dns-amplification-attacks)
    - [DNS Amplification Attack](#dns-amplification-attack)
    - [UDP Flood Detection](#udp-flood-detection-1)
  - [Fragmentation Detection](#fragmentation-detection)
    - [Fragmentation Attacks](#fragmentation-attacks)
    - [Fragment Detection](#fragment-detection)
  - [Multicast Blocking](#multicast-blocking)
    - [Protection - Multicast Blocking](#protection---multicast-blocking)
  - [Private Address Blocking](#private-address-blocking)
    - [Protection - Private Address Blocking](#protection---private-address-blocking)

## Invalid packets category

- Non-configurable, always-on
- Precedence
- Not blocking protection

### Reasons

#### IPv4

- Invalid header (malformed, checksum, short packet)
- Invalid fragmemtation (incomplete, duplicate, too long)
- Invalid protocol (short packet, flag, number)

#### IPv6

- Invalid Extension Header (duplicate, out-of-order, route type 0)
- Maximum transmission unit (MTU) violation
- Bad Options (hop-by-hop, inconsistent)
- Invalid Payload (length)

## Rate-based blocking

- Examining the bit rate and packet rate of traffic per source
- Use profile capture to identify thresholds

## Payload regular expression

### Payload regular expression

- Flexible alternative attack handling for TCP and UDP to find unique signature 
- Analyze packets to update the settings

### Enhanced Payload Regular Expression Control

Config specific ports, port ranges

### Payload Regular Expression Filters

- One per line
- Matched packet will be dropped but source host is not blocked
- Applied to individual packet only

### Example Payload Regular Expression

![](https://i.ibb.co/KjfrmKY/Screenshot-2023-05-18-202009.png)

### Use Packet Capture to Generate a Payload Regex

UDP/TCP payload begins at offset from start of IP packet – IP header (20 bytes without 
options) plus TCP (20 bytes without options) or UDP (8 bytes)

### Add Payload Regex to Server Type

- Select protection level
- Choose TCP, and UDP ports
- Select payload (contents in hex-encoded)

### Updated Server Type Payload Regex Settings

- Regular expression is a part of Payload Regular Expression filter (specificed TCP and UDP port, not auto-filled)
- Can copy regex filter for HTTP or DNS filter

## TCP-based Floods

### SYN Flood Attacks

- To exhaust the server resources
- Continuously send packets with just the SYN bit set
- Keep open connection
- `SYN packets` is small size

### TCP SYN Handshake: Half-Open Connection

![](https://i.ibb.co/pxL8vfX/Screenshot-2023-05-18-203251.png)

## TCP SYN Flood Detection

### TCP SYN Flood Detection

- The number of `SYN packets per second` exceeds the `SYN Rate`
- The `SYN ACK Delta Rate` is exceeded 
- Traffic is dropped and source is temporarily blocked

## Spoofed SYN Flood Prevention

### Spoofed SYN Flood Prevention

- Any `TCP connection attempt` will be inspected
- `TCP traffic` to other ports is not allowed through until source is authenticated
- `TCP connections` from non-authenticated sources are not allowed through but neither are the sources blocked
- Can protect against highly distributed attacks

### Spoofed SYN Flood Prevention Automation

- Can be automated
- Allow user to specify a rate above/below 

### TCP Handshake wih Spoofed SYN Flood Prevention

![](https://i.ibb.co/58TFyKs/Screenshot-2023-05-18-204224.png)

### TCP Handshake with Out-of-Sequence Authentication Selected

![](https://i.ibb.co/c2yShBf/Screenshot-2023-05-18-204351.png)

### TCP Connection Limiting

- Not block hosts
- Limit `TCP connections` from single host with system-defined threshold

### TCP Connection Limiting Default Settings

- Are different for different server types
- Block of the policy
```sh
   system attributes set pkt.engine.mitigation.ppig.connlimit.blacklist_enable = 1
```
-  Block of the policy for all protection groups
```sh
   system attributes set pkt.engine.mitigation.connlimit.default_blacklist_enable = 1
```

## TCP Connection Reset

### TCP Connection Reset

- Source host is temporarily blocked if it is over threshold
- By default only works on destination ports:
  - 80 - HTTP traffic (Web traffic)
  - 443 - HTTPS traffic (Web traffic) 
  - 25 - SMTP traffic (mail)
- Protects against the exhaustion of TCP resources when connection tables on servers are full with idle connections
- Can protect against flood, slow HTTP post and protocol attacks

### TCP Connection Reset Thresholds

- The minimum amount of data (Initial Timeout Required Data) 
- `HTTP` or `SSL/TLS` request is not sent at Minimum Request Bit Rate (token bucket with a depth of 60 seconds)
- `HTTP header` is not sent within 60 seconds
- Block any source hosts that exceed the configured number of consecutive violations
- Change time limit to allow `HTTP heade`r transmission
```sh
  system attributes set pkt.engine.mitigation.19.idle_reset.header_time = 30
```
- Compute minimum rate of `HTTP` or `SSL/TLS `request
```sh
  system attributes set pkt.engine.mitigation.19.idle_reset.rate_interval = 30
```

### TCP Connection Reset Additional Detection Criteria

- Number of seconds the AED will wait before an idle connection is reset or blocked
- Enable this protection to keep track of connections after initial state

## Traffic Shaping

### Protection - Traffic Shaping

- Limit the forwarding rate of the traffic that matches a specific filter
- Drop the packets if the packet would cause the forwarding rate to exceed the maximum rates
- Use as a last resort or when attack vector can't be isolated
- Sources are not blocked

## TCP SYN Flood Detection

- `SYN Rate` is the number of pps a source can send before it is blocked
- `SYN ACK Delta Rate` is allowable difference between the number of ACK packets and the number of `SYN packets` (Delta Rate = `SYN-ACK`) should be lower value than SYN Rate
- Block traffic which exceeds rate limit

## ICMP Flood Detection

### ICMP Flood Attack

- Continuously send `ICMP packets`
- `ICMP Reflection attack` sends an Echo Request to the (broadcast) IP 

### ICMP Flood Detection

- If the number of ICMP packets per second exceeds the ICMP Rate, offending host is temporarily blocked
- Not solve the problem for reflection attacks when the sources are highly distributed

## UDP Flood Detection

### UDP Flood Attacks

- Is stateless, a common flood attack
- Can impact infrastructure causing collateral damage cause jitter and latency, impacting other services like `VoIP`

### DNS Amplification Attacks

- DNS is the primary attack target with UDP floods with high rate of large UDP packets
- Filter List allows to deal with an UDP flood

### DNS Amplification Attack

![](https://i.ibb.co/3zKVLsz/Screenshot-2023-05-18-211757.png)

### UDP Flood Detection

- Separate thresholds for `bps` and `pps`
- `Hosts violating` a threshold during medium or high protection level are temporarily blocked
- `Hosts violating` a threshold on Iow protection level are not blocked but `UDP traffic` is policed down to the configured threshold
- Disabled by default generally except for medium and high protection levels for server type and its derivatives

## Fragmentation Detection

### Fragmentation Attacks

- Flood of IP fragments to overwhelm the victim's ability to reassemble the packets and severely reducing performance
- May also be malformed in some way
- May be a result of a network misconfiguration

### Fragment Detection

- Separate thresholds for `bps` and `pps`
- The threshold at medium or high protection level are temporarily
blocked
- The threshold at low protection level are not blocked but fragmented traffic is policed down to the configured threshold
- By default, disabled on low and enabled on medium and high protection level for all server types

## Multicast Blocking

### Protection - Multicast Blocking

- Drops all traffic sourced from or destined to multicast address space
- Disabled by default and enable only for protection groups that must not receive any multicast traffic
- Whitelist any small multicast CIDRs that are active through AED

## Private Address Blocking

### Protection - Private Address Blocking

- Protect against attacks that spoof private IP addresses
- Drops all traffic sourced from or destined to:
  - 0.0.0.0/8
  - 10.0.0.0/8
  - 127.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16