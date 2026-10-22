# Detection: Repeated Failed Login Attempts

## Objective

Identify hosts generating multiple Windows failed logon events for further security investigation.

## Data Source

* **Platform:** Windows
* **Log Source:** Windows Security Event Log
* **Event ID:** 4625
* **SIEM:** Splunk Enterprise

## Detection Logic

The Splunk query searches the previous 15 minutes for matching events, counts them by host, and returns hosts with at least three matches.

## Potential Security Significance

Repeated failed logins may indicate:

* Incorrectly entered passwords.
* Password guessing.
* Brute-force login attempts.
* Misconfigured applications repeatedly attempting authentication.

The detection alone does not establish malicious activity.

## Analyst Investigation Steps

1. Review the matching Windows security events.
2. Identify the affected account and source IP address, where available.
3. Check the timestamps and frequency of failed attempts.
4. Look for successful logins around the same period.
5. Compare activity with expected user and system behaviour.
6. Escalate suspicious activity according to the organization's incident response process.

## Limitations

The current query groups matching events by host. It does not separately correlate events by account or source IP address.

The search should be validated against the actual Windows events available in Splunk before being used in a production environment.

## Project Context

This detection was developed as part of an educational SOC monitoring and log correlation lab.
