# Section 27: Managing AED

## Table of contents

- [Section 27: Managing AED](#section-27-managing-aed)
  - [Table of contents](#table-of-contents)
  - [Viewing the Change Log](#viewing-the-change-log)
    - [Events that create change log entries](#events-that-create-change-log-entries)
    - [About exporting the change log](#about-exporting-the-change-log)
    - [Viewing the complete change log](#viewing-the-complete-change-log)
  - [Managing Diagnostics Packages](#managing-diagnostics-packages)
    - [Creating a diagnostics package](#creating-a-diagnostics-package)
    - [Emailing a diagnostics package to ATAC](#emailing-a-diagnostics-package-to-atac)
    - [Downloading a diagnostics package](#downloading-a-diagnostics-package)
    - [Deleting diagnostics packages](#deleting-diagnostics-packages)
  - [Managing the Files on AED](#managing-the-files-on-aed)
    - [About the file types](#about-the-file-types)
    - [Downloading files from AED](#downloading-files-from-aed)
    - [Uploading local files to AED](#uploading-local-files-to-aed)
    - [Deleting local files from AED](#deleting-local-files-from-aed)
  - [About Backups](#about-backups)
    - [About the backup data](#about-the-backup-data)
    - [Types of backups](#types-of-backups)
    - [About backups and password expiration](#about-backups-and-password-expiration)
    - [Storing backups](#storing-backups)
    - [Retention policy for backups](#retention-policy-for-backups)
    - [About the Available Backups list](#about-the-available-backups-list)
    - [Backing Up AED Manually](#backing-up-aed-manually)
    - [Backing up manually](#backing-up-manually)
  - [Restoring AED from Backups](#restoring-aed-from-backups)
    - [Data that is not restored from a backup](#data-that-is-not-restored-from-a-backup)
    - [Data restoration on AED devices](#data-restoration-on-aed-devices)
    - [Previous version support](#previous-version-support)
    - [Stopping and restarting AED during data restoration](#stopping-and-restarting-aed-during-data-restoration)
    - [Restoring from a backup](#restoring-from-a-backup)
    - [Error handling](#error-handling)
    - [Recovering from a system failure](#recovering-from-a-system-failure)
  - [How Restoring Backups Affects the AEM - Device Synchronization](#how-restoring-backups-affects-the-aem---device-synchronization)
    - [Guidelines for restoring an AEM backup](#guidelines-for-restoring-an-aem-backup)
    - [Guidelines for restoring a device backup](#guidelines-for-restoring-a-device-backup)
  - [Downloading and Uploading Backup Files](#downloading-and-uploading-backup-files)
    - [About the contents of incremental backup files](#about-the-contents-of-incremental-backup-files)
    - [Downloading a backup file](#downloading-a-backup-file)
    - [Uploading a backup file](#uploading-a-backup-file)

## Viewing the Change Log

Used to help with:

- To learn recent AIF update
- To determine last changed protection level during an attack
- To determine recent changes could have affected the system's operation
- To save an audit trail of system changes

### Events that create change log entries

Change log entries are created when

- Configuration changes
- Manual/automatic updates

### About exporting the change log

Save an audit trail of system changes:

- By exporting the change log to a comma-separated values (CSV) file
- By configuring AED to send change log notifications to an external system

### Viewing the complete change log

- Select Administration > Change Log
- Another method: Select Summary > Change Log tab

## Managing Diagnostics Packages

Helps the Arbor Technical Assistance Center (ATAC) to diagnose and correct any potential issues

### Creating a diagnostics package

- Select Administration > Diagnostics
- Diagnostics Packages page > Create Diagnostics Package

### Emailing a diagnostics package to ATAC

- Select Administration > Diagnostics
- Diagnostics Packages page > Choose the package to email

### Downloading a diagnostics package

- Select Administration > Diagnostics
- Diagnostics Packages page > Choose the package to download
- Follow the browser’s prompts to save the package

### Deleting diagnostics packages

- Select Administration > Diagnostics
- Select each diagnostics package or table heading row > Delete

## Managing the Files on AED

### About the file types

- Text
- Directory
- Gzip compressed
- Signed package
- SSH host keys
- Unknown

### Downloading files from AED

- Select Administration > Files
- Manage Files page > Local Files section or the System Files section > download
- Save the file according to your browser options

### Uploading local files to AED

*Note* 10 GB limit for storage of uploaded files

- Select Administration > Files
- Manage Files page > Upload File
- Upload File window > Click Choose File
- Open window > double-click the file > Upload
- Select Upload another or Close

### Deleting local files from AED

- Select Administration > Files
- Manage Files page > Local Files
- Select each file or table heading row
- Click Delete

## About Backups

### About the backup data

- Configuration data
- Traffic data
- AED does not back up any routes when vAED is deployed in layer 3

### Types of backups

- Full: All of the files
- Incremental: Only the last changed files

### About backups and password expiration

Including user account passwords and the time at which the passwords were last set in the backup

### Storing backups

- On a remote backup server
- Locally on AED

### Retention policy for backups

- AED deletes full backup that is older than the two most recent full backups
- AED deletes the oldest 6-month full backup

### About the Available Backups list

- Date and Time
- Description
- Type
- Traffic Data
- User

### Backing Up AED Manually

- Do not want schedule backups
- To save the initial system configuration.
- To save configuration data at a time that is outside the automatic backup schedule
- To save a different type of data than the what is included in the scheduled backup

### Backing up manually

- Select Administration > Backup and Restore
- Configure Backup and Restore Settings page > Back Up Now
- Manual Backup window > Back Up
  
## Restoring AED from Backups

### Data that is not restored from a backup

- The interfaces traffic data that appears in the `Interfaces section` on the `Summary page`
- The configuration data and the imported keys for the `Hardware Security Module (HSM)` and the `Cryptographic Acceleration Module (CAM)`
- Alerts and diagnostics packages
- Custom SSL certificates
- IP and network configurations

### Data restoration on AED devices

If the AED that you restore is set to a different deployment mode than the backup, the backup changes the deployment mode
on the AED

### Previous version support

Restore backups that were created in an earlier version of AED than the version

### Stopping and restarting AED during data restoration

- In bypass mode, either
network traffic passes through AED unaffected or AED is disconnected and traffic cannot pass through to the connected equipment
- Changes in the following settings can cause a restart during restoration:
  - user accounts
  - backup settings
  - DNS settings
  - NTP settings
  - SSH settings
  - system settings

### Restoring from a backup

- Select Administration > Backup and Restore
- Configure Backup and Restore Settings page > Select the backup
- Restore From Selected
- Restore AED window > Restore

### Error handling

If an error occurs during the restoration process, the configuration data is rolled back to its previous state

### Recovering from a system failure

- Reinstalling AED
- In AED, configure the backup settings to use the same remote backup server as the
failed system
- Restore the most recent backup

## How Restoring Backups Affects the AEM - Device Synchronization

### Guidelines for restoring an AEM backup

- Log in to the UI of the device
- Select Administration > General
- Configure General Settings page > clear the Arbor Enterprise Manager box and the Shared Secret box > Save
- Restore the AEM backup
- Reconnect each device

### Guidelines for restoring a device backup

The state of the connection between AEM and the device

## Downloading and Uploading Backup Files

The download and upload options are available only for local backups

### About the contents of incremental backup files

- The selected incremental backup
- All of the incremental backups between the selected incremental backup and the last full backup
- The last full backup

### Downloading a backup file

- Select Administration > Backup and Restore
- Configure Backup and Restore Settings page > Select the backup
- Download Selected
- Save the file according to your browser options

### Uploading a backup file

- Select Administration > Backup and Restore
- Configure Backup and Restore Settings page > Upload Backup
- Upload a Backup File window > Choose File > Upload
- Upload another or Close