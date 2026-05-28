# 📡 ARP Network Scanner

A fast and lightweight **network reconnaissance tool** built with Python and Scapy that discovers all **active devices** on a network using ARP (Address Resolution Protocol) — showing their IP and MAC addresses in real time.

> ⚠️ **Disclaimer:** This tool is for **educational and ethical use only**. Only scan networks you own or have explicit permission to test. Unauthorized network scanning is illegal.

---

## 📸 Preview

```
$ sudo python arp_network_scanner.py

IP              MAC Address
-------------------------------------------------
10.252.183.1    aa:bb:cc:dd:ee:ff
10.252.183.5    11:22:33:44:55:66
10.252.183.12   77:88:99:aa:bb:cc
```

---

## ✨ Features

- 🔍 **Discovers all live hosts** on a subnet using ARP requests
- 📋 **Displays IP + MAC address** of every responding device
- ⚡ **Fast scanning** — uses Scapy's `srp()` with timeout control
- 🔕 **Silent mode** — `verbose=False` keeps output clean
- 🧱 Works on any **/24 or custom CIDR** network range

---

## 🛠️ Requirements

| Requirement | Detail |
|-------------|--------|
| OS | Linux (Kali recommended) |
| Python | 3.x |
| Library | `scapy` |
| Privileges | Must run as **root** (`sudo`) |

### Install Scapy

```bash
pip install scapy
```

---

## 📁 Project Structure

```
arp-network-scanner/
│
└── arp_network_scanner.py    # Main scanner script
```

---

## ▶️ How to Run

```bash
sudo python arp_network_scanner.py
```

> ⚠️ `sudo` is required — ARP scanning needs raw socket access

---

## 🔧 Change Target Network

Inside the script, edit **line 22** to your target network range:

```python
# Default
results = scan("10.252.183.209/24")

# Examples:
results = scan("192.168.1.1/24")    # Home network
results = scan("172.16.0.1/16")     # Larger subnet
results = scan("10.0.0.1/8")        # Big network
```

---

## 🧠 How It Works

```
┌──────────────────────────────────────────────────────┐
│                    How ARP Scan Works                │
├──────────────────────────────────────────────────────┤
│  1. Create ARP request → "Who has this IP?"          │
│  2. Wrap in Ethernet frame → broadcast ff:ff:ff:ff   │
│  3. Send to ALL devices in the subnet                │
│  4. Collect replies from active/live devices         │
│  5. Extract IP + MAC from each reply                 │
│  6. Display results in a clean table                 │
└──────────────────────────────────────────────────────┘
```

---

## ✅ Expected Output

**Devices Found:**
```
IP              	MAC Address
-------------------------------------------------
192.168.1.1     	c8:3a:35:12:ab:cd    ← Router
192.168.1.5     	00:1a:2b:3c:4d:5e    ← Your PC
192.168.1.10    	34:56:78:9a:bc:de    ← Phone
```

**No Devices Found:**
```
IP              	MAC Address
-------------------------------------------------
(empty — no hosts responded)
```

---

## ⚠️ Important Notes

- 🔐 Always run with `sudo` — raw sockets need root access
- 🐧 **Linux only** — Scapy's ARP works best on Linux
- 📶 Must be **connected to the network** you want to scan
- 🔢 `/24` = scans 254 hosts (e.g., `192.168.1.1` to `192.168.1.254`)
- ⏱️ `timeout=1` — increase to `2` or `3` for slower networks

---

## 🚀 Future Improvements

- [ ] Accept IP range as command-line argument (`-r`)
- [ ] Add hostname resolution
- [ ] Export results to CSV file
- [ ] Add OS fingerprinting
- [ ] Colorized terminal output

---

## 🤝 Contributing

Pull requests are welcome! For major changes, open an issue first.

---
