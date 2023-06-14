# Unit 2: Automate Mitigations

## Table of contents

- [Unit 2: Automate Mitigations](#unit-2-automate-mitigations)
  - [Table of contents](#table-of-contents)
  - [Auto-Mitigation](#auto-mitigation)
    - [Mitigation Hierarchy](#mitigation-hierarchy)
    - [Configure](#configure)
    - [Multi-Layer Defense](#multi-layer-defense)
      - [Situation 1: TMS Mitigation only](#situation-1-tms-mitigation-only)
      - [Situation 2: TMS \& FS Mitigation](#situation-2-tms--fs-mitigation)
      - [Situation 3: BH Mitigation - To upstream carrier protecting peering](#situation-3-bh-mitigation---to-upstream-carrier-protecting-peering)

## Auto-Mitigation

### Mitigation Hierarchy

Unique assignment using the longest match

### Configure

- `Global TMS Mitigation` Settings: Administration > Mitigation > Global Settings  
- `Auto-Mitigation Settings`: Administration > Monitoring > Managed Objects
- `TMS`: Use the `Threat Mitigation System` to stop the attack
- `IPv4 Blackhole`: Only signal a `BGP Blackhole` route to the network and suppress traffic
- `TMS + IPv4 Blackhole`: Use the `Threat Mitigation System` to stop the attack till
the attack size exceeds a threshold and then the system will signal an additional
BGP Blackhole route to the network and suppress traffic
- End `TMS Auto-Mitigation` allow automatic end
- Do not use complete MO IP space, instead identify top attacked prefix
- Mitigation: `TMS only`
  - Reuse allows protection prefixes to be
added to a running mitigation, avoiding to start a new mitigation
- Mitigation: `IPv4 Blackhole only`
  - Specify BGP Communities
  - Select Nexthop to be used on advertisement
  - Select routers that should receive BGP Blackhole route
- Mitigation: `TMS & IPv4 Blackhole`
  - Threshold (over all involved TMS) that need and/or to be exceeded
  - Configure Communities and select nexthop
  - Routers that will receive the BGP Blackhole route
- Mitigation: `FlowSpec by Misuse Type`
  - Auto-Flowspec advertisements for known Host Misuse Types 

### Multi-Layer Defense

#### Situation 1: TMS Mitigation only

![](https://i.ibb.co/4FLQ2WF/Screenshot-2023-06-14-135135.png)

#### Situation 2: TMS & FS Mitigation

![](https://i.ibb.co/2nGX07R/Screenshot-2023-06-14-135511.png)

#### Situation 3: BH Mitigation - To upstream carrier protecting peering

![](https://i.ibb.co/qmyMmzh/Screenshot-2023-06-14-135748.png)
