# Unit 1: Sightline Introduction

## Table of contents

- [Unit 1: Sightline Introduction](#unit-1-sightline-introduction)
  - [Table of contents](#table-of-contents)
  - [Capturing Network Traffic Information](#capturing-network-traffic-information)
    - [In a Nutshell](#in-a-nutshell)
    - [Overview](#overview)
      - [Flow Data](#flow-data)
      - [BGP Routing Information](#bgp-routing-information)
      - [SNMP](#snmp)
    - [Flow Export](#flow-export)
    - [Router Flow Cache](#router-flow-cache)
    - [Capturing Network Traffic Information](#capturing-network-traffic-information-1)
    - [BGP Peering](#bgp-peering)
  - [Scalable Architecture](#scalable-architecture)
    - [Appliance Types And Roles](#appliance-types-and-roles)

## Capturing Network Traffic Information

### In a Nutshell

- Pervative Network Visibility (Traffic view)
- Advanced Threat Protection (Detect & mitigate)
- Service Enablement (Monetize)
- Use both `flow` and `deep packet inspection (DPI)` technologies and provides macro- and micro-level visibility

### Overview

#### Flow Data

- Network traffic details
- DDoS Detection
  
#### BGP Routing Information

- Provides reachability and data path information
- Peering analysis
- Mitigation capabilities via `Blackhole injection`, `Diversion of traffic`, or `Flow Spec`
  
#### SNMP

- Provide context for DDoS and Traffic Analysis
- Tracks interface id, name, description and speed
- Verification of flow derived traffic volumes

### Flow Export

![](https://i.ibb.co/mqYHTXF/Screenshot-2023-05-26-085251.png)

Models create both `threshold-based` and `behavioral-based` traffic `baselines`. `Sightline` uses the learned and configured traffic baselines to create alerts when the system observes `abnormal traffic`

### Router Flow Cache

![](https://i.ibb.co/9G5197C/Screenshot-2023-05-26-090427.png)

### Capturing Network Traffic Information

- Apply a longest match of `source IP` &`destination IP` from the `flow` with
the prefixes in `BGP routing table`
- Flow will match a prefix and therefore that same flow will match that prefix’s AS Path (lists all the `ASes` that need to be traversed to reach the location where the prefix that the path is attached to is advertised from), next-hops, and communities

### BGP Peering

- Reachability and path infotmation
- Peering analysis
- Mitigation capabilities
- `Flow spec` is used to convey `Access Control List information` via `BGP`

## Scalable Architecture

### Appliance Types And Roles

- Traffic and Routing Analysis (TRA)
- Threat Mitigation System (TMS)
- Data Storage (DS)
- User Interface (UI)




