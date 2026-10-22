# SOC Alert Monitoring & Log Correlation

## Project Overview

This project demonstrates a basic Security Operations Center (SOC) monitoring workflow using Splunk SIEM. It collects Windows security logs, detects repeated failed login attempts, and generates scheduled alerts.

## Objectives

- Collect Windows security logs and forward them to Splunk.
- Monitor failed login attempts.
- Create a correlation rule to identify repeated failures.
- Configure and test scheduled alerts.
- Build a dashboard for security monitoring.

## Tools & Technologies

- Splunk Enterprise (SIEM)
- Splunk Universal Forwarder
- Windows 10
- Sysmon
- Kali Linux
- Oracle VirtualBox

## System Architecture

Windows 10 → Splunk Universal Forwarder → Splunk SIEM → Correlation Rule → Scheduled Alert

## Detection Use Case: Repeated Failed Logins

Windows Security Event ID 4625 represents a failed logon attempt.

The following Splunk query detects three or more failed login events from a host within a 15-minute window:

```spl
index=main "4625" earliest=-15m
| stats count as failed_logins by host
| where failed_logins >= 3

```
### Detection Query File

You can also view the standalone Splunk query here:

[View Failed Login Detection Query](queries/failed_login_detection.spl)


## Implementation

1. Configured a virtual lab using Windows 10 and Kali Linux.
2. Configured Splunk to receive forwarded Windows events.
3. Forwarded Windows security logs using Splunk Universal Forwarder.
4. Verified failed login events in Splunk.
5. Created and tested a scheduled correlation alert.
6. Created a SOC monitoring dashboard.

## Screenshots

### Windows Failed Login Event

[Windows Event ID 4625](screenshots/02_Windows_Event_4625.png)

### Failed Login Events in Splunk

[Splunk Failed Login Events](screenshots/13_Splunk_Fresh_4625.png)

### Correlation Alert Triggered

[Splunk Correlation Alert](screenshots/24_Splunk_Correlation_Alert_Triggered.png)

### SOC Monitoring Dashboard

[SOC Dashboard](screenshots/Final_SOC_Dashboard_Screenshot.png)

## Results

- Successfully demonstrated Windows security log forwarding to Splunk.
- Implemented a correlation rule for repeated failed logins.
- Successfully tested the scheduled alert.
- Created a dashboard to support security monitoring.

**Note:** The detection rule identifies activity that requires investigation; it does not independently confirm an attack. Sysmon events were configured and verified locally, but their forwarding into Splunk was not fully reliable during final testing.

## Future Improvements

- Improve forwarding of additional event sources.
- Add more detection rules.
- Improve dashboard visualizations.
- Reduce false positives and expand investigation workflows.

## Disclaimer

This project was created for educational purposes in a controlled virtual lab.
