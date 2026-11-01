# Enterprise-SOC-Dashboard
# Enterprise SOC Dashboard Using Splunk

**A Practical SIEM-Based Approach to Windows Endpoint Monitoring and Threat Detection**

## Project Overview

The Enterprise SOC Dashboard is a cybersecurity monitoring project designed to collect, analyze, and visualize Windows endpoint security events using Splunk Enterprise.

The project uses Sysmon and Windows Event Logs to monitor endpoint activities. Splunk Universal Forwarder collects and forwards the logs to a centralized Splunk Enterprise instance for security monitoring and investigation.

The goal is to demonstrate how a Security Operations Center (SOC) can monitor endpoint activities and investigate potentially suspicious behavior using centralized security logs.

## Architecture

```text
       Azure Windows VM
              |
       +------+------+
       |             |
     Sysmon     Windows Logs
       |             |
       +------+------+
              |
       Splunk Universal
          Forwarder
              |
          Tailscale
       Private Network
              |
              v
       Splunk Enterprise
        (Windows Laptop)
              |
       +------+------+
       |             |
   SPL Queries   SOC Dashboard
       |             |
       +------+------+
              |
      Security Monitoring
       and Investigation
```

## Technologies Used

| Technology | Purpose |
|---|---|
| Microsoft Azure | Hosts the Windows monitoring VM |
| Windows Server | Endpoint operating system |
| Sysmon | Detailed endpoint activity monitoring |
| Splunk Universal Forwarder | Log collection and forwarding |
| Splunk Enterprise | Centralized log analysis and visualization |
| Tailscale | Private network connectivity |
| SPL | Security event searching and analysis |
| PowerShell | Endpoint administration and testing |

## Implemented Features

- Azure-based Windows endpoint monitoring.
- Sysmon installation and event collection.
- Windows event log forwarding.
- Splunk Universal Forwarder configuration.
- Private connectivity using Tailscale.
- Splunk receiving port configuration (9997).
- Centralized Sysmon event indexing.
- Custom SOC Command Center dashboard.
- Process creation event monitoring.
- Network connection event monitoring.
- Event activity visualization.
- Latest endpoint activity investigation.

## Dashboard Components

The SOC Command Center includes:

1. Total Sysmon Events
2. Process Creation Events
3. Network Connection Events
4. Sysmon Event Activity Trend
5. Latest Endpoint Security Activity

## Sample SPL Queries

**Total Sysmon Events**

```spl
index="sysmon" earliest=-24h
| stats count AS "Total Sysmon Events"
```

**Process Creation Monitoring**

```spl
index="sysmon" earliest=-24h
| rex field=_raw "<EventID>(?<EventCode>\d+)</EventID>"
| search EventCode=1
| stats count AS "Process Creations"
```

**Network Connection Monitoring**

```spl
index="sysmon" earliest=-24h
| rex field=_raw "<EventID>(?<EventCode>\d+)</EventID>"
| search EventCode=3
| stats count AS "Network Connections"
```

## Implementation Results

The project successfully established connectivity between the Azure Windows VM and the local Splunk Enterprise instance.

The Universal Forwarder showed an active forwarding destination at port 9997, and Sysmon events were indexed in Splunk.

A SOC Command Center dashboard was created to visualize collected endpoint telemetry.

## Future Enhancements

- Threat intelligence feed integration.
- Malicious IP and domain correlation.
- Advanced PowerShell threat detection.
- Automated security alerts.
- Incident investigation and response workflow.
- Additional Windows security event monitoring.

## Project Objectives

- Understand practical SIEM implementation.
- Develop endpoint monitoring capabilities.
- Learn SPL-based security event analysis.
- Demonstrate centralized security monitoring.
- Explore threat detection and threat intelligence enrichment.

## Disclaimer

This project is developed for educational, academic, and cybersecurity research purposes. Test activity and detection patterns are used to demonstrate monitoring capabilities. Detection candidates should be investigated before being classified as security incidents.

Threat intelligence integration and automated response are planned enhancements, not currently claimed as completed features.

## Author

**GitHub:** [GTRR3530](https://github.com/GTRR3530)

**Project:** Enterprise SOC Dashboard Using Splunk

**Domain:** Cybersecurity | Security Operations Center | SIEM

---

*Developed as an academic cybersecurity project.*
