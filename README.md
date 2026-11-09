# Network-Traffic-Analysis: Phishing & Malware Incident Investigation

## Project Overview
This project focuses on the tactical analysis of packet capture ('.pcap') files to isolate, identify, and document malicious insider activity and phishing campaigns within a simulated corporate network. Using Wireshark, network traffic logs were filtered and parsed to extract indicators of compromise (IoCs), trace phishing emails distribution, and identify compromised endpoint targets. 

## Scenario & Investigation Objectives
A network security alert flagged suspicious high-volume Simple Mail Transfers Protocol (SMTP) traffic. The objective was to: 
1. Identify the source materials IP address.
2. Extract the subject lines of the rogue phishing emails.
3. Reconstruct the attackers methodology using advanced network analysis filters.

## Tools Used
* **Network Analysis:** Wireshark
* **Protocols Investigated:** SMTP, TCP/IP
* **Environment:** Codepath Cybersecurity Sandbox

##Investigated methodology & Analysis Workflow 
To Isolate the malicious actor out of the raw network traffic captures, the following procedural steps were executed: 

1. **Sender isolation:** Applied the Wireshark filter 'smtp contains "FROM"' to isolate outgoing mail packets and rapidly identify the source email address and corresponding internal IP address.
2. **Payload Triage:** Utilized the filter 'smtp.data.fragment' to extract and inspect the raw data steams attached to the identified sender.
3. **Triage Aggregation review:** Analyzed the Packet List and Packet Details panes. A pattern of high-frequency packets originating from a single source IP traveling to the same internal destination address was observed.
4. **Packet Deep-Dive:** double-clicked high-risk packets within the file 'C.pcap' to examine the full frame structure. This confirmed that the sender has successfully targeted an internal endpoint, leading to malware infection and credential compromise.

5. ## Indicators of Compromise (IoCs) Discovered

6. ###1. Attacker Infrastructure
7. * **Malicious Source IP:** '10.6.1.104' (Identified in 'C.pcap')

   ###2. Phishing Campaign Artifacts
   The attacker deployed an aggressive email phishing campaign containing threatening and urgent subject headers to induce user interaction. The extracted email indicators included:
   * **Subject Line 1:** 'Read Carefully! - dayrit'
   * **Subject Line 2:** 'I can destroy everything! - 12345678'
   * **Subject Line 3:** 'Your password! - nafd111'
  
   ## Remediation & Key Findings
   The investigation successfully proved that an internal endpoint at '10.6.1.104' was actively communicating outbound malware signatures and broadcasting localized phishing scams. The packet inspection confirmed complete end-user device compromise.

   *Recommended next steps based on this analysis include isolating the host IP, revoking active session tokens for affected users, and initiating an endpoint incident response workflow.*
