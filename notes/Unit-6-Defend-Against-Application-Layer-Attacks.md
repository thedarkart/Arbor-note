# Unit 6: Defend Against Application Layer Attack

## Table of contents

- [Unit 6: Defend Against Application Layer Attack](#unit-6-defend-against-application-layer-attack)
  - [Table of contents](#table-of-contents)
  - [Protecting Web Servers](#protecting-web-servers)
    - [Application Attacks to Web Servers](#application-attacks-to-web-servers)
    - [Slowloris - Slow HTTP GET DDoS](#slowloris---slow-http-get-ddos)
    - [R.U.D.Y - Slow HTTP POST DDoS](#rudy---slow-http-post-ddos)
    - [Protecting Web Servers](#protecting-web-servers-1)
    - [Protection - Malformed HTTP Filtering](#protection---malformed-http-filtering)
    - [Protection - Application Misbehavior](#protection---application-misbehavior)
    - [Protection - Botnet Prevention](#protection---botnet-prevention)
    - [Botnet Prevention Options](#botnet-prevention-options)
    - [ATLAS Intelligence Feed (AIF)](#atlas-intelligence-feed-aif)
    - [AIF Policies](#aif-policies)
    - [Protection - Spoofed SYN Flood Prevention](#protection---spoofed-syn-flood-prevention)
      - [HTTP Redirect Authentication](#http-redirect-authentication)
      - [HTTP Soft Reset Authentication](#http-soft-reset-authentication)
      - [HTTP JavaScript Authentication](#http-javascript-authentication)
    - [Protection - HTTP Rate Limiting](#protection---http-rate-limiting)
    - [Web Crawlers are a Challenge](#web-crawlers-are-a-challenge)
    - [Web Crawler Support](#web-crawler-support)
    - [Web Crawler Support by Protection](#web-crawler-support-by-protection)
    - [Web Crawler Reporting](#web-crawler-reporting)
  - [Protecting SSL-Secured Services](#protecting-ssl-secured-services)
    - [SSL Protocol Attack Protection](#ssl-protocol-attack-protection)
    - [Typical SSL Implementations](#typical-ssl-implementations)
    - [DDoS Protected SSL Protocol Implementations](#ddos-protected-ssl-protocol-implementations)
    - [SSL Protocol Overview](#ssl-protocol-overview)
    - [Known Attacks: Pushdo](#known-attacks-pushdo)
    - [Known Attacks: THC-SSL-DoS](#known-attacks-thc-ssl-dos)
    - [TLS/SSL Protocol Protection](#tlsssl-protocol-protection)
    - [Protection - TLS Attack Prevention](#protection---tls-attack-prevention)
    - [TLS Attack Prevention Reporting](#tls-attack-prevention-reporting)
  - [Protecting DNS Servers](#protecting-dns-servers)
    - [DNS Threats](#dns-threats)
    - [DNS Dictionary Attack](#dns-dictionary-attack)
    - [DNS Server Protection](#dns-server-protection)
    - [Protection - Block Malformed DNS Traffic](#protection---block-malformed-dns-traffic)
    - [Protection - Block Malformed DNS Traffic (cont.)](#protection---block-malformed-dns-traffic-cont)
    - [Protection - DNS Authentication](#protection---dns-authentication)
    - [Protection - DNS Rate Limiting](#protection---dns-rate-limiting)
    - [Protection - DNS NXDomain Rate Limiting](#protection---dns-nxdomain-rate-limiting)
  - [Protecting SIP Server](#protecting-sip-server)
    - [SIP Server Protection](#sip-server-protection)
    - [Protection - Block Malformed SIP Traffic](#protection---block-malformed-sip-traffic)
    - [Protection - SIP Request Limiting](#protection---sip-request-limiting)
  - [Other Server Types And CDN/Proxy Support](#other-server-types-and-cdnproxy-support)
    - [Protecting Other Servers Types](#protecting-other-servers-types)
    - [CDN and Proxy Support](#cdn-and-proxy-support)
    - [For Sources Identified as CDN or Proxy](#for-sources-identified-as-cdn-or-proxy)

## Protecting Web Servers

### Application Attacks to Web Servers

- Get Floods
- Slow GET
- Slow POST

### Slowloris - Slow HTTP GET DDoS

- Take down a web server with minimal bandwidth and side effects on unrelated services and ports to hold open as many connections as possible to the `HTTP server`
- Abuse handling of `HTTP request headers` slowly, high impact and relatively low bandwidth usage

### R.U.D.Y - Slow HTTP POST DDoS

- Uses HTTP POST requests
- Abuses HTTP web form fields
- Iteratively injects one custom byte into a web application post field and goes to sleep

### Protecting Web Servers

- Attack Protections for HTTP traffic
- Malformed HTTP Filtering
- Application Misbehavior
- Botnet Prevention
- Spoofed SYN Flood Prevention
- HTTP Rate Limiting
- HTTP Header Regular Expression
- Web Crawler Support

### Protection - Malformed HTTP Filtering

- All HTTP requests are inspected and verified
- Traffic not matching either of the two conditions are dropped and the source is temporarily blocked
- Malformed HTTP can be used to protect against attacks that attempt to exhaust web server resources with invalid or blank HTTP requests
- Botnets commonly use this type of attack vector
- Disable 60-second blocking of HTTP Malformed packet sources
```sh
  system attributes set pkt.engine.mitigation.pgid.http_form.blacklist_enable = 0
```
- Disable 60 second blocking of HTTP Malformed packet sources by default for all protection groups
```sh
  system attributes set pkt.engine.mitigation.http_form.default_blacklist_enable = 0
```

### Protection - Application Misbehavior

- All `HTTP traffic` from a single source is inspected
- Source is temporarily blocked if `HTTP request headers` are interrupted
- Stop botnets from sending multiple small HTTP requests and terminating the connection

### Protection - Botnet Prevention

- All HTTP traffic from a single source is inspected
- Detects botnet attacks based on known botnet behaviors and on botnet signatures from ATLAS Intelligence Feed (AIF)
- Offending sources are temporarily blocked

### Botnet Prevention Options

- Checks if the `HTTP headers` are incomplete
- Checks if `HTTP request` is < 500 bytes and does not end with in indicative of a `slow HTTP attack`

### ATLAS Intelligence Feed (AIF)

- `ASERT` detects, analyzes and determines a set of policies that identifies threats
- `AIF` is almost invisible in `AED` except for active `AIF protection` while under attack
- Consist of the policies that identify threats by their traffic patterns
- By default, the `AIF` updates run automatically every 24 hours

### AIF Policies

- Contain real time `reputation-based` information such as IP Addresses,
Domain Names, Host Names, and/or URLs
- AED always tries to match all rules on risk level of rule and protection level setting
- A threat policy is a collection of the rules and actions to define a given threat

### Protection - Spoofed SYN Flood Prevention

#### HTTP Redirect Authentication

- `AED` responds to first URI request with a `302 re-direct` to a `modified URI`
- AED intercepts new connection and recognizes host has followed redirect

#### HTTP Soft Reset Authentication

- `AED` responds to HTTP client with a `302 re-direct message` to `original destination`
- `AED` intercepts new connection, recognizes host, and allows the connection through

#### HTTP JavaScript Authentication

- `AED` intercepts TCP SYN and allows HTTP client to establish a TCP connection with AED
- `AED` responds to the first GET request with a `200 status code`
- `HTTP payload` contains an HTML document with multiple `JavaScript` sections
- `AED` passes new connection through

### Protection - HTTP Rate Limiting

- The number of requests per second are compared to the configured `Request Limit threshold`
- The number of unique `HTTP objects` per second are compared to the configured `URL Limit threshold`
- Temporarily blocking if the source exceeds threshold
- Can be used to protect against flooding attacks on an `HTTP server`

### Web Crawlers are a Challenge

- Web crawlers are bots and blocking web crawlers is often unacceptable cause reduce web site visibility in search results and, consequently, and decrease in search ranking
- It is critical that web crawlers can still reach and index protected resources even when those are under attack and need protection

### Web Crawler Support

- Pass traffic from known search engines to allow
legitimate web crawling of website
- Protection group settings select whether known
web crawlers bypass some protections for
destinations within that protection group
- Single enable/disable Web Crawler setting for
each protection group protection level
- Individual search engines can be chosen
globally

### Web Crawler Support by Protection

![](https://i.ibb.co/F49jz9r/Screenshot-2023-05-20-213515.png)

### Web Crawler Reporting

`Web Crawlers` traffic widget for protection groups of Generic, Website, and DNS Server

## Protecting SSL-Secured Services

### SSL Protocol Attack Protection

- SYN Floods
- Malformed SSL Attacks
- SSL Re-negotiation Attacks
- SSL Exhaustion

### Typical SSL Implementations

![](https://i.ibb.co/Jk0YMp7/Screenshot-2023-05-20-214512.png)

### DDoS Protected SSL Protocol Implementations

![](https://i.ibb.co/h7rVJqZ/Screenshot-2023-05-20-215030.png)

### SSL Protocol Overview

- Client opens `TCP connection` to server
- SSL Handshake
- Exchange encrypted data

### Known Attacks: Pushdo

- Sends garbage packets to `port 443`
- Can quickly exhaust `CPU` on `HTTPS server`
- `TLS Attack Prevention` will flag and block `Pushdo` sources to mitigate

### Known Attacks: THC-SSL-DoS

- THC = "The Hacker's Choice"
- Designed to exhaust SSL server by constantly re-negotiating SSL encryption
- 2 modes:
  - Flood Renegotiation Requests
  - Repeatedly Connect and Disconnect
- Disable early whitelisting for `TLS Attack Prevention` to mitigate a `THC SSL attack`
```sh
  services aed protection set tls.early_whitelist server_type protection_level no
```

### TLS/SSL Protocol Protection

Provide protection from common attacks against `SSL`
- Attacks that try to force many `crypto operations` on the targeted server
- Focus on attacks against the protocol directly
- Attacks that are pre-encryption
- Do not require that we handle any private key's or do SSL offloading
- Enforce correct usage of the SSL protocol / key exchange
- Block malformed `SSL attacks` 
- Enforce specific `Algorithm Usage`

### Protection - TLS Attack Prevention

- Detects malformed and unreasonably extended TLS / SSL headers
- Detects `rate-based` and connection exhaustion attacks against TLS / SSL
- Works on both HTTPS and non-HTTP TLS / SSL
- Is a host blocking protection
- Disable early whitelisting to mitigate `THC SSL attack`
- SSL Message Validation
- Slow Attack Protection
- Handshake Validation
- Connection Flooding Protection
- Prevention limits get more severe with higher protection levels

### TLS Attack Prevention Reporting

Attack details show breakdown of specific TLS / SSL violations

## Protecting DNS Servers

### DNS Threats

- DNS whose impacts include loss of service availability, reduced customer satisfaction, and hurt profitability
- Types of attacks
  - Client-Side Attacks
  - Server-Side Reflective Attacks
  - DNS cache Poisoning Attacks
  - DNS Application Layer Attacks

### DNS Dictionary Attack

Attacker requests entries that do not exist in the `DNS Cache` to make database Server overwhelmed with lookups

### DNS Server Protection

- Protect `DNS Servers` and services with:
  - Block Malformed DNS Traffic
  - DNS Authentication
  - DNS Rate Limiting
  - DNS NXDomain Rate Limiting
  - DNS Regular Expression
- All DNS preventions apply on `UDP/53`, DNS Malformed, DNS Rate Limiting, DNS NXDomain Rate Limiting, DNS Regular Expression can also work on `TCP/53`

### Protection - Block Malformed DNS Traffic

- Traffic with a destination port of `UDP/53` is inspected
- Packets are dropped but sources are blocked

### Protection - Block Malformed DNS Traffic (cont.)

- The Block Malformed `DNS Traffic` protection will ignore the `EDNS version` and `Z flag` value of the packet
- These fields cannot be used as attack vectors
- AED will allow all `EDNS version` and `Z flag` values to pass when this protection

### Protection - DNS Authentication

- If the source does not change from a `UDP` to `TCP DNS request` the source is considered invalid
- Any unverified requests are dropped, but source hosts are not blocked
- Protects against `DNS attacks` that originate from sources that are not valid `DNS clients`

### Protection - DNS Rate Limiting

- Inspects all of the DNS traffic that originates from a single source and records the number of queries per second
- The source is temporarily blocked

Enable DNS rate limiting protection on `TCP/53`
```sh
  system attributes set pkt.engine.mitigation.dnsrate.ignore_tcp = 0
```
### Protection - DNS NXDomain Rate Limiting

- Monitor DNS response packets for sources that send requests that cause the generation of a non-existent domain (NXDomain) responses
- Any source that sends more consecutive failed DNS requests than the threshold is temporarily blocked

Enable DNS NXDomain rate limiting protection on `TCP/53`
```sh
  system attributes set pkt.engine.mitigation.dnsratenx.ignore_tcp = 0
```

## Protecting SIP Server

### SIP Server Protection

Protect VoIP (SIP) servers and services:
- Block Malformed SIP Traffic
- SIP Request Limiting

Enable SIP processing on `UDP/5060, UDP/5061, TCP/5060 and TCP/5062`

```sh
  system attributes set pkt.engine.decode.sip.tcp_ports = 5060 5062
```

### Protection - Block Malformed SIP Traffic
 
- If the headers are not properly formatted and/or do not have reasonable values
- Traffic is dropped and source is temporarily blocked

Disable 60 second blocking of `SIP Malformed packet` sources
```sh
  system attributes set pkt.engine.mitigation.ppgid sipform.blacklist_enable = 0
```

### Protection - SIP Request Limiting

Drop and the source is temporarily block If the rate of SIP requests per second exceeds the threshold

## Other Server Types And CDN/Proxy Support

### Protecting Other Servers Types

Server Types pre-configured for:
  - Mail Server
  - VPN Server
  - RLogin Server
  - File Server
  - Generic
  
`Generic Server Type` is the "catch-all" providing flexibility to accommodate specific server types

### CDN and Proxy Support

- `Proxy server` forwards traffic from many user clients or cached content from many servers
- `CDN server` forwards content 
- Special handling for sources 
- For any source host that is detected to be a `CDN or proxy server`:
  - All rate limiting protections are disabled
  - Blocking protections will not block hosts but will instead block flows
- A "flow" is traffic matching a five-tuple of:
  - Source IP address
  - Sestination IP address
  - IP protocol
  - Source `TCP/UDP` port
  - Destination `TCP/UDP` port


### For Sources Identified as CDN or Proxy

Change behavior from host blocking to flow blocking:
- DNS Malformed
- HTTP Malformed
- SIP Malformed
- SSL/TLS Attack Prevention
- HTTP Regular Expression
- Botnet Prevention
- DNS Regular Expression
- Application Misbehavior
