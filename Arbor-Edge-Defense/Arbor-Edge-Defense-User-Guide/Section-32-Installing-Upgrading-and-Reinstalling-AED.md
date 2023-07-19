# Section 32: Installing, Upgrading, and Reinstalling AED

## Table of contents

- [Section 32: Installing, Upgrading, and Reinstalling AED](#section-32-installing-upgrading-and-reinstalling-aed)
  - [Table of contents](#table-of-contents)
  - [Installing the License Keys for AED and AIF](#installing-the-license-keys-for-aed-and-aif)
    - [Renewing or upgrading your licenses](#renewing-or-upgrading-your-licenses)
    - [Exceptions to the appliance-based licensing method](#exceptions-to-the-appliance-based-licensing-method)
    - [Installing or upgrading the license keys](#installing-or-upgrading-the-license-keys)
  - [Installing a Locally-Managed Flexible License](#installing-a-locally-managed-flexible-license)
    - [Obtaining a locally-managed flexible license file](#obtaining-a-locally-managed-flexible-license-file)
    - [Installing the flexible license file](#installing-the-flexible-license-file)
  - [Installing AED](#installing-aed)
  - [Upgrading from APS to AED](#upgrading-from-aps-to-aed)
    - [Uploading the AED files](#uploading-the-aed-files)
    - [Upgrading to AED](#upgrading-to-aed)
  - [Upgrading the AED Software](#upgrading-the-aed-software)
    - [Upgrade steps](#upgrade-steps)
    - [Uploading the upgrade files](#uploading-the-upgrade-files)
    - [Upgrading the AED software](#upgrading-the-aed-software-1)
  - [Reinstalling AED](#reinstalling-aed)
    - [Determining the current software versions](#determining-the-current-software-versions)
    - [Reinstalling the AED software](#reinstalling-the-aed-software)

## Installing the License Keys for AED and AIF

Installing the license key for the AED software during the initial AED installation and configuration

Installing or replacing the licenses in the following situations:

- Purchase or renew an AED license
- Upgrade AED license to increase traffic throughput limit
- Subscribe to the AIF or renew AIF subscription
- Upgrade AIF subscription to a different level
- Upgrade from APS to AED

### Renewing or upgrading your licenses

Install a new AED license key to renew or upgrade your AED throughput license

### Exceptions to the appliance-based licensing method

- vAED uses a cloud-based flexible license instead of a license key
- The AED-HD1000 appliance and AED 8100 appliance use locally-managed flexible
licenses instead of license keys

### Installing or upgrading the license keys

- Log in to the CLI with administrator
- Enter `/ system license set AED "model" licenseKey`
- Enter `/ system license set ASERT "level expires: expirationDate" licenseKey`
- Enter `/ system license show`
- Enter `/ config write`

## Installing a Locally-Managed Flexible License

With locally-managed flexible licensing, downloading a license file from the license portal and install the file on an appliance

### Obtaining a locally-managed flexible license file

Receiving an email that contains instructions for downloading the 30-day expired license file from the license portal after  purchased a locally-managed flexible license

### Installing the flexible license file

- Log in to the AED UI
- Select Administration > Files
- Manage Files page > Upload File
- Upload File window >  Choose File
- Locact and select the license file
- Upload > Close
- Enter `/ system license server load disk:license_file license_file = the name of the license file`
- Enter `/ system license show`

## Installing AED

- Using a serial console server, connec to the serial port
- Turn on the appliance
- At the login prompt, enter `admin`
- At the password prompt, enter `arbor`
- Enter `/ services aaa local password admin interactive`
- At the password prompts, enter the new password
- Enter `ip interfaces ifconfig port IP_address {netmask | prefix_length} up`  
- Enter `/ ip route add default IP_address`
- Enter `/ ip access add service {mgt0 | mgt1 | all} CIDR` for each service
- Enter `/ ip access commit`
- Enter `/ system name set hostName`
- Enter `/ services dns server add IP_address` (Optional)
- Enter `/ services dns server add IP_address` or `/ services ssh key host set disk:fileName`
- Enter `/ services ssh start`
- Enter `/ services ntp server add IP_address` (Optional)
- Enter `/ clock set YYYY-mm-dd HH:MM:SS`
- Enter `/ system license set AED "model" licenseKey` or  `/ system license set ASERT "level expires: expirationDate" licenseKey`
- Enter `/ services aed mode set {inline | monitor}`
- Enter `/ services aed database initialize`
- Enter `/ config write` then `/ reload`
- Enter `/ services aed start` > `/ config write` > `/ exit`

## Upgrading from APS to AED

- Upload the AED files to APS
- Upgrade with CLI then start AED

### Uploading the AED files

- Verify that APS can access the AED files
- Taking note of file name
- Log in to APS
- Administration > Files > Upload File
  
### Upgrading to AED

Prepare

- Verify that the new files have been uploaded
- Log in to the CLI with administrator
- Enter `/ system files show`
- Taking note of the `APS package name`

Install

- Enter `/ system files uninstall oldPackageName`
- Enter `/ system files install disk:arbosFileName`
- Enter `/ system files install disk:aedFileName`
- Enter `/ system files show`

Take changes and reload

- Enter `/ services aps stop`
- Enter `/ config write`
- Enter `/ reload` > `/ services aed start` > `/ config write` > `/ exit` 

## Upgrading the AED Software

### Upgrade steps

- Upload the upgrade files to AED
- Upgrade with CLI
- Upgrade the firmware to use the `hardware security module (HSM)`
- Restart AED
- Install the upgrade licenses for AED and ATLAS Intelligence Feed (AIF)

### Uploading the upgrade files

- Verify that AED can access upgrade files
- Taking note of upgrade file names
- Log in with administrator
- Administration > Files
- Verify that the new version is a valid upgrade
for the package or packages
- To copy the new ArbOS file to AED and AED file, click Upload File

### Upgrading the AED software

- Verify that the new uploaded files
- Log in with administrator
- Enter `/ system files show`
- Making note of the old AED package name
- Enter `/ services aed stop`
- Enter `/ config write`
- Enter `/ system files uninstall oldPackageName`
- Enter `/ system files install disk:arbosFileName`
- Enter `/ reload`
- Enter `/ system files show`
- Enter `/ system files install disk:aedFileName`
- Enter `/sys hsm firmware update` to upgrade the firmware
- Enter `/ reload`
- Enter `/ services aed start` > `/ config write` > `/ exit`
  
## Reinstalling AED

### Determining the current software versions

- UI: in the lower-right corner of any page in the UI, click the `About link`
- CLI: enter `/ system version`

### Reinstalling the AED software

- Connect to AED with
  - Serial cable
  - VGA monitor and keyboard
- Restart the appliance
  - Log in with administrator
  - Enter `/ services aed stop`
  - Enter `/ config write`
  - Enter `/ reload`
- At the GRUB menu, press the up arrow key or down arrow key to stop the 10-second countdown
- After the installation is complete, restore the backup data
