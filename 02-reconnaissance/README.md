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
# Experiment 7: Introduction to Reconnaissance

## Aim
To understand reconnaissance in cybersecurity and perform a basic DNS lookup to observe how a domain name is resolved to an IP address.

## Theory
Reconnaissance is the process of collecting information about a target before a security assessment. It helps security professionals understand a target's digital footprint and identify systems or services that may require further authorized assessment.

### Types of Reconnaissance

**1. Passive Reconnaissance:** Collecting information from publicly available sources without directly probing the target's systems. Examples include reviewing public DNS records and domain registration information.

**2. Active Reconnaissance:** Interacting directly with a target system to identify hosts, ports, and services. Examples include authorized network discovery and Nmap scanning.

## Practical
The `nslookup` command was used to query the DNS information of a domain.

### Command Used
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

## Observations
- The configured DNS resolver was `192.168.1.1`.
- DNS uses port `53` for standard queries.
- The queried domain was `xavier.ac.in`.
- The resolver returned the IPv4 address `162.241.27.33`.
- The result demonstrates how DNS translates a domain name into an IP address.
- A DNS response alone does not prove that the target has any security vulnerability.

## Result
The `nslookup` command was executed successfully, and the returned DNS information was observed. The practical demonstrated a basic information-gathering technique used during reconnaissance.

## Safety and Authorization
DNS queries were performed for educational purposes. Any further scanning or security testing of systems will be conducted only with appropriate authorization.
