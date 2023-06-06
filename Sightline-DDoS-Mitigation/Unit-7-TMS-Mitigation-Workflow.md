# Unit 7: TMS Mitigation Workflow


## Table of contents

- [Unit 7: TMS Mitigation Workflow](#unit-7-tms-mitigation-workflow)
  - [Table of contents](#table-of-contents)
  - [TMS Mitigation Workflow](#tms-mitigation-workflow)
  - [Block versus Drop](#block-versus-drop)
  - [Countermeasure Processing Order](#countermeasure-processing-order)


## TMS Mitigation Workflow


- Process Overview
        
    ![](IMG/2023-06-06-14-59-06.png)

- Detect the Attack:
  - Detection, Classification and Alerting happens simultaneously
  - Analyze the details of the alert to determine if a mitigation is necessary

- Mitigating IPv6:

    ![](IMG/2023-06-06-15-02-04.png)

- Configuration:
  - Name: 
    - Taken from the DoS Alert
    - Unique name
  - Template
    - Associated with the MMO within the DOS Alert
  - Managed Object
    - MO associated with this mitigation, used for reports and MSSP Access
  - Allow Scoped User Access
  - Protection Prefixes
  - Use Less Specific Diversion Prefixes
  - Timeout
  - Flow Specification Filter
  - TMS Group
  - Announce Route

- Real Time Mitigation Status Page:
  - Display detailed statistics about a mitigation and allows you to edit the countermeasures being applied
  - Summary Tab
  - Traffic Graph
  - Countermeasures Tab
  - Units (bps and pps)
  - Time Period
    - Summary
    - Last 30 minute
    - Last 5 minute
    - Type of Traffic
      - Per countermeasure
      - Per TMS Appliance
      - Total
    - Sample Packets: One of the best tools for performing analysis of packets during mitigation 

- Mitigation Summary Report
- Mitigation  dropped Traffic Level in the DOS Alert:
  - When the mitigation starts, the Alert traffic graphs will reflect dropped traffic due to the mitigation actions

## Block versus Drop

- `TMS Traffic Actions`
  
    ![](IMG/2023-06-06-15-25-43.png)

- `Dynamic Blacklist (Host Blocking)`: Blacklisting countermeasure identifies source host that violate appropriate behavior
  - Offending Host added to dynamic blacklist
  - After blocking time
    - The host is removed from the dynamic blacklist
    - Traffic is processed again
    - If the host continues to offend it will be blacklisted again

- Dynamic Blacklist Countermeasures
  
    ![](IMG/2023-06-06-15-55-55.png)

## Countermeasure Processing Order

- Countermeasure are defense mechanisms that you can use to target and remove attack traffic, it act primarily using one or more of four enforcement types:
  - Pass packets
  - Drop packets
  - Block Source IP address or flow
  - Rate limit/ shape

- Processing Types
  - Per-Packet

    ![](IMG/2023-06-06-15-57-24.png)

  - Event-Driven




