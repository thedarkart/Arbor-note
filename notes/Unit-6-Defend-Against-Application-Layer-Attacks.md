# Unit 6: Defend Against Application Layer Attack

## Table of contents

- [Unit 6: Defend Against Application Layer Attack](#unit-6-defend-against-application-layer-attack)
  - [Table of contents](#table-of-contents)
  - [Protecting Web Servers](#protecting-web-servers)
    - [Application Attacks to Web Servers](#application-attacks-to-web-servers)
    - [Slowloris - Slow HTTP GET DDoS](#slowloris---slow-http-get-ddos)
    - [R.U.D.Y - Slow HTTP POST DDoS](#rudy---slow-http-post-ddos)
    - [Protecting Web Servers](#protecting-web-servers-1)

## Protecting Web Servers

### Application Attacks to Web Servers

- Get Floods
- Slow GET
- Slow POST

### Slowloris - Slow HTTP GET DDoS

- Take down a web server with minimal bandwidth and side effects on unrelated services and ports to hold open as many connections as possible to the `HTTP server`
- Abuse handling of `HTTP request headers` slowly, high impact and relatively low bandwidth usage

### R.U.D.Y - Slow HTTP POST DDoS

- Uses HTTP POST requests
- Abuses HTTP web form fields
- Iteratively injects one custom byte into a web application post field and goes to sleep

### Protecting Web Servers

- Attack Protections for HTTP traffic
- Malformed HTTP Filtering
- Application Misbehavior
- Botnet Prevention
- Spoofed SYN Flood Prevention
- HTTP Rate Limiting
- HTTP Header Regular Expression
- Web Crawler Support