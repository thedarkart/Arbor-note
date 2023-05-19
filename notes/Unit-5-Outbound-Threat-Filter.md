# Unit 5: Outbound Threat Filter

## Table of contents

- [Unit 5: Outbound Threat Filter](#unit-5-outbound-threat-filter)
  - [Table of contents](#table-of-contents)
  - [Outbound Threat Filter (OTF)](#outbound-threat-filter-otf)
  - [Details of the Outbound Threat Filter Page](#details-of-the-outbound-threat-filter-page)
  - [Update Outbound Threat Filter Configuration](#update-outbound-threat-filter-configuration)
  - [AIF Standard Categories](#aif-standard-categories)
  - [AIF Advanced Categories](#aif-advanced-categories)
  - [Confidence Index](#confidence-index)
  - [Outbound Threat Filter - STIX Feeds](#outbound-threat-filter---stix-feeds)
  - [Outbound Threat Filter — Payload Regular Expression](#outbound-threat-filter--payload-regular-expression)
  - [Outbound Threat Filter — DNS Rate Limiting](#outbound-threat-filter--dns-rate-limiting)
  - [Outbound Threat Filter — Malformed HTTP Filtering](#outbound-threat-filter--malformed-http-filtering)
  - [Summary Page Outbound ATLAS Threat Activity](#summary-page-outbound-atlas-threat-activity)

## Outbound Threat Filter (OTF)

- Prevents malicious traffic from leaving your network
- Outbound traffic not analyzed when in Monitor deployment mode
- Must be enabled for the outbound blacklist/whitelist to work
- Protect from the threats that can affect the traffic that originates 
- Protect all of the outbound traffic that flows through the `NETSCOUT AED`, such as communication with a known botnet `command-and-control`

## Details of the Outbound Threat Filter Page

- Enabled by default
- Use `Time Selector` and `Bytes and Packets buttons` to update view
- Table lists categories of protections
— Source Hosts Blocked
— Lists the five `ATLAS` threat categories

## Update Outbound Threat Filter Configuration

- Protection Mode and Protection Level
- ATLAS Intelligence Feed
- Stix Feeds
— Payload Regular Expression
- DNS Rate Limiting
- Malformed HTTP Filtering
- AIF Threat Categories blocks any outbound traffic that matches threat policies
- ATLAS Confidence Index defaults changed to 60/40/20 in version 6.0
- Recommended configure a route to 0.0.0.0/0 with a nexthop that is reachable by the extemal interface

## AIF Standard Categories

- DDoS Threats
- IP Location
- Web Crawler Identification
- Command and Control
- Malware

## AIF Advanced Categories

- Location Based Threats
- Email Threats
- Campaign and Targeted Attacks
- Mobile
- Threat Policies
- AIF Botnet Signatures
- Web Crawler Support
- IP Location data

## Confidence Index

- `ATLAS threat categories` (IP & DNS reputation) block incoming attacks based on `ASERT's Confidence Index`
- Is reflective of active malware, botnets, and campaigns in real time
- Default confidence value is recommended but can use custom value

## Outbound Threat Filter - STIX Feeds

- Enable/disable the use of `STIX indicators` of compromise (IOCs) to block outbound threat traffic
— Enabled for outbound traffic by default

## Outbound Threat Filter — Payload Regular Expression

- Prevent attacks by packets that contain unique data patterns in their payload or header
- Applies `regular expressions` to individual packets only
— Does not detect matching content that spans multiple packets

## Outbound Threat Filter — DNS Rate Limiting

- Prevent attacks from legitimate hosts who misuse `DNS requests` to flood `DNS servers`
- Maximum number of DNS queries per second that a source can send before it is blocked
- Type the maximum number of DNS queries per second that a source can send before it is
blocked

## Outbound Threat Filter — Malformed HTTP Filtering

- Protects against attacks that exhaust resources 
— Verifies that the HTTP header, entire request, consistent format
— AED blocks the request if any of these evaluations fails

## Summary Page Outbound ATLAS Threat Activity

Display the five ATLAS threat categories that blocked the most inbound traffic and outbound traffic during the last hour