# TCP SYN Flood Incident Analysis

## Overview
This project presents an analysis of Wireshark packet captures involving TCP and HTTP requests. The investigation identifies a TCP SYN Flood Denial-of-Service (DoS) attack that caused website timeouts and service disruption.

## Incident Summary
- **Attack Type:** TCP SYN Flood (DoS)
- **Target Port:** 443 (HTTPS)
- **Affected Resource:** sales.html
- **Impact:** HTTP 504 Gateway Time-out errors

## Repository Structure
- `report/` – Detailed cybersecurity incident report
- `logs/` – Packet capture summary
- `references/` – Mitigation techniques and security concepts

## Key Concepts Covered
- TCP three-way handshake
- SYN flood attack behavior
- HTTP request failures
- SYN cookies and mitigation strategies

## Tools Used
- Wireshark
- TCP/IP analysis
- HTTP protocol inspection
