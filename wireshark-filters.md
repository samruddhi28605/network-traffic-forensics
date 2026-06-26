# Wireshark Display Filters Used

## ICMP Traffic

```text

icmp

```

Displays all ICMP packets.

---

## TCP Traffic

```text

tcp

```

Displays all TCP packets.

---

## TCP SYN Packets

```text

tcp.flags.syn == 1

```

Displays packets with the SYN flag enabled.

---

## Initial SYN Packets

```text

tcp.flags.syn == 1 \\\&\\\& tcp.flags.ack == 0

```

Displays TCP packets initiating new connections.

---

## Localhost Traffic

```text

ip.addr == 127.0.0.1

```

Displays packets exchanged over the loopback interface.

---

## Display Only Nmap Scan Packets

```text

tcp.flags.syn == 1 \\\&\\\& tcp.dstport

```

Useful for highlighting TCP reconnaissance attempts.
