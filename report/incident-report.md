# Cybersecurity Incident Report  
**Analysis of Wireshark Packet Captures Involving TCP and HTTP Requests**

---

## Section 1: Identification of the Attack

### Type of Attack
The network interruption was caused by a **TCP SYN Flood Denial-of-Service (DoS) attack** targeting the web server on **port 443 (HTTPS)**.

---

## Log Evidence Summary

| Activity | Source IP | Destination IP | Protocol | Description |
|--------|-----------|----------------|----------|-------------|
| Normal TCP handshake | 198.51.100.23 | 192.0.2.1 | TCP | Successful three-way handshake |
| Normal HTTP request | 198.51.100.23 | 192.0.2.1 | HTTP | `GET /sales.html` → `200 OK` |
| SYN flood traffic | **203.0.113.0** | **192.0.2.1** | TCP | Repeated SYN packets |
| Handshake failure | 203.0.113.0 | 192.0.2.1 | TCP | Missing final ACK |
| Server overload | 192.0.2.1 | Multiple | TCP | RST packets sent |
| Service failure | 198.51.100.5 | 192.0.2.1 | HTTP | `504 Gateway Time-out` |

---

### Log Observations
- A single source IP (**203.0.113.0**) repeatedly sent SYN packets to the server  
- SYN packets were sent continuously at short intervals  
- TCP handshakes were not completed  
- The server responded with SYN-ACK and later RST packets  
- Legitimate users experienced HTTP 504 Gateway Time-out errors  

---

### Attack Classification
This activity is consistent with a **TCP SYN Flood DoS attack**, where an attacker overwhelms a server by creating many half-open TCP connections, exhausting available resources.

---

## Section 2: How the Attack Caused Website Malfunction

### TCP Three-Way Handshake
1. **SYN** – Client requests a connection  
2. **SYN-ACK** – Server acknowledges and prepares connection  
3. **ACK** – Client completes the handshake  

---

### Attack Behavior Observed
- Hundreds of SYN packets were sent to port 443  
- The server responded but did not receive final ACK packets  
- Half-open connections accumulated  
- Server resources were exhausted  
- HTTP requests such as `GET /sales.html` failed  

---

### Impact on the Server
- CPU, memory, and connection tables were exhausted  
- Legitimate users experienced slow responses or timeouts  
- The website became unstable or unavailable  
- Normal HTTP requests could not be processed reliably  

---

### Important Note
`GET /sales.html` is an HTTP request asking the server to retrieve and send the **sales.html** webpage to the client.  
Due to the SYN flood, the request resulted in a timeout instead of a successful response.

---

## Organizational Impact

The attack disrupted online services, caused website downtime, risked financial loss, and negatively affected organizational reputation. Additional operational effort was required to identify and mitigate the issue.

---

## SYN Cookies (Mitigation Technique)

### What Are SYN Cookies
SYN cookies prevent the server from allocating memory for TCP connections until the client successfully completes the handshake.

### Why SYN Cookies Are Effective
- Prevent half-open connection exhaustion  
- Protect server availability  
- Block SYN flood attacks  

---

## Conclusion

This incident demonstrates how a TCP SYN Flood attack can disrupt network availability by exploiting the TCP handshake process. Implementing security mechanisms such as SYN cookies, rate limiting, firewalls, and IDS/IPS systems can significantly reduce the risk of similar attacks.

---
