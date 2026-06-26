# Investigation Findings

## Case Information

**Case ID:** NTF-001

**Investigator:** Samruddhi Bhasme

**Investigation Type:** Network Traffic Forensics

---

## Executive Summary

A packet-level investigation was performed to compare legitimate ICMP communication with TCP SYN reconnaissance generated using Nmap. The captured traffic was analyzed using Wireshark display filters to identify behavioral differences between normal network activity and reconnaissance attempts.

---

## Investigation 1 — ICMP Echo

### Command

```bash

ping -c 5 localhost

```

### Wireshark Filter

```text

icmp

```

### Findings

* Echo Requests were observed.
* Echo Replies were successfully received.
* Communication occurred entirely over localhost.
* No abnormal behavior was detected.

### Assessment

**Severity:** Informational

---

## Investigation 2 — TCP SYN Scan

### Command

```bash

sudo nmap -sS localhost

```

### Wireshark Filter

```text

tcp.flags.syn == 1 \\\&\\\& tcp.flags.ack == 0

```

### Findings

* Multiple SYN packets targeted different ports.
* Traffic pattern matched reconnaissance behavior.
* TCP connection establishment was intentionally incomplete.

### Assessment

**Severity:** Medium

---

# Overall Assessment

The investigation demonstrates how packet analysis can distinguish legitimate network communication from reconnaissance traffic.

Although the scan was performed in a controlled environment against localhost, the packet characteristics are representative of reconnaissance attempts observed in operational environments.

---

## Lessons Learned

* Packet captures provide valuable forensic evidence.
* Display filters simplify network investigations.
* Understanding TCP flags is essential for threat hunting.
* Reconnaissance activity can often be detected before exploitation begins.
