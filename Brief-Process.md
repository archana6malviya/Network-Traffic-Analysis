# 🔹 Network Traffic Analysis (Wireshark + tcpdump)

## 🧩 Lab Setup

### ✅ Requirements

* **Host OS**: Windows
* **VM**: Ubuntu Linux (VirtualBox / VMware)
  
* **Tools**:
  * Wireshark
  * tcpdump (already installed in Ubuntu)

### ✅ Network Mode 

Set your VM network to:

* **NAT** 
* **Bridged**

---

## 🔹 PART 1: Install & Verify Tools (Ubuntu VM)

### 1️⃣ Update system

```bash
sudo apt update && sudo apt upgrade -y
```

### 2️⃣ Install Wireshark

```bash
sudo apt install wireshark -y
```

When asked:
👉 **“Allow non-superusers to capture packets?” → YES**

### 3️⃣ Add user to wireshark group

```bash
sudo usermod -aG wireshark $USER
```

Then **logout & login again**

### 4️⃣ Verify tcpdump

```bash
tcpdump --version
```

---

## 🔹 PART 2: Capture Traffic using tcpdump

### 1️⃣ Identify network interface

```bash
ip a
```

You’ll see something like:

* `eth0` or `ens33`

---

### 2️⃣ Capture ICMP (Ping traffic)

Open **Terminal 1**:

```bash
sudo tcpdump -i eth0 icmp
```

Open **Terminal 2**:

```bash
ping google.com
```

👉 ICMP Echo Request & Reply

---

### 3️⃣ Capture DNS traffic

```bash
sudo tcpdump -i eth0 port 53
```

In another terminal:

```bash
nslookup google.com
```

DNS query & response

---

### 4️⃣ Capture SSH traffic

```bash
sudo tcpdump -i eth0 port 22
```

If SSH not installed:

```bash
sudo apt install openssh-server -y
sudo systemctl start ssh
```

Then:

```bash
ssh localhost
```

TCP handshake

---

### 5️⃣ Capture HTTP traffic

```bash
sudo tcpdump -i eth0 port 80 -nn
```

Then:

```bash
curl http://example.com
```

 HTTP traffic

---

### 6️⃣ Capture HTTPS traffic

```bash
sudo tcpdump -i eth0 port 443 -nn
```

Then:

```bash
curl https://google.com
```

 encrypted HTTPS packets

---

## 🔹 PART 3: Capture Traffic using Wireshark

### 1️⃣ Start Wireshark

```bash
wireshark
```

Select:
👉 **eth0 / ens33**

Click **Start Capture**

---

### 2️⃣ Apply Filters (Very Important)

| Traffic | Filter            |
| ------- | ----------------- |
| ICMP    | `icmp`            |
| DNS     | `dns`             |
| HTTP    | `http`            |
| HTTPS   | `tcp.port == 443` |
| SSH     | `tcp.port == 22`  |


---

## 🔹 PART 4: Detect Suspicious Activity

### 🔴 Port Scan Detection

Install nmap:

```bash
sudo apt install nmap -y
```

Run scan:

```bash
nmap -p 1-1000 localhost
```

In Wireshark filter:

```
tcp.flags.syn == 1 and tcp.flags.ack == 0
```

multiple SYN packets
👉 This is **port scanning behavior**

---

### 🔴 Unusual Traffic Pattern

* Repeated SYN packets
* Same source IP hitting multiple ports
* High packet rate in short time

Write observation like:

> “Multiple SYN packets detected from 127.0.0.1 targeting different ports, indicating possible port scanning.”

---

## 🔹 PART 5: Documentation (THIS MAKES IT RESUME-READY)

### 🔹 Create Incident Findings

Write:

* Protocol analyzed
* Normal behavior
* Suspicious behavior
* SOC conclusion

---

> **Network Traffic Analysis using Wireshark & tcpdump**
> • Captured and analyzed ICMP, DNS, HTTP, HTTPS, and SSH traffic to identify normal and suspicious network behavior
> • Detected port scanning activity using SYN packet analysis
> • Documented findings with screenshots and SOC-style incident observations

---


