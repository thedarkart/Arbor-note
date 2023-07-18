# Section 6: Managing AED from Arbor Enterprise Manager

## Table of contents

- [Section 6: Managing AED from Arbor Enterprise Manager](#section-6-managing-aed-from-arbor-enterprise-manager)
  - [Table of contents](#table-of-contents)
  - [About Managing Devices from AEM](#about-managing-devices-from-aem)
    - [Device management tasks](#device-management-tasks)
    - [Communication between AEM and the devices](#communication-between-aem-and-the-devices)
    - [Single sign-on](#single-sign-on)
  - [About Data Synchronization with AEM](#about-data-synchronization-with-aem)
    - [Viewing the synchronization status](#viewing-the-synchronization-status)

## About Managing Devices from AEM

### Device management tasks

- Centrally create, configure, and manage the server types,protection groups, outbound threat filter, deny lists, and allow lists in AEM
- Share common protection groups and server types across multiple devices
- View the traffic and statistics from each device as well as an aggregate of the data from all of the devices
- View active bandwidth alerts and system alerts for all of the devices
- View and respond to the threats that are identified by the ATLAS threat policies
- Respond to availability attacks by changing the protection level, adding hosts to the deny list, or modifying the protection settings globally or per device.
- Navigate to a specific device to view more detailed information about its configuration or traffic.

### Communication between AEM and the devices

- Connect the device to AEM for manage a device from AEM
  - AEM sends request to each device for information (alerts, traffic data)
  - Device checks AEM periodically for configuration changes and obtains the changes that apply to the device

### Single sign-on

- Can navigate to a device from several areas in the AEM UI
- If your user account on the device has the same username as your AEM user account, then the device opens without prompting you to log in. 
  - Can use a different password for each account
- Must have a valid reverse DNS lookup

## About Data Synchronization with AEM

### Viewing the synchronization status

- `Initial synchronization`
- `Preparing configuration`
- `Good`
- `Out of sync`