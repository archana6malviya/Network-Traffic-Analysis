## Network Traffic Analysis using Wireshark and tcpdump

To capture, analyze, and identify normal and suspicious network traffic using Wireshark and tcpdump in a virtual lab, Linux environment..


### Tools Used
- Wireshark
- tcpdump
- Linux (Ubuntu)
- VirtualBox
- Nmap

### Traffic Analyzed
- ICMP
- DNS
- HTTP vs HTTPS
- SSH

### Wireshark Filters
- Purpose	       | Filter
- ICMP flood	   |icmp
- DNS traffic   	|dns
- HTTP traffic	| http
- HTTPS        |tcp.port == 443
- Failed logins 	|tcp.port == 22
- Specific IP	  |ip.addr == 192.168.56.101

### tcpdump Advanced Filters
#### sudo tcpdump -i eth0 tcp
Captures all TCP traffic on interface

Shows:

- HTTP / HTTPS

- SSH

- FTP

- Any TCP-based communication
  
##### 📌 When to use

✔ General network investigation
✔ Checking if a service is reachable
✔ Identifying suspicious TCP connections

#### sudo tcpdump -i eth0 port 22
Captures traffic only on port 22, Port 22 = SSH

###### 📌 When to use

✔ Detect SSH login attempts
✔ Brute-force attack investigation
✔ Monitor remote access activity

#### sudo tcpdump -i eth0 icmp
Captures ping &  ICMP traffic

ICMP includes:

- ping

- echo request

- echo reply

###### 📌 When to use

✔ Network connectivity testing
✔ Detect ICMP flooding
✔ Identify scanning or reconnaissance

#### sudo tcpdump -nn -i eth0

No name resolution, No DNS lookup, No port name conversion( Raw packet visibility)
Shows raw IP addresses and port numbers

###### 📌 Why -nn is important

✔ Faster packet capture
✔ Accurate investigation
✔ Avoids misleading name resolution

### Capture traffic using tcpdump & Wireshark

ping google.com
ssh localhost
curl http://example.com


### Key Findings
- ICMP traffic analysis
- DNS and HTTP traffic inspection
- Packet capture using tcpdump
- SSH brute-force attack detection
- Filtering and identifying suspicious traffic
- HTTP traffic was visible in plain text.
- HTTPS traffic was encrypted.
- Port scanning activity detected using SYN packets.


### Key Learnings
- Packet-level traffic analysis
- SOC-style investigation approach
- Hands-on experience with pcap files
