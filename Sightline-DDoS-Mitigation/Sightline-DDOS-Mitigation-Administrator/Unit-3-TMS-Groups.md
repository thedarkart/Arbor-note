# Unit 3: TMS Groups

## Table of contents

- [Unit 3: TMS Groups](#unit-3-tms-groups)
  - [Table of contents](#table-of-contents)
  - [Locations and Traffic Distribution](#locations-and-traffic-distribution)
    - [Overview](#overview)
    - [Redundancy](#redundancy)
    - [Traffic Diversion](#traffic-diversion)
    - [Load Sharing](#load-sharing)
    - [TMS Group Design](#tms-group-design)
  - [TMS Group Configuration](#tms-group-configuration)
  - [Mitigation Orchestration](#mitigation-orchestration)
    - [Overview](#overview-1)
    - [Configuration](#configuration)
    - [Monitoring](#monitoring)

## Locations and Traffic Distribution

### Overview 

- Distributed
  - Small attack footprint
  - Limited scalability
- Centralized
  - Bigger attack footprint
  - Scalability, supports Redundancy

### Redundancy

- Scrubbing Centers use an IP Anycast, the IGP routing protocol selects the closest location
- In the event of an outage the traffic is routed by the IGP routing protocol to the remaining Scrubbing Center

### Traffic Diversion

- BGP Route Diversion
- BGP FlowSpec Diversion

### Load Sharing

Traffic Distribution between TMS in the same Location

### TMS Group Design

- North and South
- Data center 1 and 2
- Managed services classes

## TMS Group Configuration

- Choose Administration > Mitigation > TMS Groups
- Add with name and decription
- Specified BGP diversion parameters will overwrite the individual TMS configuration:
  - Nexthops
  - Communities
  - Flowspec redirect
- Deployment: Define the TMS Group behaviour if a member fails
- Mitigation Preconditions: Define required preconditions before a TMS Groups accepts a any new Mitigation
- DNS Authentication countermeasure in Active UDP mode is used, the TMS should know for which DNS Authoritative Servers 6 it should use which IP 7 for ‘redirecting’ during the authentication process

## Mitigation Orchestration

### Overview

The volume of attacks can lead to a TMS appliance being overloaded according to its maximum capacity

### Configuration

- Choose Administration > Mitigation > Global Settings
- Be returned to the original TMS Group
- Interval in which the capacity is checked if a mitigation can be returned
- Pause time where mitigation is present on
the initial and the new TMS Group to ensure
the network can converge
- Time the capacity must be exceeded on any
TMS in a group to start a mitigation move
- On the TMS Group configure the bandwidth threshold that must be exceeded before a mitigation can be moved
- Specify the TMS Group to which the mitigation should be moved to (if there are
enough resources available)

### Monitoring

Sightline will generate a corresponding alert and update the annotations
- Successful
- Failed

