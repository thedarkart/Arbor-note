# Section 26: Managing and Viewing Reports

## Table of contents

- [Section 26: Managing and Viewing Reports](#section-26-managing-and-viewing-reports)
  - [Table of contents](#table-of-contents)
  - [Executive Summary Report](#executive-summary-report)
    - [Top hosts data](#top-hosts-data)
    - [Outbound traffic data](#outbound-traffic-data)
    - [Information](#information)
      - [Report header and footer](#report-header-and-footer)
        - [Header](#header)
        - [Footer](#footer)
      - [Cloud Signaling](#cloud-signaling)
      - [DDoS Protection](#ddos-protection)
        - [Inbound Traffic](#inbound-traffic)
        - [Outbound Traffic](#outbound-traffic)
      - [Top Inbound Countries](#top-inbound-countries)
      - [Top Blocked Threat Categories](#top-blocked-threat-categories)
      - [Top Inbound Sources](#top-inbound-sources)
      - [Top Inbound Destination](#top-inbound-destination)
  - [ATLAS Global DDoS Report](#atlas-global-ddos-report)
    - [Configuring On-Demand Reports](#configuring-on-demand-reports)
    - [Requirements for emailing the reports](#requirements-for-emailing-the-reports)
    - [Configuring an on-demand report](#configuring-an-on-demand-report)
    - [Setting a custom date range](#setting-a-custom-date-range)
  - [Configuring and Editing Scheduled Reports](#configuring-and-editing-scheduled-reports)
    - [Requirements for emailing the reports](#requirements-for-emailing-the-reports-1)
    - [Configuring or editing a scheduled report](#configuring-or-editing-a-scheduled-report)
  - [Viewing and Deleting Generated Reports](#viewing-and-deleting-generated-reports)
    - [Searching for generated reports](#searching-for-generated-reports)
    - [Viewing report results](#viewing-report-results)
    - [Deleting generated reports](#deleting-generated-reports)
  - [Viewing and Deleting Scheduled Reports](#viewing-and-deleting-scheduled-reports)
    - [Searching for scheduled reports](#searching-for-scheduled-reports)
    - [Deleting scheduled reports](#deleting-scheduled-reports)


## Executive Summary Report

- Providing information about the detected and blocked attacks
- Providing information about high-level traffic trends

### Top hosts data

- The top hosts is based on all of the traffic for the AED
- Enable `Top sources and destinations` tracking

### Outbound traffic data

- Enable the outbound threat filter
- Including IPv4 traffic data only

### Information

#### Report header and footer

##### Header

- Report name
- AED name
- Description
- Date range

##### Footer

- The user name
- The date and time
- Explanations

#### Cloud Signaling

- Events Mitigated shows the number of unique DDoS attacks that were mitigated
- Targeted IPs Protected shows the number of hosts in your network that AED protected from DDoS attacks by using cloud-based mitigation

#### DDoS Protection

##### Inbound Traffic

- The amount of blocked inbound traffic in bytes
- The percentage inbound traffic that was blocked compared to the total inbound traffic
- The number of unique blocked hosts
- A stacked graph displays the amount of blocked inbound traffic versus passed inbound traffic
- The average daily amount of total inbound traffic, blocked inbound traffic, and passed inbound traffic
- The average rate of total inbound traffic, blocked inbound traffic, and passed inbound traffic is provided in **bps**

##### Outbound Traffic

- Including information for all protection groups
- It mentions the amount of *blocked outbound traffic* in **bytes**
- The percentage blocked of outbound traffic that was compared to the total outbound traffic
- The number of unique blocked hosts
A stacked graph displays the amount of blocked outbound traffic versus passed outbound traffic
- The average daily amount of total outbound traffic, blocked total traffic, and passed outbound traffic
- The average rate of total outbound traffic, blocked outbound traffic, and passed outbound traffic is provided in bps
- Omitting the outbound traffic section while no outbound traffic is available
- Including `IPv4` traffic data only

#### Top Inbound Countries

- A *flag icon* representing each country and *IPv6 flag*
- A stacked graph shows the total passed traffic (in green) and total blocked traffic (in red) for each country
- Amount of traffic from each country that was passed and blocked in **bps and pps**
- The percentage of the total traffic that each country's traffic represents
- The proportion bar for the top country occupies the full column width, while the remaining bars are proportional to it

#### Top Blocked Threat Categories

Including five threat categories in the `ATLAS Intelligence Feed` that blocked the most traffic:

- The amount of blocked inbound traffic
- The amount of blocked outbound traffic
- A key for each graph that shows the color that represents a specific threat category in the graph
- The name of the threat category that blocked the traffic

#### Top Inbound Sources

- Based on all of the traffic for the `AED`
- Including the following information about the five external IP addresses that sent the most traffic:
  - The IP address for the source host, available flag icon and IPv6 flag.
  - Total traffic from the source
  - The total amount of traffic from the source, in bytes and packets
  - The average rate of traffic from the source, in bps and pps

#### Top Inbound Destination

- The data for Top Inbound Destinations is based on all of the traffic for the AED.
- Including information about the five internal IP addresses groups that received the most traffic:
  - The IP address to which the traffic is destined
  - A graph that represents the total traffic to the destination
  - The total amount of traffic to the destination, in bytes and packets
  - The average rate of traffic to the destination, in bps and pps

## ATLAS Global DDoS Report

Show the scope of internal threats to your network in the context of other networks and the internet

Keyword:

- Arbor Security Engineering and Response Team (ASERT)
- ATLAS Intelligence Feed (AIF)

View and download:

- Select Administration > ATLAS Intelligence Feed
- On the Configure AIF Settings page, select the `Enable Automated Connection to AIF check box`
- Select the Yes, I want to opt in to Arbor's data-sharing program check box
- Click Save
- Select Reports > ATLAS Global DDoS

### Configuring On-Demand Reports

- Providing information about the attacks
that AED detected and blocked on your network over time
- Scheduled to run one time or multiple times in the future
- View as PDF, Web page

### Requirements for emailing the reports

Configure an `SMTP server` on the `Configure General Settings` page (Administration > General)

### Configuring an on-demand report

- Select Reports > Executive Summary.
- Executive Summary Reports page > Configure New Report.
- Select a date range for the data:
  - Select a predefined timeframe, select Quick Date Range, Days, Weeks, or Months
  - The report includes data for complete days, weeks, or months only
  - Timeframe for the data and AED generates the report on April 10, the report includes the data for February and March only or specify a custom timeframe, select Custom Date Range > Select a start date
- Select the protection groups > select at least one protection group
- In the Report Name box, type a unique name for the report
- Click Submit

### Setting a custom date range

- Create New Report wizard
- Pick a start date and an end date
- The timeframe for the report starts at 12:00 am on the selected start date and ends at 11:59:59 pm on the selected end date

## Configuring and Editing Scheduled Reports

- Providing information about the attacks that AED detected and blocked on your network over time
- To edit a scheduled report, click the report name to access the configuration settings
- View the results as web page or PDF

### Requirements for emailing the reports

Configure an `SMTP server` on the `Configure General Settings` page (Administration > General)

### Configuring or editing a scheduled report

- Select Reports > Executive Summary
- Executive Summary Reports page > Schedules tab
- Configure New Report Schedule
- Select the number of days, weeks, or months and specific complete days, weeks, or months of data including in the report
- Select start date to generate the first report
- Select the `Repeat check box` to run the report multiple times
- Select frequency of the report in the `Every box`
- Select protection groups
- Type a unique name for the report in the `Name box`
- Select Submit

## Viewing and Deleting Generated Reports

### Searching for generated reports

- Select Reports > Executive Summary
- Search for reports by partial name of reports or person in `Search box`
- To clear the search, delete all of the text in the Search box

### Viewing report results

- Select Reports > Executive Summary
- View the report in default web browser or export to PDF

### Deleting generated reports

- Select Reports > Executive Summary
- Select each report or Name column to delete
- Click (context menu) to the right of a report name and select Delete

## Viewing and Deleting Scheduled Reports

### Searching for scheduled reports

- Reports > Executive Summary > Schedules tab
- Search for reports by partial name of report or person in `Search box`
- To clear the search, delete all of the text in the Search box
  
### Deleting scheduled reports

- Reports > Executive Summary > Schedules tab
- Select each report or Name column to delete
- Click (context menu) to the right of a report name and select Delete