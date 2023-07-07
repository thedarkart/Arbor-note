# Section 4: Implementing AED

## Table of contents

- [Section 4: Implementing AED](#section-4-implementing-aed)
  - [Table of contents](#table-of-contents)
  - [Implementing AED for Trial or Monitoring Only](#implementing-aed-for-trial-or-monitoring-only)
    - [About trial implementations](#about-trial-implementations)
    - [Trial of protection groups and the outbound threat filter](#trial-of-protection-groups-and-the-outbound-threat-filter)
    - [Required configurations](#required-configurations)
    - [Work flow](#work-flow)
    - [After the trial period](#after-the-trial-period)
  - [Implementing AED for Active Mitigation](#implementing-aed-for-active-mitigation)
    - [Workflow](#workflow)
  - [About the AED Deployment Models](#about-the-aed-deployment-models)
    - [Types of deployment models](#types-of-deployment-models)
  - [Network Connectivity Models](#network-connectivity-models)
      - [About the Protection interface connections](#about-the-protection-interface-connections)
      - [Connectivity Model: Inline mode](#connectivity-model-inline-mode)
      - [Connectivity model: layer 3 mode (vAED only)](#connectivity-model-layer-3-mode-vaed-only)
      - [Connectivity model: monitor mode](#connectivity-model-monitor-mode)
  - [About the Deployment Modes](#about-the-deployment-modes)
    - [About the inline mode and layer 3 mode](#about-the-inline-mode-and-layer-3-mode)
    - [About the monitor mode](#about-the-monitor-mode)
    - [Viewing the current deployment mode](#viewing-the-current-deployment-mode)
  - [About the Layer 3 Deployment Mode](#about-the-layer-3-deployment-mode)
    - [Changing the deployment mode from inline to layer 3](#changing-the-deployment-mode-from-inline-to-layer-3)
    - [Changing the deployment mode from layer 3 to inline](#changing-the-deployment-mode-from-layer-3-to-inline)
    - [Backing up and restoring data while oin the layer 3 deployment mode](#backing-up-and-restoring-data-while-oin-the-layer-3-deployment-mode)
  - [Setting the Protection Mode (Active or Inactive)](#setting-the-protection-mode-active-or-inactive)
    - [About changing the protection mode for multiple devices](#about-changing-the-protection-mode-for-multiple-devices)
    - [Viewing the current protection mode](#viewing-the-current-protection-mode)
    - [Changing the system-wide protection mode](#changing-the-system-wide-protection-mode)



## Implementing AED for Trial or Monitoring Only

### About trial implementations

- Should perform a trial implementation before you allow AED to affect your network traffic
- A trial is the same as a monitor-only implementation but it can show you how AED would block traffic, and you can adjust different protection settings to analyze how they affect the suggested mitigations
- Recommend to allow 30 to 60 days for a trial period

### Trial of protection groups and the outbound threat filter

- Situations that you might test an individual protection group after the initial implementation:
  - Introduce a new server within the data center and create a new protection group for that server
  - An existing web site is updated with a new page
  - An AED upgrade introduces new protection categories

### Required configurations

- Monitor deployment mode
- Inline deployment mode with the protection mode set to inactive

### Work flow

- Performing a trial or monitor-only implementation

  ![](IMG/2023-07-02-01-00-52.png)
  ![](IMG/2023-07-02-01-01-07.png)

### After the trial period

- Use AED in monitor-only mode: no further steps are needed.
- Begin mitigating traffic: Configure for an active implementation


## Implementing AED for Active Mitigation

- AED can mitigate traffic only when the deployment mode is `Inline Bridged` and the protection mode is active

### Workflow

Step 
1. Determine where and how to place AED in your network
2. Install AED by following the instructions in the `AED Installation Guide`
3. Configure the minium settings for using AED
4. Verify the following settings
   - The protection mode: **Active**
   - The protection level: **Low**
5. (Optional) Adjust the protection settings
6. (Optional) Add one or more protection groups
7. (Optional) Add one or more protection groups

## About the AED Deployment Models

### Types of deployment models

  ![](IMG/2023-07-05-18-20-45.png)

## Network Connectivity Models

- Ways to connect AED
  - Inline with or without mitigations enabled
  - Out-of-line through a span port or network tap, with no mitigations (monitor mode)

#### About the Protection interface connections

- The protection interfaces: ext, int0, ext1, int1 (ext for external, int for internal)
  
#### Connectivity Model: Inline mode

- AED analyzes the traffic, detects attacks and mitigates the attacks before it sends the traffic to its destination

  ![](IMG/2023-07-05-18-29-57.png)

- Can configure AED to fail open (bypass) or fail closed (disconnect) if a power failure, hardware failure, or software failure occurs
- By default, hardware bypass is set to fail open and software bypass is enabled
- Inactive protection mode: AED analyzes traffic and detects attacks without performing mitigations

#### Connectivity model: layer 3 mode (vAED only)

- Configure mitigations routes by specifying IP addresses for the nexthop and the destination host
- vAED inspects all of the traffic that traverses the specified route and mitigates any attacks before it routes the traffic to its destination.

  ![](IMG/2023-07-05-19-24-32.png)

#### Connectivity model: monitor mode

- Deployed out-of-line through a span port or network tap
- Analyze traffic, detects possible attacks but not mitigations

  ![](IMG/2023-07-05-19-26-00.png)

- Should disable link state propagation if you deploy AED in the monitor mode:  The link state propagation can prevent the corresponding external interface from coming up


## About the Deployment Modes

### About the inline mode and layer 3 mode

- As a physical connection between two end points
- Can configure to block traffic

- The inline deployment mode: **Inline Bridged**
- The layer 3 deployment mode appears: **Inline Routed**
  
- Protection mode:
  - Active: AED mitigates attacks in addition monitoring traffic and detecting attacks
  - Inactive: Not performing mitigations

### About the monitor mode

### Viewing the current deployment mode

In the upper right of the AED window

## About the Layer 3 Deployment Mode

- Only for vAED
- Deployment Mode: **Inline Routed**
- Need a valid license 
- In this mode, vAED will forwards all of the traffic that meets the mitigation rules and has a route configured for the destination network

### Changing the deployment mode from inline to layer 3

- vAED removes any GRE tunneling settings: routes, local IP address, remote IP address, subnet mask length

### Changing the deployment mode from layer 3 to inline

- vAED removes:
  - Any routes that are configured for the protection interfaces
  - Any Ip addrtess that are configured for the protection interfaces
  - Any GRE tunneling settings: local IP addresses, remove IP addresses, subnet mask length

### Backing up and restoring data while oin the layer 3 deployment mode

- The following data is not included in any backup:
  - Any GRE tunneling settings that are configured on the **Interfaces** in the UI 
  - Any routes that are configured for the protection interfaces

## Setting the Protection Mode (Active or Inactive)

- Active: Monitoring traffic, detecting attacks, mitigates attacks
- Inactive: Like active but not have mitigates attacks

### About changing the protection mode for multiple devices

- Can set the protection mode for multiple devices
  - Every device to which a protection group is assigned uses the protection mode that you configure for that protection group
    - Can override the protection group's protection mode of a specific device
  - For outbound traffic, all of the managed devices use the protection mode that is set for the AEM outbound threat filter

### Viewing the current protection mode

- `System-wide`: display in the upper right of the device window
- `Protection group`: 
  - List Protection Groups (Protect > Inbound Protection > Protection Groups)
  - View Protection Group
- `Outbound threat filter`: Protect > Outbound Protection > Outbound Threat Filter


### Changing the system-wide protection mode

- Select at the upper right of the device window