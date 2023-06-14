# Unit 1: Onboarding New Customers

## Table of contents

- [Unit 1: Onboarding New Customers](#unit-1-onboarding-new-customers)
  - [Table of contents](#table-of-contents)
  - [Continual Improving Services](#continual-improving-services)
  - [Managed Object Configuration](#managed-object-configuration)
    - [Object Type](#object-type)
    - [Configuration (Cont.)](#configuration-cont)
    - [Managed Object Match](#managed-object-match)
    - [Dynamic DNS Matching](#dynamic-dns-matching)
      - [Dynamic DNS Matching – Case A](#dynamic-dns-matching--case-a)
      - [Dynamic DNS Matching – Case B](#dynamic-dns-matching--case-b)
      - [Every Managed Object requires a boundary definition](#every-managed-object-requires-a-boundary-definition)
      - [Configuration options per Managed Object](#configuration-options-per-managed-object)
      - [Shared Host Detection Settings](#shared-host-detection-settings)
      - [User-Defined Misuse Types](#user-defined-misuse-types)
      - [Detection Exclusion for Host Detection](#detection-exclusion-for-host-detection)
      - [Profiled Router Detection](#profiled-router-detection)
      - [False Positive Monitoring](#false-positive-monitoring)
  - [Learning Mitigation](#learning-mitigation)
    - [Configuration](#configuration)
    - [Mitigation Listing](#mitigation-listing)
  - [Adding Filter Lists](#adding-filter-lists)
    - [Adding Filter Lists](#adding-filter-lists-1)
    - [Configuration](#configuration-1)
    - [Adding Filter Lists](#adding-filter-lists-2)
  - [Building Mitigation \& Templates](#building-mitigation--templates)
    - [Template Concepts](#template-concepts)
      - [Configuration](#configuration-2)
  - [Inactive TMS Mitigation](#inactive-tms-mitigation)
    - [Configuration](#configuration-3)

## Continual Improving Services

![](https://i.ibb.co/xsQk8P0/Screenshot-2023-06-13-132842.png)

## Managed Object Configuration

![](https://i.ibb.co/94z0FD3/Screenshot-2023-06-13-133141.png)

### Object Type

Choose Administrator > Monitoring > Managed Objects > Customer

### Configuration (Cont.)

`Custom Tag` - Helps searching and build grouped reports

Sightline does a longest match of the source & destination IP from the
flow with the prefixes in `BGP (Border Gateway Protocol)`

All other attributes are matched based on the prefix to source/destination IP match

### Managed Object Match

![](https://i.ibb.co/MVGCMrr/Screenshot-2023-06-13-135125.png)

- `CIDR Block` monitors traffic and detects anomalies for resources that are static
- `CIDR Group` provides detailed baselines
- `BGP Matching` monitors `BGP resources` that are dynamic
- `Peer ASNs` downstream `BGP Customers` and BGP Peers
- `Advanced Boolean Matching`: A matching expression including the other match types and the operators: and, or, not
- `ASPath Regular Expression`: A Cisco style, string based AS regular expression
- `Communities`: A regular expression including one or more BGP communities in the form of X:Y, where X represents the `AS` (autonomous system) number and Y represents a number of local significance to AS X
- `FCAP` (fault, configuration, accounting, performance) monitor specific applications, attack vectors or market verticals
- `Interfaces`: Boundary defined for `MO`( Managed Object)
- `Local ASN/SubAS`: The AS number of a sub or local AS on network
- `Application ID`: Arbor Sightline maps application ID numbers to names, descriptions, and ports that is in sync with the mapping on the `TMS`(Transcranial Magnetic Stimulation) devices
- `TMS Ports`: Arbor Sightline maps the selected port to the managed object, so traffic is into or out of the managed object
- `TMS VLANS`: The VLANs associated with a TMS device
- `Flow Filter`: A fingerprint expression used to define which flows to match on

### Dynamic DNS Matching

Requirements: 
- Sentinel License
- ISNG/vStream DNS Probe

#### Dynamic DNS Matching – Case A

- There are two managed object configured by dynamic DNS matching
- Server it will update Sightline with the DNS binding information
- Every NetFlow record that includes the IP address a.b.c.d will now be considered equal to *.ott.at domain and will be matched and binned

#### Dynamic DNS Matching – Case B

- Another client in the network tries to resolve an IP address for a resource
- Managed Object configured to match on Service IP only
- Whereas this overcomes potential overreporting it also requires that the DNS requests and DNS replies for all clients are seen by the vStream and that all these information are send to Sightline

#### Every Managed Object requires a boundary definition

`Default / Network / Global Boundary`: all interfaces that are marked as external and
represent external connectivity

`Local Boundary`: set of explicit selected interfaces where the customer is connected

Sightline can alert when Traffic towards a Managed Object exceeds or falls below a certain threshold. Traffic is measured in 5-minute intervals

Sightline uses a hierarchy in the `Host Detection Settings`

#### Configuration options per Managed Object

- Default (System defaults)
- Shared (Preferred)
  - Shared Host detection “template” for one or more MOs
  - Template can be re-used for “similar” MOs
- Custom
  - Unique MO specific settings
  - Cannot be reused

#### Shared Host Detection Settings

- `Multiple Shared Host Detection` templates can be created
- Default is the global template that is used unless configured otherwise
- Choose Administration > Detection > Shared Host Detection Settings

#### User-Defined Misuse Types

- Choose Administration > Detection > User-Defined Misuse Types
- Using `FCAP expressions`
- Automatic `UDP filter` to be used during a `TMS mitigation`

#### Detection Exclusion for Host Detection

- Exclude IP Addresses or CIDR from triggering Host Alerts
- Source (external) and Destination (internal) to the Managed Object defined Match

#### Profiled Router Detection

- Is advised for Managed Object
- With Stable and Predictable Traffic
- Matching large block of infrastructure
- Fast Flood Detection
- Thresholds automatically recalculated every 8 hours using recent traffic statistics
- Sensitivity during the first week to prevent False Positives

#### False Positive Monitoring

![](https://i.ibb.co/3BSDDCT/Screenshot-2023-06-13-150651.png)

Single target triggering the same misuse-types multiple times per day

## Learning Mitigation

![](https://i.ibb.co/x6ynKxQ/Screenshot-2023-06-13-150936.png)

### Configuration

- Choose Administration > Monitoring > Managed Objects
- Multiple Learning Mitigation can be run per MO to learn different services

### Mitigation Listing

Sightline counts all running learning mitigations toward your licensed mitigation limit

## Adding Filter Lists

![](https://i.ibb.co/xGsWYr3/Screenshot-2023-06-13-152253.png)

### Adding Filter Lists

- Black/White List: Uses FCAP expressions to identify traffic
- IP Address List: Uses CIDR blocks to allow or deny
- DNS List: Regular expressions that search for DNS queries and responses
- HTTP/URL List: Regular expressions that search HTTP queries
- IP Location: Uses GeoIP data to identify traffic from specific countries

### Configuration

- Specify filter type and enter or upload filter list elements
- IP Location filter type requires a selection from a list of Countries
- Schedule automatic updating from external sources

### Adding Filter Lists

- Choose Administration > Mitigation > Filter Lists
- There is a limit of 85.000 bytes (of FCAP expressions) for the combined size of Black/White filter list and Blacklisted Fingerprints
- The new Managed Object is using APS/AED Cloud Signaling, ensure the system will use the provided Filter Lists during a mitigation

## Building Mitigation & Templates

![](https://i.ibb.co/1XHmj7m/Screenshot-2023-06-13-153605.png)

- Mitigation templates can be assigned to multiple Managed Objects:
- TMS Group
- BGP Signalling 
- Timeout length
- Filter Lists
- Conter-measures
- Diversion Prefix

Combine global mitigation configuration
parameters with a pre-set group of IPv4 or IPv6 countermeasures that can be used to thwart an attack

### Template Concepts

- `Generic Template`: default, for most common countermeasures, quickly configure mitigations to block likely attacks as soon as possible
- `Resource-based Template`: optimized for the type resource protected that are set according to the characteristics of a particular resource to be protected
- `Attack-based Template`: optimized for a specific attack that are set according to the 
characteristics of a particular type of attack

#### Configuration

- Choose Administration > Mitigation > Templates
- Template configuration looks the same as within the mitigation configuration
   - Name: Unique and should be meaningful
   - Description: A brief
summary of its targeted use case
   - Protection Prefixes: Determine which prefixes will be diverted to TMS
   - Use Less Specific `Diversion Prefixes`
- Specify `TMS Group` that should be used when mitigating the attack
- Select `Announce Route` to permit Sightline/TMS BGP route advertisements
- `One-Time` display of `Learning Mitigation` Data Set into the Template
- `Black/White List`: specific filter that should black- or whitelist traffic
- `IP Based Filter Lists`: any IPv4 Address Filter Lists to black or whitelist `CIDR` that are appropriate for the managed object
- Used in case of an `User-Initiated` and / or `Auto Mitigation`
- Influence the distribution of the BGP diversion information
- Available per `Managed Object` from type:
  - Customer
  - Peer

## Inactive TMS Mitigation

![](https://i.ibb.co/QcXydMn/Screenshot-2023-06-14-130415.png)

### Configuration

- Choose Mitigation > Threat Management
- Run inactive mitigation and review the number of false positive drops