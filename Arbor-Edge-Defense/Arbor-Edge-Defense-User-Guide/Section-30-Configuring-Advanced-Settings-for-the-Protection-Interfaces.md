# Section 30: Configuring Advanced Settings for the Protection Interfaces

## Table of contents

- [Section 30: Configuring Advanced Settings for the Protection Interfaces](#section-30-configuring-advanced-settings-for-the-protection-interfaces)
  - [Table of contents](#table-of-contents)
  - [Changing the Speed, Duplex Mode, and MTU for Protection Interfaces](#changing-the-speed-duplex-mode-and-mtu-for-protection-interfaces)
    - [About hardware bypass when making media changes](#about-hardware-bypass-when-making-media-changes)
    - [Viewing the media settings](#viewing-the-media-settings)
    - [Changing the speed and duplex mode](#changing-the-speed-and-duplex-mode)
    - [Changing the MTU](#changing-the-mtu)
  - [Configuring VLAN Subinterfaces](#configuring-vlan-subinterfaces)
    - [Adding VLAN subinterfaces](#adding-vlan-subinterfaces)
    - [Configuring VLAN subinterfaces](#configuring-vlan-subinterfaces-1)
    - [Adding access rules to a VLAN subinterface](#adding-access-rules-to-a-vlan-subinterface)
    - [Removing VLAN subinterfaces](#removing-vlan-subinterfaces)
  - [Troubleshooting the Protection Interfaces](#troubleshooting-the-protection-interfaces)
    - [Viewing the pause parameter settings for a protection interface](#viewing-the-pause-parameter-settings-for-a-protection-interface)
    - [Viewing the register information for a protection interface](#viewing-the-register-information-for-a-protection-interface)
    - [Viewing the configuration settings for a protection interface](#viewing-the-configuration-settings-for-a-protection-interface)

## Changing the Speed, Duplex Mode, and MTU for Protection Interfaces

- MTU: maximum transfer unit
- Set automatically when installing AED or change some of the these settings on certain appliances
- Cannot change the speed and duplex mode on `AED-HD1000`

### About hardware bypass when making media changes

- AED sets hardware bypass to open on all appliances except the `AED-HD1000`
- Hardware bypass on the `AED-HD1000` requires the external `NETSCOUT 3296 Inline Bypass Switch`
- If hardware bypass is not set to open on the `AED-HD1000`, then AED drops all packets on the protection interface for up to one minute while the changes take effect

### Viewing the media settings

- Log in to the CLI with administrator
- Enter `/ services aed mitigation interface media show interfaceName`

### Changing the speed and duplex mode

- In the CLI, enter `/ services aed stop`
- Enter `/ services aed mitigation interface media interfaceName {autoselect | speed value} duplex {full | half}`
- Enter `/ services aed start`
- Enter `/ config write`

### Changing the MTU

- In the CLI on the `AED HD-1000` appliance only, enter `/ services aed bypass force open`
- Enter `/ services aed stop`
- Enter `/ services aed mitigation interface media interfaceName mtu size`
- Enter `/ services aed start`
- Enter `/ config write`

## Configuring VLAN Subinterfaces

- Dividing a single management interface into multiple VLAN subinterfaces
- The management interface can be a physical or logical interface

### Adding VLAN subinterfaces

- Log in to the CLI with administrator
- Enter `/ ip interfaces vlan {mgt0 | mgt1} VLAN_ID`for each subinterface to add
- Enter `/ config write`

### Configuring VLAN subinterfaces

Configure a VLAN subinterface:

- In the CLI, enter `/ ip interfaces ifconfig subint_name IP_address {netmask | prefix_length} up` for each VLAN subinterface
- Enter `/ config write`

*Note*: Must delete existed route that uses a different interface or subinterface

Configure a default route that uses a VLAN subinterface:

- Enter `/ ip route delete default`
- Enter `/ ip route add default IP_address subint_name`
- Enter `/ config write`

### Adding access rules to a VLAN subinterface

- Enter `/ ip access add service subint_name CIDR` (Services: https, ping, ssh, snmp) for each service VLAN subinterface
- Enter `/ ip access commit`
- Enter `/ config write`

### Removing VLAN subinterfaces

- Enter `/ ip access show`
- Enter `/ ip access delete all` or enter `/ ip access delete service subint_name CIDR` for each access rule to delete
- Enter `/ ip interfaces vlan mgt_interface VLAN_ID delete`
- Enter `/ config write`

## Troubleshooting the Protection Interfaces

### Viewing the pause parameter settings for a protection interface

- Log in to the CLI with administrator
- Enter `/ system hardware interface protect_Interface pause-frames`

### Viewing the register information for a protection interface

Enter `/ system hardware interface protect_Interface dump-regs`

### Viewing the configuration settings for a protection interface

Enter `/ system hardware interface protect_Interface`

