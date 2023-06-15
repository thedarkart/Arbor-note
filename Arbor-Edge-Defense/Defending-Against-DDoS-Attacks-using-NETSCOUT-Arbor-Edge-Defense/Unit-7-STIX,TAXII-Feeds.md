# Unit 7: STIX, TAXII Feeds

## Table of contents

- [Unit 7: STIX, TAXII Feeds](#unit-7-stix-taxii-feeds)
  - [Table of contents](#table-of-contents)
  - [Netsout AED STIX/TAXII Implementation](#netsout-aed-stixtaxii-implementation)
    - [Note pattern](#note-pattern)
    - [STIX 2.0 and TAXII 2.0 Support](#stix-20-and-taxii-20-support)
    - [STIX 2.0 and TAXII 2.0 Overview](#stix-20-and-taxii-20-overview)
    - [Supported STIX Objects and Patterns](#supported-stix-objects-and-patterns)
    - [Configuring TAXII Clients to Push STIX IOCs](#configuring-taxii-clients-to-push-stix-iocs)
    - [Authorize a Client](#authorize-a-client)
    - [Add a TAXII Client](#add-a-taxii-client)
    - [Create and Manage Collections of STIX IOCs](#create-and-manage-collections-of-stix-iocs)
    - [Add a TAXII Collection](#add-a-taxii-collection)
    - [Enabling STIX Feeds for In/Outbound Threats](#enabling-stix-feeds-for-inoutbound-threats)
    - [Viewing STIX Threats on the Summary Page](#viewing-stix-threats-on-the-summary-page)
    - [Viewing Traffic Blocked by STIX Threats](#viewing-traffic-blocked-by-stix-threats)
    - [Viewing Hosts Blocked by STIX Threats](#viewing-hosts-blocked-by-stix-threats)

## Netsout AED STIX/TAXII Implementation

### Note pattern

- STIX - Structured Threat Information eXpression: `JSON-based` lexicon to express and share threat intelligence information
- TAXII - Trusted Automated eXchange of Intelligence Information works by defining the protocols for exchanging data

### STIX 2.0 and TAXII 2.0 Support

- For now only 'push' from a `Threat Intelligence Platform (TIP)` Supports up to 3 million `Indicators of Compromise (IOCs)`
- 16 Collections includes 1 "Default Indicators Collection" and 15 Custom Collections
- 500,000 `IOCs` per collection

### STIX 2.0 and TAXII 2.0 Overview

![](https://i.ibb.co/5KrSx9z/Screenshot-2023-05-21-203313.png)

### Supported STIX Objects and Patterns

Support for `STIX objects`:
- attack-pattern
- indicator
- malware
- tools
- relationship

Support for `IOC patterns`:
- ipv4-addr
- domain-name
- url

### Configuring TAXII Clients to Push STIX IOCs

- Select Administration > STIX/TAXII
- Configure authorized TAXII clients
- Manage STIX collections

### Authorize a Client

- Add a client 
- Disable or enable client

### Add a TAXII Client

- Unique name to identify the `TAXII 2.0 client`
- Create a unique username to
authenticate the client
- A password to authenticate the client

### Create and Manage Collections of STIX IOCs

- Add a collection
- Enable, disable, clear, delete collection

### Add a TAXII Collection

Create collection for per purpose

### Enabling STIX Feeds for In/Outbound Threats

- Outbound Threat Filter Protection Setting
- Server Type Protection Setting

### Viewing STIX Threats on the Summary Page

Show sumary bytes and packets blocked for each collection

### Viewing Traffic Blocked by STIX Threats

Additional Attack Category Listed for the OTF or the Protection Group

### Viewing Hosts Blocked by STIX Threats

Using filter to view specific Protection groups and Attack categories