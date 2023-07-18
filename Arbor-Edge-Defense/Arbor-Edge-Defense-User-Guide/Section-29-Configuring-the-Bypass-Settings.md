# Session 29: Configuring the Bypass Settings

## Table of contents

- [Session 29: Configuring the Bypass Settings](#session-29-configuring-the-bypass-settings)
  - [Table of contents](#table-of-contents)
  - [About Hardware Bypass and Software Bypass](#about-hardware-bypass-and-software-bypass)
    - [About hardware bypass](#about-hardware-bypass)
    - [About software bypass](#about-software-bypass)
    - [About bypass operations on the AED-HD1000 appliance](#about-bypass-operations-on-the-aed-hd1000-appliance)
      - [Hardware bypass on the AED-HD1000 appliance](#hardware-bypass-on-the-aed-hd1000-appliance)
      - [Software bypass on the AED-HD1000 appliance](#software-bypass-on-the-aed-hd1000-appliance)
  - [Configuring Hardware Bypass and Software Bypass](#configuring-hardware-bypass-and-software-bypass)
    - [Viewing the bypass configuration and status](#viewing-the-bypass-configuration-and-status)
    - [Setting the hardware bypass mode](#setting-the-hardware-bypass-mode)
    - [Forcing the hardware bypass mode](#forcing-the-hardware-bypass-mode)
    - [Enabling or disabling software bypass](#enabling-or-disabling-software-bypass)
    - [Disabling and re-enabling hardware bypass](#disabling-and-re-enabling-hardware-bypass)

## About Hardware Bypass and Software Bypass

- Configure AED to fail open (bypass) or fail closed (disconnect) if a power failure, hardware failure, or software failure occurs
- AED supports hardware bypass and software bypass (enabled by default). vAED supports software bypass only

### About hardware bypass

If a system failure occurs when hardware bypass is set to fail open, traffic passes through to the connected equipment. However, the traffic is not inspected

Setting to fail open or after issuing
```
  services aed bypass force open
```

AED drops the traffic
```
  services aed bypass force closed 
```

### About software bypass

If you disable software bypass and hardware bypass is configured, then the hardware bypass handles the software failures

### About bypass operations on the AED-HD1000 appliance

#### Hardware bypass on the AED-HD1000 appliance

Must reverse the connections on each module
of the `3296 Bypass Switch`:

- Connect the appliance ports (A1 and A2) on the bypass switch to the network
- Connect the network ports (N1 and N2) on the bypass switch to the protection ports on the `AED-HD1000`

The hardware bypass mode in the following situations:

- The management module on the AED-HD1000 is turned off or loses its connection with the 3296 bypass switch
- The software that handles communication with the 3296 bypass switch on the `AED HD1000 stops` working
- The PPMs are unable to perform a software bypass. This situation sometimes occurs when the system starts

#### Software bypass on the AED-HD1000 appliance

The usual software bypass method does not apply to the `AED-HD1000`:

- Initiating software bypass only when the AED services are stopped
- Do not initiate software bypass in the following situations:
  - One or more packet processors fail
  - One or more PPMs go down, are disabled, or are removed

## Configuring Hardware Bypass and Software Bypass

- By default, hardware bypass is set to fail open and software bypass is enabled.
- Hardware bypass and software bypass work only when AED is set to inline mode. AED
does not initiate a bypass when it is in monitor mode

### Viewing the bypass configuration and status

- Log in to the CLI with administrator
- Enter `/ services aed bypass show`

### Setting the hardware bypass mode

- In the CLI, enter `/ services aed bypass fail {open | closed}`
- Reversing the connections of the appliance ports and network ports on each module of the `3296 Bypass Switch`

### Forcing the hardware bypass mode

- Enter `/ services aed bypass force {open | closed}`
- Force a hardware bypass, the hardware
bypass takes precedence

### Enabling or disabling software bypass

Enter `/ services aed bypass software {enable | disable}`

### Disabling and re-enabling hardware bypass

- Enter `/ services aed bypass disable`
- Use the fail open command or the fail closed command to re-enable hardware bypass