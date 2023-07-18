# Section 28: Using the Command Line Interface (CLI)

## Table of contents

- [Section 28: Using the Command Line Interface (CLI)](#section-28-using-the-command-line-interface-cli)
  - [Table of contents](#table-of-contents)
  - [About the Command Line Interface](#about-the-command-line-interface)
    - [Prerequisite](#prerequisite)
  - [About the Connections to the Command Line Interface](#about-the-connections-to-the-command-line-interface)
    - [Options for connecting to the CLI](#options-for-connecting-to-the-cli)
    - [Serial port connection](#serial-port-connection)
    - [Terminal emulation settings](#terminal-emulation-settings)
    - [Direct monitor and keyboard connection](#direct-monitor-and-keyboard-connection)
    - [SSH connection](#ssh-connection)
  - [Logging in to and out of the AED Command Line Interface](#logging-in-to-and-out-of-the-aed-command-line-interface)
    - [Username and password](#username-and-password)
    - [Logging in to the serial port through terminal emulation](#logging-in-to-the-serial-port-through-terminal-emulation)
    - [Logging in directly to the serial port](#logging-in-directly-to-the-serial-port)
    - [Logging out of the CLI](#logging-out-of-the-cli)
  - [Getting Help in the CLI](#getting-help-in-the-cli)
    - [Types of Help commands](#types-of-help-commands)
  - [About the CLI Command Components](#about-the-cli-command-components)
    - [Components of CLI commands](#components-of-cli-commands)
    - [Conventions for commands and expressions](#conventions-for-commands-and-expressions)
  - [Entering CLI Commands](#entering-cli-commands)
    - [Command types](#command-types)
    - [Entering a command](#entering-a-command)
    - [Guidelines for typing commands](#guidelines-for-typing-commands)
    - [Saving the configuration](#saving-the-configuration)
  - [Navigating the CLI Command Hierarchy](#navigating-the-cli-command-hierarchy)
    - [Navigating the CLI hierarchy](#navigating-the-cli-hierarchy)
  - [Viewing Statuses in the CLI](#viewing-statuses-in-the-cli)
    - [Viewing the status of the current directory](#viewing-the-status-of-the-current-directory)
    - [Viewing the current configuration](#viewing-the-current-configuration)

## About the Command Line Interface

To access the AED CLI, connecting to the AED directly or remotely

### Prerequisite

Must complete the initial installation and
configuration procedures

## About the Connections to the Command Line Interface

### Options for connecting to the CLI

- Serial port
  - Serial console server
  - Compute
- VGA connector with monitor
- USB port with keyboard
- Management port mgt0 with SSH

### Serial port connection

- Connecting a computer directly to the serial port on the AED appliance
- Connecting a serial console to the serial port on the AED appliance, and using a terminal emulator to access the CLI

### Terminal emulation settings

- Baud rate
- Data bits
- Stop bits
- Parity
- Flow control

### Direct monitor and keyboard connection

- Connecting a monitor and keyboard to the VGA and USB ports respectively
- The boot commands are available

### SSH connection

- Accessing the AED appliance by using a network protocol such as SSH
- The SSH service is enabled by default
- The boot commands are not available

## Logging in to and out of the AED Command Line Interface

Performing advanced configurations and other tasks with CLI

### Username and password

Username is configured when installed AED or default is `admin`

### Logging in to the serial port through terminal emulation

- Connect with the AED serial port
- Select disk
- Enter username and password

### Logging in directly to the serial port

- Connect with the IP address or DNS
hostname for AED as needed
- Enter username and password

### Logging out of the CLI

In the CLI, enter `/ exit`

## Getting Help in the CLI

### Types of Help commands

- help: all available commands within a directory
- help global: all available commands from all directories
- ?: all available commands within a directory or the arguments that are available within a command

## About the CLI Command Components

### Components of CLI commands

The CLI command syntax is `command keyword argument` parameter

### Conventions for commands and expressions

Do not type the brackets, braces, or vertical bars that indicate options and variables

## Entering CLI Commands

### Command types

- Sub commands: specific to the current directory
- Global: available anywhere in the command
hierarchy

### Entering a command

Type the command, and then press `ENTER`

### Guidelines for typing commands

- The commands are case sensitive
- Can minimize typing like `sy` instead of `system` or using `TAB` to complete commmands
- Multiple commands into one compound command

### Saving the configuration

From anywhere within the CLI, enter `/ config write`

## Navigating the CLI Command Hierarchy

### Navigating the CLI hierarchy

- One or more directory commands: Navigating the CLI hierarchy
- `..`: back up one level
- `/`: return to the root directory

## Viewing Statuses in the CLI

### Viewing the status of the current directory

Enter `show`

### Viewing the current configuration

From anywhere within the CLI, enter `config show`

