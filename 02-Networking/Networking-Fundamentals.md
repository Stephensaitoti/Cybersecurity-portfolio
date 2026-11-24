# Networking Fundamentals

## 1. Ports and Protocols

A port is a numbered doorway on a computer where a service listens for
connections. A protocol is the set of rules two devices follow to talk.
Common ports: 22 SSH (remote login), 53 DNS, 80 HTTP, 443 HTTPS (encrypted web),
3389 RDP (Windows remote desktop). Each open port is a possible entry point,
so only needed ports should be open.
## 2. TCP vs UDP

TCP is reliable: it sets up a connection with a three-way handshake
(SYN, SYN-ACK, ACK) and checks that data arrives. It is used for web pages and SSH.
UDP is faster but does not guarantee delivery. It is used for DNS lookups,
video calls and streaming.
## 3. DNS

DNS translates names like google.com into IP addresses, like a phone book
for the internet. It normally uses port 53. Attackers can abuse it with
DNS spoofing, which sends users to a fake site, so trusted resolvers matter.
## 4. Firewalls and NAT

A firewall allows or blocks traffic based on rules (source, destination, port).
In AWS, security groups and network ACLs do this job.
NAT lets many private devices share one public IP address and hides internal
addresses from the internet.
## 5. Network Security Risks
### Risk 1: Open Ports and Misconfigured Services
- Threat:
- Vulnerability:
- Impact:
- Recommended control:
## 6. Practical Lab: Nmap Scan
## 7. Day 3 Reflection

Today I learned that Nmap's default scan only checks the top 1,000 ports, so a
full scan with -p- found 12 open ports instead of 2. I also learned that
"unknown" in Nmap means no known name, not danger, and that ss -tlnp shows
which process owns each port. Next I want to understand how these ideas apply
to AWS security groups.
## 6. Practical Lab: Nmap Scan

*Commands:* nmap localhost then nmap -sV localhost (own Codespace only)

*Result:* 2 open TCP ports, 998 closed.

| Port | Nmap's first guess | Verified with -sV |
|---|---|---|
| 2000 | cisco-sccp | ssh (OpenSSH 8.9p1) |
| 2222 | EtherNetIP-1 | ssh (OpenSSH 9.6p1) |

*Observation:* The default scan guessed service names from port numbers, and
both guesses were wrong. Version detection (-sV) identified the real service.
Banner and version information also shows an attacker which software to target.

*Security takeaway:* Verify services instead of trusting port numbers. Keep
software patched, disable password logins for SSH, restrict who can reach SSH,
and close any service that isn't needed.
### Cross-check with ss -tlnp

sudo ss -tlnp lists every listening port and the process behind it.

| Listening address | Meaning | Risk |
|---|---|---|
| [::]:2000, [::]:2222 | SSH, all interfaces | Higher: reachable from the network |
| 127.0.0.1 / [::1] high ports | Local-only services | Lower: this machine only |
| 127.0.0.53:53 | Local DNS resolver | Low: loopback only |

*Findings:*
- Nmap's default scan covers only the top 1000 ports, so it missed several
  local-only listeners. ss shows the full picture, and nmap -p- scans all ports.
- Binding to 127.0.0.1 limits exposure. Binding to all interfaces widens it.
### Full port scan

*Command:* nmap -p- localhost (all 65,535 ports, own Codespace only)

*Result:* 12 open ports, versus 2 in the default scan.

*Lesson:* The default scan checks only the top 1,000 ports. Services on high
ports are invisible to it, so a full scan or ss -tlnp is needed for an
accurate inventory. "Unknown" in Nmap means the port number has no known name;
the service must be identified another way (-sV, or ss -tlnp to find the process).

*Security takeaway:* An accurate asset and port inventory is the first step in
reducing attack surface. Check each listener: is it needed, what is it bound to,
and who can reach it?