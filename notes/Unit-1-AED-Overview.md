# Unit 1: NETSCOUT AED Overview

## Table of contents

- [Unit 1: NETSCOUT AED Overview](#unit-1-netscout-aed-overview)
  - [Table of contents](#table-of-contents)
  - [AED architectural and functional](#aed-architectural-and-functional)
    - [AED Platform](#aed-platform)
    - [AED Interfaces](#aed-interfaces)
  - [Establish UI familiarity and workflow](#establish-ui-familiarity-and-workflow)
    - [Accessing the Web User Interface (UI)](#accessing-the-web-user-interface-ui)
    - [AED Administration Workflows](#aed-administration-workflows)
  - [Current AED Operational status](#current-aed-operational-status)
  - [Establish perspective by identifying current traffic characteristics](#establish-perspective-by-identifying-current-traffic-characteristics)
    - [Improving Visibility with Protection Groups](#improving-visibility-with-protection-groups)
    - [Turning Protection Setting using Traffic Profiles](#turning-protection-setting-using-traffic-profiles)


## AED architectural and functional

### AED Platform

- Arbor Edge Defense (AED) platform:
  - A single, stand-alone device
  - Deploy at ingress point to detect, block, and report on DDoS attacks.

- `First & Last Line of Defense`
  - First line of defense:
    - Deployed at the network perimeter
    - Using stateless technology and armed with millions of IoCs => Can detect and block inbound commodity cyber threats 
    - Taking pressure off of stateful devices such as Next Gen Firewalls
  - Last line of defense:
    - Can detect and block outbound communication to known bad IP addresses, domains, URLs, geographies 
    - Helping stop the further proliferation of malware within an organization and avoid a data breach.

  ![](IMG/2023-05-17-18-57-16.png)

  - Deployment guidelines:
    - Deploy the appliance at the data center’s premises, on the internet edge of the data center’s network.
    - AED is external to all of the additional security devices => Protects these devices from attacks
    - Inline deployment without an IP address with either the inbound interface or the outbound interface.


- `Support for Virtual & Hybird-Cloud Environments`

- `"Out-of-the-box" Protection`

- `Outbound Threat Filter`

- `ATLAS Intelligence Feed (AIF)`

- `Block Threats using STIX/TAXII 2.0 Support`

- `Cloud Signaling`

- `Protecting SSL Encrypted Traffic`

- `Central Management`

- `Executive Summary and ATLAS Global DDoS Reports`


### AED Interfaces

- AED Management Interfaces

- AED Protection Interfaces

- Interface Pairing
  
- Protection Interfaces: Bypass

- Bypass Subcommands:

## Establish UI familiarity and workflow

### Accessing the Web User Interface (UI)

- Instructor-led Demonstration of Web UI


### AED Administration Workflows

- Status Bar - Deployment Mode

- Monitor Deployment Mode

## Current AED Operational status

- Summary Page Overview

- Top Protection Groups Section

- Overview Section

- Top Countries Section

- Top Inbound Sources & Destinations Sections

- ATLAS Botnet Prevention Section

- Web Crawlers

- Viewing Protections Interfaces

## Establish perspective by identifying current traffic characteristics

### Improving Visibility with Protection Groups 

- Protection Groups (PGs)

- Default Protection Group

- Supported Protection Groups Limits

- Protection Group Mode

- Protection level

- Server types

- Protection group Server type

- Server Types and Attack Protections

- Protections per Standard Server type

- Inbound Protection Processing Sequence


### Turning Protection Setting using Traffic Profiles

- Traffic Profile Learning

- Profile - Protections Supported

- Profile Capture

- Inaccurate Profiled Data May Result
