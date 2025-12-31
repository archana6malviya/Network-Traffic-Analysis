## Network Traffic Analysis using Wireshark and tcpdump

To capture, analyze, and identify normal and suspicious network traffic using Wireshark and tcpdump in a virtual lab.


### Tools Used
- Wireshark
- tcpdump
- Linux (Ubuntu)
- VirtualBox

### Wireshark Filters
- Purpose	       | Filter
- Failed logins 	|tcp.port == 22
- ICMP flood	   |icmp
- DNS traffic   	|dns
- HTTP traffic	| http
- Specific IP	  |ip.addr == 192.168.56.101

### Scenarios Covered
- ICMP traffic analysis
- DNS and HTTP traffic inspection
- Packet capture using tcpdump
- SSH brute-force attack detection
- Filtering and identifying suspicious traffic

### Key Learnings
- Packet-level traffic analysis
- SOC-style investigation approach
- Hands-on experience with pcap files
