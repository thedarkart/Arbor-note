# Section 7: Getting Started with AED


## Table of contents

- [Section 7: Getting Started with AED](#section-7-getting-started-with-aed)
  - [Table of contents](#table-of-contents)
  - [Logging in to and out of the UI](#logging-in-to-and-out-of-the-ui)
    - [Prerequisites](#prerequisites)
    - [Logging in as a new user](#logging-in-as-a-new-user)
    - [About the SSL certificate for secure sessions](#about-the-ssl-certificate-for-secure-sessions)
    - [Logging in to the AED  UI](#logging-in-to-the-aed--ui)
    - [Logging out of the AED UI](#logging-out-of-the-aed-ui)
  - [Navigating the AED UI](#navigating-the-aed-ui)
    - [About the UI menu bar](#about-the-ui-menu-bar)
    - [About the Arbor Smart Ba](#about-the-arbor-smart-ba)
    - [Using Help](#using-help)
    - [Navigating multiple pages](#navigating-multiple-pages)
    - [Searching for data](#searching-for-data)
  - [Saving and Emailing Pages from the UI](#saving-and-emailing-pages-from-the-ui)
    - [Exporting a page as a CSV fil](#exporting-a-page-as-a-csv-fil)
    - [Saving a page as a PDF file](#saving-a-page-as-a-pdf-file)
    - [Emailing a page as a PDF file](#emailing-a-page-as-a-pdf-file)
  - [Viewing Graphs in the UI](#viewing-graphs-in-the-ui)
    - [About stacked graphs](#about-stacked-graphs)
    - [About minigraphs](#about-minigraphs)
    - [Changing the display timeframe](#changing-the-display-timeframe)
    - [Changing the display unit of measure](#changing-the-display-unit-of-measure)

## Logging in to and out of the UI

### Prerequisites

- Must complete the initial installation and configuration procedures
- Set your browser preferences to allow pop-ups and accept cookies from AED

### Logging in as a new user

### About the SSL certificate for secure sessions

- AED UI uses the HTTPS protocol for secures sessions
- In the first time you access the AED UI, accept the SSL certificate to complete the connection
    - Can upload a custom certificate and its certificate authority (CA) file to comply with your company's security policies and prevent browser errors

### Logging in to the AED  UI

- `http://<IP address of you AED appliance`

### Logging out of the AED UI

## Navigating the AED UI

### About the UI menu bar

- **Summary**: Display the current health of AED and provides traffic forensics in real time
- **Explore**: Allows you to display information about the traffic that AED monitors and mitigates
- **Protect**: Allow to view, configure, and menage protection groups
- **Administration**: Allows to configure and maintain AED

### About the Arbor Smart Ba

- Allow you to take certain actions on the current page

### Using Help

-  Read about the functions that are available on the current AED page
-  View related topics
-  Scroll through the table of contents for the User Guide
-  Search for topics in the User Guide

### Navigating multiple pages

### Searching for data

## Saving and Emailing Pages from the UI

### Exporting a page as a CSV fil

- Only available for certain pages only (Blocked Hosts Log page,..)
- `Arbor Smart bar > CSV Export icon`

### Saving a page as a PDF file

- `Arbor Smart bar > Create a PDF icon`

### Emailing a page as a PDF file

- `Administration > General`
  - Must configure an SMTP server
  - Necessary settings
    - **From Address** - the sender of the email messages (default: username@hostname)
    - **Default URL Hostname** 

- Emailing a UI page
  - `Arbor Smart Bar > Email this page icon`
    - Email to box
    - Comment box
  - `Send Email` 

## Viewing Graphs in the UI

- AED uses graphs to represent your organization's traffic in real time

### About stacked graphs

- See specific types of graph data more clearly
- Each data type has its own color-coded segment
- The height of the stack segment represents that segments's data as a percentage of the total data

### About minigraphs

- Allow to see a small representation of graph data

### Changing the display timeframe

- The timeframe can represent a specific time increment or a time range

### Changing the display unit of measure

- Can display the traffic data in terms of bytes or packets

