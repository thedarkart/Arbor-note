# Section 31: Configuring Other Advanced Settings

## Table of contents

- [Section 31: Configuring Other Advanced Settings](#section-31-configuring-other-advanced-settings)
  - [Table of contents](#table-of-contents)
  - [Setting the Time and Date for the System Clock](#setting-the-time-and-date-for-the-system-clock)
    - [Setting the system clock](#setting-the-system-clock)
    - [Viewing the current time and date setting](#viewing-the-current-time-and-date-setting)
  - [Setting the Deployment Mode](#setting-the-deployment-mode)
    - [Setting the deployment mode](#setting-the-deployment-mode-1)
  - [Inspecting Packets with VLAN Q-in-Q Tunneling Tags](#inspecting-packets-with-vlan-q-in-q-tunneling-tags)
    - [About the supported ethertypes](#about-the-supported-ethertypes)
    - [Viewing the current VLAN Q-in-Q settings](#viewing-the-current-vlan-q-in-q-settings)
    - [Enabling VLAN Q-in-Q processing](#enabling-vlan-q-in-q-processing)
    - [Changing the ethertype](#changing-the-ethertype)
    - [Disabling VLAN Q-in-Q processing](#disabling-vlan-q-in-q-processing)
    - [Saving the configuration changes](#saving-the-configuration-changes)
  - [Overriding the AIF Feed URLs](#overriding-the-aif-feed-urls)
    - [Components of the AIF](#components-of-the-aif)
    - [Viewing the feed URLs](#viewing-the-feed-urls)
    - [Overriding a feed URL](#overriding-a-feed-url)
    - [Clearing a URL override](#clearing-a-url-override)
  - [Viewing AIF Version Information](#viewing-aif-version-information)
    - [Components of the AIF](#components-of-the-aif-1)
    - [Viewing the current AIF feed versions](#viewing-the-current-aif-feed-versions)
    - [Version information](#version-information)
  - [Advanced File Management from the Command Line Interface](#advanced-file-management-from-the-command-line-interface)
    - [Viewing the files in a directory](#viewing-the-files-in-a-directory)
    - [Copying a file](#copying-a-file)
    - [Arguments for copying files](#arguments-for-copying-files)
    - [Deleting a file](#deleting-a-file)
    - [Renaming a file](#renaming-a-file)


## Setting the Time and Date for the System Clock

Configure these settings on the Configure
General Settings page (Administration > General)

### Setting the system clock

- Log in to the CLI with administrator
- Enter `/ clock` set `YYYY-mm-dd HH:MM:SS`

### Viewing the current time and date setting

- Enter `/ clock`
- Enter `/ config write`

## Setting the Deployment Mode

The deployment modes:

- Inline: acts as a physical connection
- Layer 3 (vAED only): forwards all of
the traffic that meets the mitigation rules
- Monitor: monitor traffic without blocking a span port or network tap

### Setting the deployment mode

`AED` in the monitor mode requires to disable link state propagation

`vAED` in the layer 3 mode requires specify IP addresses for the protection interfaces and to configure routes for the traffic

- Log in to the CLI with administrator
- Enter `/ services aed mode set {inline | l3 | monitor}`

## Inspecting Packets with VLAN Q-in-Q Tunneling Tags

`VLAN Q-in-Q` tunneling tags while set to inline mode, then forwards the packets without inspecting them

### About the supported ethertypes

- 0x8100: the ethertype for the 802.1Q standard
- 0x9100: the proprietary Q-in-Q ethertype
- 0x88a8: the ethertype for the 802.11ad standard

### Viewing the current VLAN Q-in-Q settings

- Log in to the CLI with administrator
- Enter `/ services aed mitigation vlan-qinq show`

### Enabling VLAN Q-in-Q processing

Enter `/ services aed mitigation vlan-qinq enable`

### Changing the ethertype

Enter `/ services aed mitigation vlan-qinq ethertype hexValue`

### Disabling VLAN Q-in-Q processing

Enter `/ services aed mitigation vlan-qinq disable`

### Saving the configuration changes

Enter `/ config write`

## Overriding the AIF Feed URLs

AED uses HTTPS to download the latest AIF information at specified intervals

### Components of the AIF

- attack_rules: AIF botnet signatures
- geoip_countries: IP location data
- reputation_feed: ATLAS threat policies
- webcrawler_allowlist: a list of legitimate search engine web crawlers

### Viewing the feed URLs

- Log in to the CLI with administrator
- Enter `/ services aed aif url show [attack_rules | geoip_countries |reputation_feed | webcrawler_allowlist]`

### Overriding a feed URL

Enter `/ services aed aif url set feed_name url`

### Clearing a URL override

Enter `/ services aed aif url clear [attack_rules | geoip_countries | reputation_feed | webcrawler_allowlist]`

## Viewing AIF Version Information

Information about the downloaded feed components is recorded in the syslog

### Components of the AIF

- attack_rules: AIF botnet signatures
- geoip_countries: IP location data
- reputation_feed: ATLAS threat policies
- webcrawler_allowlist: a list of legitimate search engine web crawlers

### Viewing the current AIF feed versions

- Log in to the CLI with administrator
- Enter `/ services aed aif versions show [attack_rules | geoip_countries |reputation_feed | webcrawler_allowlist]`

### Version information

- `UNIX` timestamp of the latest download
- Etag (entity tag) identifier for the specific version
- Version number of the feed component
  
## Advanced File Management from the Command Line Interface

### Viewing the files in a directory

- Log in to the CLI with administrator
- Enter `/ system files directory { disk: | usb: | flash:}`

### Copying a file

Enter `/ system files copy source target`

### Arguments for copying files

- ftp: | http: | https: | scp:} = the protocol to use to access the remote host
- {disk: | usb: | flash:} = the storage device that contains the source file or the
storage device to copy the file to
- user = the user name that is required to access the remote host
- password = the user password that is required to access the remote host
- {A.B.C.D | \aaaa:bbbb::\} = the IP address of the remote host that contains the source
file
- port = the port on the remote host
- file_name = the name of the file to be copied

### Deleting a file

Enter `/ system files delete {disk: | usb:}file_name`

### Renaming a file

Enter `/ system files rename {disk: | usb:}old_name {disk: | usb:}new_name`



