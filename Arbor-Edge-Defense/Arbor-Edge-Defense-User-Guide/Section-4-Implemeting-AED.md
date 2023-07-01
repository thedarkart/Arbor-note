# Section 4: Implementing AED

## Table of contents

- [Section 4: Implementing AED](#section-4-implementing-aed)
  - [Table of contents](#table-of-contents)
  - [Implementing AED for Trial or Monitoring Only](#implementing-aed-for-trial-or-monitoring-only)
    - [About trial implementations](#about-trial-implementations)
    - [Trial of protection groups and the outbound threat filter](#trial-of-protection-groups-and-the-outbound-threat-filter)
    - [Required configurations](#required-configurations)
    - [Work flow](#work-flow)
    - [After the trial period](#after-the-trial-period)
  - [Implementing AED for Active Mitigation](#implementing-aed-for-active-mitigation)



## Implementing AED for Trial or Monitoring Only

### About trial implementations

- Should perform a trial implementation before you allow AED to affect your network traffic
- A trial is the same as a monitor-only implementation but it can show you how AED would block traffic, and you can adjust different protection settings to analyze how they affect the suggested mitigations
- Recommend to allow 30 to 60 days for a trial period

### Trial of protection groups and the outbound threat filter

- Situations that you might test an individual protection group after the initial implementation:
  - Introduce a new server within the data center and create a new protection group for that server
  - An existing web site is updated with a new page
  - An AED upgrade introduces new protection categories

### Required configurations

- Monitor deployment mode
- Inline deployment mode with the protection mode set to inactive

### Work flow

- Performing a trial or monitor-only implementation

  ![](IMG/2023-07-02-01-00-52.png)
  ![](IMG/2023-07-02-01-01-07.png)

### After the trial period

- Use AED in monitor-only mode: no further steps are needed.
- Begin mitigating traffic: Configure for an active implementation


## Implementing AED for Active Mitigation

-