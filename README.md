### Ghost-Bridge 👻

**Ghost-Bridge** is a Python-based Man-in-the-Middle (MITM) framework that performs ARP Spoofing to intercept, manipulate, and sniff traffic on a local network. It features a modular architecture with three distinct components: Reconnaissance, Attack, and Surveillance.

---

### ⚠️ Disclaimer
**FOR EDUCATIONAL PURPOSES ONLY.**
This software is intended for use on networks you own or have explicit permission to test. Unauthorized interception of data is a violation of the Computer Fraud and Abuse Act (CFAA) and other local laws. The developer assumes no responsibility for misuse.

---

### 🛠️ Features

* **Reconnaissance (`get_mac.py`):**
    * Scans the local LAN for active devices.
    * Maps IP addresses to MAC addresses.
    * Detects the Gateway (Router) automatically.

* **Attack (`spoof.py`):**
    * Performs ARP Poisoning on both the Target and the Gateway.
    * Enables IP Forwarding to maintain the victim's internet connection (Invisible Bridge).
    * Includes a "Kill Switch" mode (DoS) if forwarding is disabled.

* **Surveillance (`spy.py`):**
    * Sniffs DNS queries in real-time.
    * Filters traffic to show only websites visited by the specific target.
    * Ignores background noise and non-target traffic.

---

### 🚀 Installation

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/Trex2013/Ghost-Bridge.git](https://github.com/Trex2013/Ghost-Bridge.git)
    cd Ghost-Bridge
    ```

2.  **Install Dependencies:**
    You need Python 3 and Scapy.
    ```bash
    pip install scapy
    ```

3.  **Requirements (Windows):**
    * Install **Npcap** (Ensure "Install in WinPcap API-compatible Mode" is checked).
    * Enable **IP Forwarding** in Windows Registry (required for MITM mode):
        ```powershell
        Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters" -Name "IPEnableRouter" -Value 1
        ```

---

### 💀 Usage

**Step 1: The Bridge (Attack):**
Start the ARP Spoofer in a dedicated terminal. This establishes the MITM connection.

```bash
python spoof.py
```
Select the target device from the list.

**Step 2: The Eye (Sniffer):** 
Open a new terminal and run the spy module to watch the traffic.

```bash
python spy.py
```


### 🧩 Architecture

> **Layer 2 Injection:** Uses raw Ethernet frames to bypass Scapy's broadcast warnings.

> **Persistent Looping:** Sends spoof packets every 0.5s to combat Router ARP refreshing.

> **Packet Filtering:** Uses Scapy's BPF syntax (udp port 53) to strictly capture DNS requests.



