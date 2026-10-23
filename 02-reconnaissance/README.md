# Reconnaissance in Cybersecurity

## Objective
To understand passive and active reconnaissance techniques used to collect information about a target during an authorized security assessment.

## Topics
- Introduction to reconnaissance
- Passive reconnaissance
- Active reconnaissance
- Domain and DNS information gathering
- Network enumeration
- Ethical and legal considerations

## Practical Exercises
Practical commands, observations, screenshots, and findings will be documented here after testing.

## Safety and Authorization
All reconnaissance activities will be limited to systems I own or have explicit permission to assess.
# MINI TASK 2: LINUX, SECURITY TOOLS & RECONNAISSANCE

**Student Name:** Romit Singh  
**Environment:** Kali Linux (VirtualBox)  
**Tools Used:** Linux Terminal, `nslookup`, Nmap, Linux `ip` utility

## Experiment 7: Introduction to Reconnaissance

### Aim
To understand the concept of reconnaissance and perform a basic DNS lookup to obtain the IP address associated with a domain.

### Theory
Reconnaissance is the process of collecting information about a target before security testing.

- **Passive reconnaissance:** Collecting information from publicly available sources without directly probing the target's services.
- **Active reconnaissance:** Interacting directly with a target system to collect information.

DNS lookups can help identify domain-related information.

### Command Executed
```bash
nslookup xavier.ac.in
```

### Observed Output
```text
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   xavier.ac.in
Address: 162.241.27.33
```

### Explanation
- `nslookup` is a utility used to query DNS records.
- `192.168.1.1` is the DNS resolver used for this query.
- Port `53` is the standard DNS port shown in the output.
- `162.241.27.33` is the IPv4 address returned for the domain at the time of the lookup.
- A non-authoritative answer means the response was provided by a resolver rather than directly by the domain's authoritative name server.

### Result
The DNS lookup completed successfully and returned an IP address associated with the domain.

---

## Experiment 8: Passive Reconnaissance Using NS Records

### Aim
To identify the name servers associated with a domain by querying its DNS NS records.

### Command Executed
```bash
nslookup -type=NS xavier.ac.in
```

### Observed Output
```text
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
xavier.ac.in    nameserver = sns7.webhostbox.net.
xavier.ac.in    nameserver = sns8.webhostbox.net.

Authoritative answers can be found from:
```

### Explanation
- `-type=NS` requests the domain's Name Server records.
- NS records identify the DNS name servers responsible for a domain's DNS information.
- The query returned `sns7.webhostbox.net` and `sns8.webhostbox.net`.

### Result
The NS record lookup completed successfully and identified two name servers associated with the domain.

---

## Experiment 9: Passive Reconnaissance Using MX Records

### Aim
To identify the mail servers associated with a domain using DNS MX records.

### Command Executed
```bash
nslookup -type=MX xavier.ac.in
```

### Observed Output
```text
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
xavier.ac.in    mail exchanger = 10 alt4.aspmx.l.google.com.
xavier.ac.in    mail exchanger = 5 alt1.aspmx.l.google.com.
xavier.ac.in    mail exchanger = 10 alt3.aspmx.l.google.com.
xavier.ac.in    mail exchanger = 5 alt2.aspmx.l.google.com.
xavier.ac.in    mail exchanger = 1 aspmx.l.google.com.

Authoritative answers can be found from:
```

### Explanation
- `-type=MX` requests Mail Exchange records.
- MX records identify mail servers designated to receive email for a domain.
- The numbers are priority values; a lower number indicates a higher preference.
- The returned records suggest that the domain uses Google's mail infrastructure.

### Result
The MX record lookup completed successfully and returned five mail exchanger entries.

---

## Experiment 10: DNS A Record Enumeration

### Aim
To retrieve the IPv4 address associated with a domain using its DNS A record.

### Command Executed
```bash
nslookup -type=A xavier.ac.in
```

### Observed Output
```text
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   xavier.ac.in
Address: 162.241.27.33
```

### Explanation
- `-type=A` requests an IPv4 address record.
- The domain resolved to `162.241.27.33` during this query.
- DNS results may change over time due to changes in hosting or DNS configuration.

### Result
The A record query completed successfully and returned the domain's IPv4 address.

---

## Experiment 11: DNS CNAME Record Enumeration

### Aim
To identify whether a hostname is configured as an alias of another hostname using a DNS CNAME record.

### Command Executed
```bash
nslookup -type=CNAME www.xavier.ac.in
```

### Observed Output
```text
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
www.xavier.ac.in        canonical name = xavier.ac.in.

Authoritative answers can be found from:
```

### Explanation
- `-type=CNAME` requests a Canonical Name record.
- A CNAME record maps an alias hostname to another canonical hostname.
- The output indicates that `www.xavier.ac.in` is configured as an alias of `xavier.ac.in`.

### Result
The CNAME lookup completed successfully and identified the canonical hostname for `www.xavier.ac.in`.

---

## Experiment 12: Network Enumeration Using Nmap on 127.0.0.2

### Aim
To perform a basic TCP port scan against a local loopback address using Nmap.

### Command Executed
```bash
nmap 127.0.0.2
```

### Observed Output
```text
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-23 13:40 -0400
Nmap scan report for 127.0.0.2
Host is up (0.0000010s latency).
All 1000 scanned ports on 127.0.0.2 are in ignored states.
Not shown: 1000 closed tcp ports (reset)

Nmap done: 1 IP address (1 host up) scanned in 2.57 seconds
```

### Explanation
- Nmap is a network exploration and security auditing tool.
- `127.0.0.2` is within the IPv4 loopback range, which refers to the local system.
- `Host is up` indicates that Nmap determined the target was reachable.
- The scan checked Nmap's default set of 1,000 common TCP ports.
- All 1,000 checked ports were reported as closed.

### Result
The Nmap scan completed successfully. The local loopback target was reachable, and all 1,000 default TCP ports checked were reported as closed.

---

## Experiment 13: Network Enumeration Using Nmap on Localhost

### Aim
To scan the standard localhost address and examine the status of common TCP ports.

### Command Executed
```bash
nmap 127.0.0.1
```

### Observed Output
```text
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-23 13:41 -0400
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0000010s latency).
All 1000 scanned ports on localhost (127.0.0.1) are in ignored states.
Not shown: 1000 closed tcp ports (reset)

Nmap done: 1 IP address (1 host up) scanned in 0.06 seconds
```

### Explanation
- `127.0.0.1` is the standard IPv4 loopback address, commonly known as `localhost`.
- The scan targeted the local system rather than a remote computer.
- Nmap reported the target as reachable.
- All 1,000 default TCP ports checked were closed at the time of the scan.
- The scan completed in approximately 0.06 seconds.

### Result
The localhost scan completed successfully and reported all 1,000 checked TCP ports as closed.

---

## Experiment 14: Identification of Linux Network Interfaces

### Aim
To identify network interfaces in Kali Linux and understand their status.

### Command Executed
```bash
ip -br link
```

### Observations
1. The loopback interface `lo` was present.
2. Another network interface was present and marked `UP`.
3. The brief output format displayed interface information in a compact form.

### Explanation
- `ip` is a Linux utility for inspecting and managing network configuration.
- `-br` displays information in brief format.
- `link` displays network-interface information.
- `lo` is the loopback interface used for communication within the local system.
- `UP` indicates that the interface is administratively enabled; it does not by itself confirm internet connectivity.
- In a VirtualBox environment, an additional interface may be a virtual network adapter.

### Result
The network-interface inspection was completed successfully. The loopback interface and another enabled network interface were identified.

---

## Overall Conclusion

In Mini Task 2, Experiments 7–14, the following activities were performed:

1. Learned the fundamentals of reconnaissance.
2. Retrieved DNS NS, MX, A and CNAME records using `nslookup`.
3. Identified name servers, mail exchangers, an IPv4 address and a hostname alias.
4. Performed two basic Nmap scans against local loopback addresses.
5. Inspected Linux network interfaces using the `ip` command.
6. Learned the difference between DNS reconnaissance, local port scanning and network-interface inspection.

These experiments introduced essential Linux networking and reconnaissance concepts used in cybersecurity.

## Safety and Authorization Note

The Nmap scans in this report targeted local loopback addresses. DNS lookups were made for the specified domain. Future active scans of external systems should only be performed with explicit authorization. Private IP addresses, MAC addresses and other unnecessary network details should be masked in any publicly shared screenshots or reports.

