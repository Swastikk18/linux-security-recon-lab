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

#Additional
### Practical: Passive Reconnaissance Using WHOIS

**Aim:** To collect publicly available domain registration information using the WHOIS utility.

**Command:**
```bash
whois xavier.ac.in
```

**Observations:**
- Registrar: ERNET India
- Domain creation date: 6 September 2018
- Registry expiry date: 6 September 2028
- Domain status: `ok`
- DNSSEC status: `unsigned`
- Registrant, administrative and technical contact details were mostly redacted.

**Result:** Public domain registration information was collected successfully. The exercise demonstrated passive reconnaissance without performing a port scan or directly testing the target system.

**Security Note:** WHOIS data represents a snapshot and may change. An unsigned DNSSEC status is an observation, not proof of a vulnerability. The exercise was limited to publicly available registration information.
# Linux Security Audits and DNS Reconnaissance — Experiments 15–22

## Experiment 15: Checking Linux Firewall Status

**Aim:** To inspect the availability and status of firewall components in Kali Linux.

**Commands used:**
```bash
command -v ufw
sudo nft list ruleset
systemctl is-active nftables
```

**Observations:**
- `ufw` was not found using `command -v ufw`.
- `sudo nft list ruleset` returned no visible rules.
- `systemctl is-active nftables` returned `inactive`.

**Conclusion:** The checks did not show an active nftables service or visible nftables rules. This does not establish the complete firewall status of the system.

## Experiment 16: Inspecting Linux Authentication Logs

**Aim:** To inspect system journal entries related to authentication and sudo activity.

**Command used:**
```bash
sudo journalctl -b | grep -iE 'authentication failure|failed password|sudo:' | tail -20
```

**Observations:** The output included sudo session-opened and session-closed entries associated with normal administrative activity.

**Conclusion:** The displayed entries showed sudo session activity. No failed-login event was established from the shown output.

## Experiment 17: Auditing File Permissions

**Aim:** To identify files in the home directory with group-write or others-write permission bits.

**Command used:**
```bash
find "$HOME" -maxdepth 2 -type f -perm /0022 -ls 2>/dev/null
```

**Observations:** Two files were listed:
- `/home/kali/.cache/zcompdump`
- `/home/kali/.config/user-dirs.locale`

Both had permissions displayed as `-rw-rw-r--`.

**Conclusion:** The listed files allowed their owner and group to write, while others had read permission only. The output alone does not establish a security vulnerability.

## Experiment 18: DNS SOA Record Analysis

**Aim:** To examine the Start of Authority (SOA) record for a domain.

**Command used:**
```bash
nslookup -type=SOA www.xavier.ac.in
```

**Observations:**
- The `www` hostname was returned as an alias of `xavier.ac.in`.
- SOA origin: `sns7.webhostbox.net`
- SOA mail field: `root.sh004.webhostbox.net`
- Serial: `2026101501`
- Refresh: `86400` seconds
- Retry: `7200` seconds
- Expire: `3600000` seconds
- Minimum: `86400` seconds

**Conclusion:** The query returned zone-management metadata, including the serial number and timing values. The minimum field is commonly relevant to negative DNS caching.

## Experiment 19: DNS TXT and SPF Record Analysis

**Aim:** To inspect the domain's TXT record containing an SPF policy.

**Command used:**
```bash
nslookup -type=TXT xavier.ac.in
```

**Observed TXT record:**
```text
v=spf1 a mx include:websitewelcome.com ~all
```

**Analysis:**
- `v=spf1`: identifies the SPF policy version.
- `a`: authorizes addresses matched by the domain's A-record mechanism.
- `mx`: authorizes addresses matched by the domain's MX mechanism.
- `include:websitewelcome.com`: references another domain's SPF policy.
- `~all`: specifies a softfail for sources not matched by the preceding mechanisms.

**Conclusion:** The query returned an SPF policy in a TXT record. This observation alone does not verify that the policy is optimally configured.

## Experiment 20: DMARC Record Verification

**Aim:** To query the conventional DMARC record location.

**Command used:**
```bash
nslookup -type=TXT _dmarc.xavier.ac.in
```

**Observation:**
```text
server can't find _dmarc.xavier.ac.in: NXDOMAIN
```

**Conclusion:** The resolver returned NXDOMAIN for the queried name, so the lookup did not retrieve a DMARC TXT record. This result should not be treated as conclusive proof of the domain's current DMARC configuration without further authoritative verification.

## Experiment 21: Passive Reconnaissance Using WHOIS

**Aim:** To collect publicly available domain registration information.

**Command used:**
```bash
whois xavier.ac.in
```

**Observations from the returned output:**
- Domain: `xavier.ac.in`
- Registrar: ERNET India
- Creation date: `2018-09-06`
- Registry expiry date: `2028-09-06`
- Domain status: `ok`
- DNSSEC: unsigned
- Registrant organization: Xavier Institute of Engineering
- Some contact fields were redacted.

The WHOIS output listed `ns1.sh004.webhostbox.net` and `ns2.sh004.webhostbox.net` as nameservers, while the earlier NS lookup returned `sns7.webhostbox.net` and `sns8.webhostbox.net`.

**Conclusion:** WHOIS provided registration metadata without requiring an active port scan. The difference between nameserver listings should be investigated separately; it may reflect different or outdated registry and DNS information. An unsigned DNSSEC status alone does not prove a vulnerability.

## Experiment 22: DNS Response Verification Using Google Public DNS

**Aim:** To compare nameserver results from a public resolver with a previously used local resolver.

**Command used:**
```bash
nslookup -type=NS xavier.ac.in 8.8.8.8
```

**Observation:**
```text
Server:         8.8.8.8
Address:        8.8.8.8#53

Non-authoritative answer:
xavier.ac.in nameserver = sns8.webhostbox.net.
xavier.ac.in nameserver = sns7.webhostbox.net.
```

**Conclusion:** Google Public DNS returned the same two nameservers as the earlier local-resolver query. This supports consistency between these two responses at the time of testing, but does not independently guarantee that all DNS data is correct.


## Overall Conclusion

These experiments covered Linux firewall-status checks, authentication-log review, file-permission auditing, DNS SOA/TXT/DMARC lookups, WHOIS-based passive reconnaissance, and comparison of DNS resolver responses. They developed practical skills in interpreting system-security evidence and publicly available DNS information.

**Safety note:** DNS and WHOIS queries were used for information gathering. Any active scanning or security testing of systems outside a controlled lab requires explicit authorization.

## Safety and Authorization Note

The Nmap scans in this report targeted local loopback addresses. DNS lookups were made for the specified domain. Future active scans of external systems should only be performed with explicit authorization. Private IP addresses, MAC addresses and other unnecessary network details should be masked in any publicly shared screenshots or reports.

# Linux Security and Network Reconnaissance — Practicals 23–40

## Practical 23: Network Route Tracing Using Traceroute

**Aim:** To observe the network path toward a domain.

**Command:**
```bash
traceroute -m 12 -w 2 xavier.ac.in
```

**Observation:**
- The domain resolved to `162.241.27.33`.
- The first hop responded from `10.0.2.2`.
- Subsequent hops did not respond within the configured timeout.

**Conclusion:** Traceroute identified the first responding hop. The remaining route could not be determined because intermediate devices may filter or ignore traceroute probes.

## Practical 24: Network Interface Configuration

**Aim:** To identify active network interfaces and assigned IP addresses.

**Command:**
```bash
ip -br addr
```

**Observation:**
- `lo` used the loopback addresses `127.0.0.1/8` and `::1/128`.
- `eth0` was UP with IPv4 address `10.0.2.15/24`.
- IPv6 unique-local and link-local addresses were also displayed.

**Conclusion:** The command displayed network interfaces and their assigned addresses. The IPv4 configuration was consistent with a VirtualBox NAT network.

## Practical 25: Inspecting the Routing Table

**Aim:** To identify the default gateway and connected network routes.

**Command:**
```bash
ip route
```

**Observation:**
- Default gateway: `10.0.2.2`
- Interface: `eth0`
- Source IPv4 address: `10.0.2.15`
- Connected subnet: `10.0.2.0/24`

**Conclusion:** The routing table showed the default route and directly connected network, helping explain how outgoing traffic is routed.

## Practical 26: Testing IP Connectivity

**Aim:** To test connectivity to an external IP address.

**Command:**
```bash
ping -c 4 8.8.8.8
```

**Observation:**
- Four packets were transmitted.
- Four packets were received.
- Packet loss: 0%.
- Average round-trip time: approximately 5.804 ms.

**Conclusion:** The system successfully reached `8.8.8.8` during the test. This confirms connectivity to that IP at that time, not the availability of every internet service.

## Practical 27: Hostname Resolution Using getent

**Aim:** To resolve a domain using the system's configured name-resolution mechanism.

**Command:**
```bash
getent hosts xavier.ac.in
```

**Observation:**
```text
162.241.27.33 xavier.ac.in
```

**Conclusion:** The system successfully resolved the domain to an IPv4 address during the test.

## Practical 28: DNS A Record Lookup Using dig

**Aim:** To retrieve the IPv4 address associated with a domain.

**Command:**
```bash
dig xavier.ac.in A
```

**Observation:**
- Status: `NOERROR`
- One answer record was returned.
- IPv4 address: `162.241.27.33`
- Query time: 24 ms.

**Conclusion:** The A record was successfully retrieved using `dig`.

## Practical 29: DNS Nameserver Lookup Using dig

**Aim:** To identify the domain's listed nameservers.

**Command:**
```bash
dig xavier.ac.in NS
```

**Observation:**
- `sns7.webhostbox.net`
- `sns8.webhostbox.net`

The response returned two NS records.

**Conclusion:** The query successfully retrieved the domain's NS records. This does not independently verify nameserver security or availability.

## Practical 30: DNS Mail Exchange Lookup Using dig

**Aim:** To identify the domain's mail exchange records.

**Command:**
```bash
dig xavier.ac.in MX
```

**Observation:**
Five MX records were returned, associated with Google mail infrastructure:
- Priority 1: `aspmx.l.google.com`
- Priority 5: `alt1.aspmx.l.google.com`
- Priority 5: `alt2.aspmx.l.google.com`
- Priority 10: `alt3.aspmx.l.google.com`
- Priority 10: `alt4.aspmx.l.google.com`

Lower MX priority values indicate higher preference.

**Conclusion:** The domain's MX records were successfully retrieved, indicating the configured mail exchange destinations.

## Practical 31: DNS TXT and SPF Record Lookup

**Aim:** To retrieve and interpret the domain's TXT/SPF record.

**Command:**
```bash
dig xavier.ac.in TXT
```

**Observation:**
```text
"v=spf1 a mx include:websitewelcome.com ~all"
```

The record includes the SPF version, `a` and `mx` mechanisms, an included SPF policy, and `~all` (softfail).

**Conclusion:** The TXT/SPF record was retrieved successfully. Further analysis would be needed to assess whether the policy is appropriate and effective.

## Practical 32: DMARC Record Lookup

**Aim:** To query the conventional DMARC TXT record location.

**Command:**
```bash
dig _dmarc.xavier.ac.in TXT
```

**Observation:**
- Status: `NXDOMAIN`
- Answer records: 0
- An SOA record appeared in the authority section.

**Conclusion:** The queried name returned `NXDOMAIN`, consistent with the earlier `nslookup` result. This lookup alone is not sufficient to make a definitive claim about the domain's overall DMARC configuration.

## Practical 33: DNS Verification Using Google Public DNS

**Aim:** To compare DNS resolution using a public resolver.

**Command:**
```bash
dig @8.8.8.8 xavier.ac.in A
```

**Observation:**
- Resolver: `8.8.8.8`
- Status: `NOERROR`
- Returned IPv4 address: `162.241.27.33`
- Query time: 16 ms.

The returned address matched the result from the default resolver in earlier tests.

**Conclusion:** Both resolvers returned consistent A-record results at the times tested.

## Practical 34: Inspecting Listening Network Sockets

**Aim:** To inspect listening TCP/UDP sockets and associated processes.

**Command:**
```bash
sudo ss -tulnp
```

**Observation:** The command displayed column headers but no socket entries.

**Conclusion:** No listening sockets were displayed by this command at the time of testing. This result does not establish that the system has no network activity or that every service is inactive.

## Practical 35: Listing Running Processes

**Aim:** To inspect running processes and their resource usage.

**Command:**
```bash
ps aux | head -10
```

**Observation:** The output displayed process owners, PIDs, CPU and memory usage, process states, and command names. System initialization and kernel threads appeared in the output.

**Conclusion:** The `ps` command provides a snapshot of running processes and selected resource-usage information.

## Practical 36: Live Process Monitoring

**Aim:** To monitor running processes and system resource usage in real time.

**Command:**
```bash
top
```

**Observation:** The interactive display showed process IDs, users, priorities, memory usage, CPU usage, process states, and accumulated CPU time.

**Conclusion:** The `top` command supports continuous monitoring of processes and system resource usage. Pressing `q` exits the display.

## Practical 37: Listing Processes for a Specific User

**Aim:** To filter processes belonging to a particular user.

**Command:**
```bash
ps -u kali
```

**Observation:** The output included desktop environment processes, VirtualBox integration processes, the terminal application, the shell, and the `ps` command.

**Conclusion:** The command can filter process listings by user, helping administrators inspect user-specific activity.

## Practical 38: Viewing the Process Hierarchy

**Aim:** To examine parent-child relationships between processes.

**Command:**
```bash
pstree -p
```

**Observation:** The command executed successfully and displayed the process hierarchy with process IDs.

**Conclusion:** `pstree -p` helps visualize how processes are organized and related to one another.

## Practical 39: Checking System Uptime and Load Average

**Aim:** To check system uptime, logged-in users, and recent load averages.

**Command:**
```bash
uptime
```

**Observation:**
- Uptime: approximately 7 hours and 6 minutes.
- Logged-in users: 1.
- Load averages: 0.13, 0.18, and 0.17 for the 1-, 5-, and 15-minute intervals, respectively.

**Conclusion:** The command provides a quick summary of system uptime and recent load. Load average is not a direct CPU-usage percentage and should be interpreted in the context of available CPU cores.

## Practical 40: Checking Disk Space Usage

**Aim:** To inspect the space used and available on mounted filesystems.

**Command:**
```bash
df -h
```

**Observation:**
- Main filesystem `/dev/sda1`: 79 GB total.
- Used space: 17 GB.
- Available space: 58 GB.
- Reported usage: 22%.

Temporary filesystems such as `/tmp` and `/dev/shm` were also displayed.

**Conclusion:** The command displayed filesystem capacity and usage in human-readable units. The main filesystem had approximately 58 GB available at the time of testing.

---

## Overall Conclusion

Practicals 23–40 covered network route tracing, IP configuration, routing, connectivity testing, hostname resolution, DNS reconnaissance, listening socket inspection, Linux process management, system monitoring, and disk-space analysis.

These exercises developed practical familiarity with Linux networking and administration commands. The observations represent results collected during the tests and should not be interpreted as a comprehensive security audit of the target domain or the Kali system.

# Practicals 41–65: Security Tools and Controlled Reconnaissance Lab

## Practical 41: Nmap Service Detection on Localhost

**Objective:** To identify open TCP ports and detect services running on the local system.

**Command:**
```bash
nmap -sV 127.0.0.1
```

**Observation:** The host was reachable, and the 1000 default TCP ports scanned were reported closed.

**Conclusion:** Nmap service detection was performed successfully. No service versions were identified because no open ports were found in the scanned range.

## Practical 42: Wireshark Version Verification

**Objective:** To verify the installation of Wireshark.

**Command:**
```bash
wireshark --version
```

**Observation:** Wireshark version 4.6.6 was installed.

**Conclusion:** Wireshark was available for network traffic analysis.

## Practical 43: Network Interface Identification

**Objective:** To identify available network interfaces.

**Command:**
```bash
ip -br link
```

**Observation:** The system displayed the loopback interface (`lo`) and Ethernet interface (`eth0`).

**Conclusion:** The command successfully listed the network interfaces available in the Kali Linux environment.

## Practical 44: Network Traffic Capture

**Objective:** To capture network packets using Wireshark.

**Procedure:** Wireshark was opened, a capture was started on `eth0`, and ordinary web browsing was performed.

**Observation:** Network packets were captured successfully.

**Conclusion:** Wireshark was used to observe traffic generated during normal browsing.

## Practical 45: DNS Packet Filtering

**Objective:** To isolate DNS traffic from a packet capture.

**Display filter:**
```text
dns
```

**Observation:** DNS packets appeared in the capture and a DNS packet was inspected.

**Conclusion:** Wireshark display filters can help identify DNS-related network activity.

## Practical 46: TCP Packet Filtering

**Objective:** To view TCP packets in a capture.

**Display filter:**
```text
tcp
```

**Observation:** TCP packets were displayed successfully.

**Conclusion:** The filter helped isolate TCP traffic for analysis.

## Practical 47: TCP Flag Observation

**Objective:** To inspect TCP control flags.

**Procedure:** A TCP packet was selected in Wireshark and its flags were examined.

**Observation:** The ACK (Acknowledgment) flag was observed.

**Conclusion:** TCP flags provide information about connection and data-delivery behavior.

## Practical 48: HTTP Traffic Inspection

**Objective:** To identify HTTP packets in captured traffic.

**Display filter:**
```text
http
```

**Observation:** Two packets matched the filter, and packet details were inspected.

**Conclusion:** Wireshark can display HTTP traffic when such packets are present in the capture.

## Practical 49: TLS Traffic Inspection

**Objective:** To identify TLS-related packets.

**Display filter:**
```text
tls
```

**Observation:** TLS packets were displayed in the capture.

**Conclusion:** Wireshark can help identify encrypted transport sessions and inspect their visible protocol metadata.

## Practical 50: Burp Suite Installation Verification

**Objective:** To verify the installation of Burp Suite Community Edition.

**Command:**
```bash
burpsuite --version
```

**Observation:** Burp Suite Community Edition version 2026.3.2 was reported. A Java environment warning was displayed before the version output.

**Conclusion:** Burp Suite was available and launched successfully.

## Practical 51: Burp Suite Project Setup

**Objective:** To prepare Burp Suite for HTTP traffic analysis.

**Procedure:** A temporary project was opened using the default configuration, and the built-in browser was launched.

**Observation:** Burp Suite's project interface and browser were accessible.

**Conclusion:** The environment was prepared for observing browser requests and responses.

## Practical 52: Burp Suite Browser Verification

**Objective:** To verify that the built-in browser could generate HTTP traffic through Burp Suite.

**Procedure:** The browser was used to visit a website during the earlier reconnaissance exercise.

**Observation:** HTTP request and response information was available in Burp Suite.

**Conclusion:** Burp Suite was functioning as a web traffic inspection tool.

## Practical 53: Basic HTTP Request and Response Observation

**Objective:** To understand the structure of an HTTP request and response.

**Observed request:**
```http
GET / HTTP/1.1
Host: xavier.ac.in
```

**Observed response status:**
```http
HTTP/2 200 OK
```

**Conclusion:** The request asked for the website's root path, and the observed response indicated success. This was ordinary browsing only; no active security testing was performed against the external website.

## Practical 54: OWASP ZAP Installation Verification

**Objective:** To verify the OWASP ZAP installation.

**Observation:** OWASP ZAP version 2.17.0 was reported, and its graphical interface opened. A Java deprecation warning was observed.

**Conclusion:** ZAP was installed and its interface was accessible. An automated scan was not performed as part of this verification.

## Practical 55: OWASP ZAP Interface Familiarization

**Objective:** To become familiar with the ZAP interface.

**Procedure:** The Sites panel, Contexts, Default Context, and History tab were explored.

**Observation:** The main interface panels were accessible.

**Conclusion:** Basic familiarity with the ZAP interface was established. This practical did not establish that a security scan had been completed.

## Practical 56: Local Security Lab Preparation

**Objective:** To prepare an isolated web application for controlled security testing.

**Procedure:** Podman was used as the container runtime through a Docker-compatible command interface.

**Observation:** Podman version 5.8.6 was available, and the container runtime information was checked.

**Conclusion:** A container runtime was available for preparing a local training environment.

## Practical 57: OWASP Juice Shop Image Retrieval

**Objective:** To retrieve the intentionally vulnerable OWASP Juice Shop training application.

**Command:**
```bash
podman pull docker.io/bkimminich/juice-shop
```

**Observation:** The image was pulled successfully.

**Conclusion:** The Juice Shop image was available for local deployment.

## Practical 58: Local Juice Shop Deployment

**Objective:** To launch the training application locally.

**Command:**
```bash
podman run -d --name juice-shop -p 127.0.0.1:3000:3000 docker.io/bkimminich/juice-shop
```

**Observation:** The container started successfully and was listed as running. Port 3000 was bound to `127.0.0.1`.

**Conclusion:** The application was exposed on the local loopback interface rather than being intentionally published on all network interfaces.

## Practical 59: Local Application Accessibility

**Objective:** To verify that the local training application was accessible.

**Procedure:** The URL below was opened in the Kali browser:
```text
http://127.0.0.1:3000
```

**Observation:** The OWASP Juice Shop homepage loaded successfully.

**Conclusion:** The local application was available for further controlled testing.

## Practical 60: Nmap Port and Service Check

**Objective:** To check the application port and observe the service response.

**Command:**
```bash
nmap -sV -p 3000 127.0.0.1
```

**Observation:** Port `3000/tcp` was open. Nmap did not confidently identify the service and displayed an uncertain service label (`ppp?`). Its response data contained an HTTP `200 OK` response and HTML associated with OWASP Juice Shop.

**Conclusion:** The local application port was reachable. The uncertain Nmap service label was not treated as a confirmed service identification.

## Practical 61: HTTP Response Header Inspection

**Objective:** To inspect the HTTP headers returned by the local application.

**Command:**
```bash
curl -I http://127.0.0.1:3000
```

**Observation:** The application returned `HTTP/1.1 200 OK`. Headers included `Content-Type: text/html; charset=UTF-8`, `X-Content-Type-Options: nosniff`, `X-Frame-Options: SAMEORIGIN`, and `Access-Control-Allow-Origin: *`.

**Conclusion:** The application responded successfully and exposed HTTP response headers for review. The wildcard CORS header warrants context-specific review but does not, by itself, establish a vulnerability.

## Practical 62: HTTP Response Body Inspection

**Objective:** To inspect the beginning of the application's HTML response.

**Command:**
```bash
curl -s http://127.0.0.1:3000 | head -n 15
```

**Observation:** The output contained HTML markup, the page title `OWASP Juice Shop`, and the application's copyright and licence information.

**Conclusion:** The local web server returned the expected HTML page.

## Practical 63: Burp Suite HTTP Traffic Analysis

**Objective:** To observe HTTP traffic for the local training application.

**Procedure:** The application was opened in Burp Suite's built-in browser, and the request was located under Proxy → HTTP history.

**Observation:** The main page request returned `200 OK`.

**Conclusion:** Burp Suite successfully displayed the request and its successful response for the local application.

## Practical 64: HTTP Response Header Inspection in Burp Suite

**Objective:** To view response details through Burp Suite.

**Procedure:** The main page request was selected in HTTP history, and the Response panel was opened.

**Observation:** The response status and headers were visible.

**Conclusion:** Burp Suite provided a way to inspect HTTP response metadata without relying only on terminal commands.

## Overall Summary

These practicals covered Nmap, Wireshark, Burp Suite, OWASP ZAP installation and interface exploration, Linux networking, DNS/TCP/TLS traffic observation, and a controlled local web application environment.

The OWASP Juice Shop lab was deployed on `127.0.0.1:3000` and verified using the browser, Nmap, curl, and Burp Suite. No conclusion about exploitability was drawn solely from the observed response headers. The ZAP automated scan and interpretation of its alerts remain pending.

**Scope note:** Active testing in this lab is limited to the locally hosted OWASP Juice Shop. The earlier request to `xavier.ac.in` was ordinary browsing and observation, not an active vulnerability scan.
