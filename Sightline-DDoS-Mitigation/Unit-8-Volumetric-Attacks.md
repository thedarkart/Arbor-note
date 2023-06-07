# Unit 8: Volumetric Attacks

## Table of content

- [Unit 8: Volumetric Attacks](#unit-8-volumetric-attacks)
  - [Table of content](#table-of-content)
  - [Flooding Attacks](#flooding-attacks)
  - [Invalid Packets](#invalid-packets)
  - [Filter Lists](#filter-lists)
  - [UDP Reflection and Amplification](#udp-reflection-and-amplification)
  - [Zombie Detection](#zombie-detection)


## Flooding Attacks

- Overview:
  - Description:
    - Traffic to one or more protocols or ports
    - Spoofed or non-spoofed Traffic
    - Looks like normal Traffic
    - Reflection Attacks
  - Sightline Detection Capabilities:
    - Host Detection
    - Profiled Detection
  - TMS Mitigation CountermeasuresL
    - Zombie Detection
    - UDP Reflection/ Amplification
    - Per Connection Flood
    - Black/ White lists
    - HTTP/ DNS Rate Limiting 
    - Payload RegEX Filtering
  - Attacks: 
    - UDP Floods
    - Reflection Attacks
    - Black Energy
    - Mirai Botnet Variants
    - Memcached

- UDP Floods

      ![](IMG/2023-06-07-13-57-55.png)

- Fragmentation Attacks

      ![](IMG/2023-06-07-14-01-26.png)


## Invalid Packets

- Invalid Packets is a per packet countermeasure that ensures that all incoming frames are valid IP packets and that basic IP header requirement are fulfilled

- IPv4:
  - Invalid packet checks apply to every mitigation

      ![](IMG/2023-06-07-14-11-46.png)

- IPv6:
  - Invalid packet checks apply to every mitigation 

      ![](IMG/2023-06-07-14-12-30.png)

## Filter Lists

- Overview: 
  - Filter Lists can reduce the processing load on the TMS
    - Limiting the amount of traffic that needs to go through all countermeasures
    - If a packet matches, no further processing will be done
  - Sightline can automatically import Filter Lists from external
    - Filter Lists are configured globally 
    - Filter Lists can be pre-assigned via template or added on the fly
    - Multiple filters can be selected simultaneously
    - Multiple filters can be selected simultaneously
  - Filter lists are often compared to ACLs


- Use Cases:
  - Pass lists
    - Known partner network
    - Approved remote workers
    - Know secure clients
  - Block lists
    - Security group infected subscriber lists
    - Third-party tool bot and infected host lists
    - Networks or countries without legitimate use case

- Types:
  
      ![](IMG/2023-06-07-14-18-38.png)

- IP Address Filter:
  - User-defined lists of IP addresses/CIDR blocks
    - Towards the top of the processing order, immediately after the the Blocked Host List
    - IP address sources that are known in advance can be processed immediately

- IPv4 Black/ White Filter List:
  - Inline Filters
    - Freeform FCAP filter
    - Configured before or during Mitigation
  - Black/ White Filter Lists
  - Blacklist Fingerprints

- FCAP format to explicitly DROP or PASS traffic
  - Known sources to PASS
  - Known sources to DROP
  - Invalid/ Unwanted port and protocols


- IP Location Filter
  - IP Location filter lists are selected IP location country codes.
  - IP location Country codes use large lists of associated IP address prefixes to match traffic
  - IP Location filter lists are globally configured or uploaded
  - Mitigations can use any IP Location filter list to match traffic

## UDP Reflection and Amplification

- Overview:
  - It comes later in the packet processing order
    - Useful if you need to pass some legitimate traffic before applying this countermeasure
    - It provides detailed individual drop statistics
    - Can be automated through the Alert Misuse types detected

- Configuration
  - Built to handle most common UDP DDoS attack vectors
  - Can be configured to either drop or blacklist offending external hosts
  - Uses predefined FCAP filters
  
- Expand any of the filters to add additional FCAP match criteria

## Zombie Detection

- Overview:
  - A per-packet countermeasure against flood, TCP SYN and protocol attacks
  - It monitors overall bps, pps and traffic rate from each source host. Once every minute, the zombie countermeasure checks bps, pps and traffic rate from each source host 





