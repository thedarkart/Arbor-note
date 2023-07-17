# Section 5: Configuring User Groups and Authentication

## Table of contents

- [Section 5: Configuring User Groups and Authentication](#section-5-configuring-user-groups-and-authentication)
  - [Table of contents](#table-of-contents)
  - [About User Authentication](#about-user-authentication)
    - [About local user account](#about-local-user-account)
    - [About access to local user account](#about-access-to-local-user-account)
    - [How authentication works with RADIUS and TACACS+](#how-authentication-works-with-radius-and-tacacs)
    - [About the AED user groups in RADIUS](#about-the-aed-user-groups-in-radius)
    - [Integrating AED with RADIUS or TACACS+](#integrating-aed-with-radius-or-tacacs)
  - [About User Groups](#about-user-groups)
    - [About authorization keys](#about-authorization-keys)
    - [Predefined groups](#predefined-groups)
    - [Custom user groups](#custom-user-groups)
  - [Adding and Deleting User Groups](#adding-and-deleting-user-groups)
    - [Adding a user group](#adding-a-user-group)
    - [Copying a user group](#copying-a-user-group)
    - [Deleting a user group](#deleting-a-user-group)
  - [Assigning Authorization Keys to User Group](#assigning-authorization-keys-to-user-group)
    - [Adding and deleting authorization keys](#adding-and-deleting-authorization-keys)
    - [Viewing the group authorization keys](#viewing-the-group-authorization-keys)
    - [User group authorization keys](#user-group-authorization-keys)
  - [Configuring the User Accounting Level](#configuring-the-user-accounting-level)
    - [Configuring the accounting level](#configuring-the-accounting-level)
  - [Configuring Password Requirements for Local User Accounts](#configuring-password-requirements-for-local-user-accounts)
    - [Before you enable password expiration](#before-you-enable-password-expiration)
    - [Enabling or disabling password expiration](#enabling-or-disabling-password-expiration)
    - [Enabling or disabling the password expiration warning message](#enabling-or-disabling-the-password-expiration-warning-message)
    - [Changing the required password length](#changing-the-required-password-length)
    - [About the complexity mode for password](#about-the-complexity-mode-for-password)
      - [Changing the complexity mode](#changing-the-complexity-mode)
      - [Viewing the password requirement settings](#viewing-the-password-requirement-settings)
  - [Adding and Editing Local User Accounts](#adding-and-editing-local-user-accounts)
    - [Adding accounts for users that manage AED devices on AEM](#adding-accounts-for-users-that-manage-aed-devices-on-aem)
    - [Adding local user accounts](#adding-local-user-accounts)
    - [Editing local user accounts](#editing-local-user-accounts)
    - [Deleting local user accounts](#deleting-local-user-accounts)
    - [Local user account settings](#local-user-account-settings)
    - [When to change your password](#when-to-change-your-password)
    - [Password requirements](#password-requirements)
  - [Setting the Authentication Method for RADIUS and TACACS+](#setting-the-authentication-method-for-radius-and-tacacs)
    - [About the default user group](#about-the-default-user-group)
    - [Setting the authentication method](#setting-the-authentication-method)
    - [Setting an exclusive authentication method](#setting-an-exclusive-authentication-method)
    - [Configuring the accounting levels](#configuring-the-accounting-levels)
  - [Setting the AED User Group for RADIUS Users](#setting-the-aed-user-group-for-radius-users)
  - [Setting the AED User Group for TACACS+ Users](#setting-the-aed-user-group-for-tacacs-users)
  - [Changing the Default User Group for RADIUS and TACACS+](#changing-the-default-user-group-for-radius-and-tacacs)
    - [Changing the default user group](#changing-the-default-user-group)
  - [Configuring RADIUS Integration](#configuring-radius-integration)
    - [About the authentication server](#about-the-authentication-server)
    - [Adding a RADIUS server](#adding-a-radius-server)
    - [Setting the number of retries and the timeout period](#setting-the-number-of-retries-and-the-timeout-period)
    - [Configuring a Network Access Server identifier](#configuring-a-network-access-server-identifier)
    - [Clearing the NAS identifier](#clearing-the-nas-identifier)
    - [Viewing the current RADIUS configuration](#viewing-the-current-radius-configuration)
  - [Configuring TACACS+ Integration](#configuring-tacacs-integration)
    - [Adding a TACACS+ server](#adding-a-tacacs-server)
    - [Setting the timeout period](#setting-the-timeout-period)
    - [Reverting to the default timeout period](#reverting-to-the-default-timeout-period)
    - [Configuring password expiration notifications](#configuring-password-expiration-notifications)
    - [Viewing the current TACACS+ configuration](#viewing-the-current-tacacs-configuration)



Administrators who have the `srv_aaa authorization key` can complete all of the actions
that are described in this section.

## About User Authentication

- Each unique user account contains:
  - The user's login credentials
  - The levels of access that the user is allowed

- User authentication methods:
  - Local
  - RADIUS (Remote Authentication Dial In User Service)
  - TACACS+ (Terminal Access Controller Access-Control System Plus)

- Provide access to the CLI through SSH and to the user interface (UI) through HTTPS

### About local user account

- Can add, edit, and delete the local user accounts in the UI or the CLI
- The AED installation creates a user account named "admin" in system_admin group

### About access to local user account

- Administrators can creation, modification and deletion of user accounts and groups.
- Non-administrative users only have access to a view of the user account

### How authentication works with RADIUS and TACACS+

- AED can integrate with the RADIUS service or TACACS+ service for centralized user authentication

- When a RADIUS user or TACAS+ user logs in to AED
  - AED connects to the primary authentication server that you designated
  - If the server can authenticate
    - Sends the AED user group 
    - AED logs in the user with the access permissions that are associated with the user group
  - If the server does not respond
    - AED tries to connect to  the backup server
    - if AED cannot reach either of the designated servers
      - AED tries to authenticates the user locally


### About the AED user groups in RADIUS

- Need to define an AED user group on the appropriate authentication server
- Any user who is not assigned to a user group on the authentication server is assigned to the predefined system_user group in AED

### Integrating AED with RADIUS or TACACS+

- Process for integrating AED with RADIUS or TACACS+
  - Step 1: Set the user group for the AED users on the RADIUS/TACACS+ server 
  - Step 2: Change the default AED user group for RADIUS/TACACS+ users 
  - Step 3: Configure AED to access the authentication server and an optional backup server for RADIUS or TACACS+
  - Step 4: Set the authentication method
  - Step 5: (optional) Configure the user accounting level

## About User Groups

- Allow to organize AED users by the different levels of system access that the users are allowed
- The Owner of the account inherits the access levels that are assigned to the user group

### About authorization keys

- Determine the level of sytem access that is granted to the users in the group

### Predefined groups

![](IMG/2023-07-14-19-37-55.png)

### Custom user groups

- Administrators can define custom user groups in the CLI

## Adding and Deleting User Groups

### Adding a user group

- with `name` is the group name:
`/ services aaa groups add name`

- Save: `/ config write`

### Copying a user group

- `/ services aaa groups copy existingGroup newGroup`
- Save: `/ config write`

### Deleting a user group

- `/ services aaa groups delete name`
- Enter `y` at the confirmation prompt
- Save: `/ config write`

## Assigning Authorization Keys to User Group

- Determine the level of access
that is granted to the users in that group

### Adding and deleting authorization keys

- `/ services aaa groups key {add | delete} name key`
- Save: `/ config write`

### Viewing the group authorization keys

- ` / services aaa groups show name`

### User group authorization keys

![](IMG/2023-07-14-19-48-39.png)

![](IMG/2023-07-14-19-48-52.png)

![](IMG/2023-07-14-19-49-07.png)

![](IMG/2023-07-14-19-49-16.png)

## Configuring the User Accounting Level

- Determines whether AED logs the following user acitvites to the local syslog:
  - software logins
  - configuration changes
  - interactive commands

- This logging applies to activities in the AED CLI only

### Configuring the accounting level

- `/ services aaa {local | radius | tacacs} accounting set level
{none | login | change | commands}`
    - `none` — (default) disables account logging
    - `login` — tracks log ins to AED
    - `change` — (TACACS+ only) tracks configuration changes
    - `commands` — (TACACS+ only) tracks the use of CLI commands
- Save: `/ config write`

## Configuring Password Requirements for Local User Accounts

- The password requirements 
  - Password Expiration
  - Warning messages for password expiration
  - Password length
  - Password complexity

### Before you enable password expiration

- By default, password expiration is not exist
- Should reset the passwords for all user accounts before you enable password expiration

### Enabling or disabling password expiration

- View the current password expiration setting: `/ services aaa local policy expiration`
- Change the password expiration setting: `/ services aaa local policy expiration set days`
  - **days**: a number from 1 to 365
- If you want to disable password expiration:
  - `/ services aaa local policy expiration clear`
  - `/ services aaa local policy expiration set 0`
- Save: `/ config write`

### Enabling or disabling the password expiration warning message

- Can configure AED to display a warning message before a password expires
- View: `/ services aaa local policy expiration warning`
- Set the time frame: `/ services aaa local policy expiration warning set days`
  - **days** is a number from 1 to 30 (number of days before the password expires that the warning message starts to appear)
- (Disable):
  - `/ services aaa local policy expiration warning clear`
  - `/ services aaa local policy expiration warning set 0`
- Save: `/ config write`

### Changing the required password length

- Default: Minium length is 10 and maximum length is 72
- View: `/ services aaa password_length`
- Specify the password length: `r / services aaa password_length {min minValue | max maxValue}`
- Reset to the default minium length and maximum length: `/ services aaa password_length {min | max} reset_default`
- Save: `/ config write`

### About the complexity mode for password

- The character types:
  - uppercase letters
  - lowercase letters
  - numbers
  - symbols

- The character mix requirement
  - Uppercase cannot be at the start
  - Numbers cannot be at the end
  - Symbols cannot be at the ent 

#### Changing the complexity mode

- View: `/ services aaa local policy complexity`
- Change the complexity mode: `/ services aaa local policy complexity {standard | advanced}`
  - **Standard**: Password must contain at least two character types
  - **Advanced**: Password must contain four character types
- Save: `/ config write`


#### Viewing the password requirement settings

- View all the authentication, authorization, and accounting settings: `/ services aaa show`
- View the settings for local user accounts: `/ services aaa local show`

## Adding and Editing Local User Accounts

### Adding accounts for users that manage AED devices on AEM

- Use the same username in both AEM and AED can help you to open a managed AED from AEM without having to log in to AED

### Adding local user accounts

- `Administration > User Accounts > Add Account > Add New Account`
- Configure the settings and Click `Create Account`

### Editing local user accounts

- `Administration > User Accounts`
- If you are a non-administrative user, use `Edit Account` page 

### Deleting local user accounts

### Local user account settings

- Administrators can edit any of the user account settings except the username

- Settings for local user account
  - Username box
  - Real name box
  - Email box
  - Time zone list
  - Password box

### When to change your password

- After the first time you log in to the AED
- When your system administrator recommends
- Before your password expires, if password expiration is configured.
- ...

### Password requirements

- Password length
- Number of character types
- Character mix

## Setting the Authentication Method for RADIUS and TACACS+

### About the default user group

- By default, any user who is not assigned to a user group on the RADIUS or TACACS+ server is assigned to the predefined system_user group in AED

### Setting the authentication method

- `/ services aaa method set{local | radius | tacacs}`
  - {local | radius | tacacs} = Methods that AED should use to authenticate (type a space between each method)

### Setting an exclusive authentication method

- When you set multiple authentication methods, but want a user to log in with one method
only
- `/ services aaa method exclusive enable`

### Configuring the accounting levels

- Use local and TACACS+ accounting settings for each authentication to track and log software logins. configuration changes, and interactive commands.
- Use RADIUS accounting to track software logins

- `/ services aaa {local | radius | tacacs} accounting set level {none | login | change | commands}`

## Setting the AED User Group for RADIUS Users

- Set the AED user group for RADIUS users on the RADIUS server
  - Set an `Arbor-Privilege-Level` attribute that has the user group name as its value
    - `Arbor-Privilege-Level = system_user`
    - `Arbor-Privilege-Level = system_none`
    - For the RADIUS server to interpret the `Arbor-Privilege-Level` attribute
      - `VENDOR Arbor 9694
        ATTRIBUTE Arbor-Privilege-Level 1 string Arbor`

## Setting the AED User Group for TACACS+ Users

- Set an `arbor` service with an `arbor_group` attribute that has the user group name as its value
  - Example:
    - `service = arbor { arbor_group = system_user }`
    - `service = arbor { arbor_group = system_user }`

## Changing the Default User Group for RADIUS and TACACS+

- Deny AED access to RADIUS users or TACACS+ users with no group assignment
  - Change the default group to `system_none`

### Changing the default user group

- `/ services aaa groups default set groupName`
- Save: ` / config write`

## Configuring RADIUS Integration

### About the authentication server

- Can integrate AED with a primary server and a backup server

### Adding a RADIUS server

- To add a RADIUS server: 
  - `/ services aaa radius server set {primary | backup} IP_address {encrypted | unencrypted} secret [port]`
    - secret = The secret that AED uses to communicate with the authentication server. For security purposes, use a secret that contains a variety of characters
    - The default RADIUS port is 1812

### Setting the number of retries and the timeout period

- `/ services aaa radius retries set number`
  - `number`: Number of times (1-60) that AED tries to authenticate after the first attempt fails
- `/ services aaa radius timeout set number`
  - `number`: Number of seconds (1-60) that AED waits for a connection before it tries the backup server

### Configuring a Network Access Server identifier

- A string that identifies the NAS that originates an access request
  - `/ services aaa radius nas_identifier set string`
    - ASCII strings (up to 253 characters)

### Clearing the NAS identifier

- `/ services aaa radius nas_identifier clear`

### Viewing the current RADIUS configuration

- `/ services aaa radius show`

## Configuring TACACS+ Integration

### Adding a TACACS+ server

- `/ services aaa tacacs server set {primary | backup} IP_address port{encrypted | unencrypted} secret`
  - Must specify a TCP port

### Setting the timeout period

- `/ services aaa tacacs timeout set number`

### Reverting to the default timeout period

- `/ services aaa tacacs timeout clear`

### Configuring password expiration notifications

- `/ services aaa tacacs tacpass_expiry_notify {enable | disable} `

### Viewing the current TACACS+ configuration

- `/ services aaa tacacs show`