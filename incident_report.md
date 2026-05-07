# SOC Incident Report

**Traffic Analysis Exercise:** Download from Fake Software Site  
**Date of PCAP Exercise:** 2025-01-22  
**Analyst:** Hyperveil

## Executive Summary

A Windows workstation on the **BLUEMOONTUESDAY / bluemoontuesday.com** LAN was infected after visiting a fake Google Authenticator download page. Network evidence identifies the infected host, associated user account, likely fake Authenticator domain, and C2 infrastructure contacted after infection.

## Incident Findings

| Question | Answer |
|---|---|
| IP address of infected Windows client | `10.1.17.215` |
| MAC address of infected Windows client | `00:d0:b7:26:4a:74` |
| Hostname of infected Windows client | `DESKTOP-L8C5GSJ` |
| User account name | `shutchenson` |
| Likely fake Google Authenticator domain | `google-authenticator.burleson-appliance.net` |
| C2 IP address | `5.252.153.241` |
| C2 IP address | `45.125.66.32` |
| C2 IP address | `45.125.66.252` |

## Additional Suspicious Infrastructure

- `authenticatoor.org`
- `82.221.136.26`

**Analyst note:** `82.221.136.26` is associated with the fake-page / initial lure or delivery path, but the primary C2 answer list is limited to `5.252.153.241`, `45.125.66.32`, and `45.125.66.252`.

## Environment Details

| Detail | Value |
|---|---|
| LAN segment | `10.1.17.0/24` |
| AD domain | `BLUEMOONTUESDAY / bluemoontuesday.com` |
| Domain controller | `10.1.17.2 / WIN-GSH54QLW48D` |
| Gateway | `10.1.17.1` |
| Broadcast address | `10.1.17.255` |

## Recommended Follow-Up Actions

1. Isolate `DESKTOP-L8C5GSJ` from the network.
2. Reset credentials for `shutchenson` and review recent authentication activity.
3. Block the listed C2 IPs and suspicious domains at DNS, proxy, firewall, and EDR controls.
4. Hunt for PowerShell download cradle behavior, suspicious VBScript execution, and persistence involving `TeamViewer.exe` under nonstandard paths.
5. Review other hosts for outbound communication to the same infrastructure.

## Sources Consulted

- Malware-Traffic-Analysis.net exercise page: https://www.malware-traffic-analysis.net/2025/01/22/index.html
- Malware-Traffic-Analysis.net answers page: https://www.malware-traffic-analysis.net/2025/01/22/page2.html
- Public PCAP walkthroughs corroborating host artifacts and C2 indicators.
