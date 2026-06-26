# Network Traffic Forensics: Packet-Level Analysis of ICMP Communication and TCP SYN Reconnaissance

> A hands-on cybersecurity mini project focused on analyzing network reconnaissance techniques using Wireshark and Nmap from a defensive security perspective.

---

## Executive Summary

Understanding network traffic is a fundamental skill for security analysts. Before an attack is launched, adversaries often perform reconnaissance to discover active hosts and open ports. This project demonstrates how different types of network traffic appear at the packet level and how they can be identified using Wireshark.

The investigation compares normal ICMP communication with TCP SYN reconnaissance traffic generated using Nmap. Rather than focusing on offensive scanning, the project emphasizes packet inspection, traffic interpretation, and defender-oriented analysis.

---

## Objectives

* Capture network traffic using Wireshark
* Generate legitimate ICMP traffic using `ping`
* Generate TCP SYN reconnaissance traffic using Nmap
* Compare packet characteristics of both activities
* Document observations from a SOC analyst's perspective
* Demonstrate the use of Wireshark display filters for investigation

---

## Tools Used

| Tool           | Purpose                   |
| -------------- | ------------------------- |
| Kali Linux     | Testing Environment       |
| Wireshark      | Packet Capture & Analysis |
| Nmap           | Network Reconnaissance    |
| Linux Terminal | Traffic Generation        |

---

## Lab Environment

| Component        | Details                 |
| ---------------- | ----------------------- |
| Operating System | Kali Linux              |
| Network Scope    | Localhost (127.0.0.1)   |
| Packet Capture   | Loopback Interface (lo) |
| Target           | Local System            |

---

## Investigation Workflow

```

Generate Network Traffic

\\\&#x20;       │

\\\&#x20;       ▼

Capture Packets using Wireshark

\\\&#x20;       │

\\\&#x20;       ▼

Apply Display Filters

\\\&#x20;       │

\\\&#x20;       ▼

Inspect Packet Headers

\\\&#x20;       │

\\\&#x20;       ▼

Compare Traffic Patterns

\\\&#x20;       │

\\\&#x20;       ▼

Document Findings

```

---

# Investigation 1 — ICMP Echo Analysis

Command Executed

```bash

ping -c 5 localhost

```

Display Filter

```text

icmp

```

### Evidence

![ICMP Echo](screenshots/01_icmp_echo.jpeg)

### Observation

ICMP Echo Request and Echo Reply packets were successfully captured over the loopback interface. The communication demonstrated expected request-response behavior used for connectivity verification.

---

# Investigation 2 — TCP SYN Reconnaissance

Command Executed

```bash

sudo nmap -sS localhost

```

Display Filter

```text

tcp.flags.syn == 1 \\\\\\\&\\\\\\\& tcp.flags.ack == 0

```

### Evidence

![SYN Scan](screenshots/02_syn_scan.jpeg)

The packet capture shows multiple SYN packets targeting different ports without completing a full TCP session. This behavior is consistent with reconnaissance activity performed before exploitation.

---

# Packet Comparison

![Comparison](screenshots/04_comparison_table.jpeg)

---

# Key Findings

* ICMP traffic follows a predictable request-response pattern.
* SYN scans generate multiple TCP SYN packets across different destination ports.
* Wireshark display filters significantly simplify packet investigation.
* Packet-level analysis enables defenders to distinguish legitimate traffic from reconnaissance attempts.

---

# Detection Recommendations

* Monitor repeated TCP SYN packets targeting multiple ports.
* Investigate abnormal scanning frequency.
* Configure IDS/IPS signatures for SYN scan detection.
* Enable firewall logging for reconnaissance attempts.

---

# Skills Demonstrated

* Packet Analysis
* Network Traffic Investigation
* Wireshark Display Filters
* TCP/IP Fundamentals
* Nmap Reconnaissance
* Threat Hunting
* Technical Documentation

---

# Privacy Considerations

This project was conducted exclusively on the local loopback interface (`127.0.0.1`). No external hosts were scanned, and no sensitive network information has been included in this repository.

---

# Future Improvements

* Analyze FIN, NULL and XMAS scans
* Automate packet parsing using Python
* Generate PDF reports automatically
* Integrate Snort/Suricata detection rules
