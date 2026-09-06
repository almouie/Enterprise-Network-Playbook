Markdown

# Lab 1: Layer 2 Port Security & Errdisable Automatic Recovery

## 📝 Overview
This lab demonstrates the configuration and verification of **Cisco Port Security** on Access switches to mitigate unauthorized MAC address connections, prevent **MAC Address Flooding attacks**, and automate operational recovery using **Errdisable Auto-Recovery**.

---

## 🗺️ Topology & Architecture
Markdown

# Lab 1: Layer 2 Port Security & Errdisable Automatic Recovery

## 📝 Overview
This lab demonstrates the configuration and verification of **Cisco Port Security** on Access switches to mitigate unauthorized MAC address connections, prevent **MAC Address Flooding attacks**, and automate operational recovery using **Errdisable Auto-Recovery**.

---

## 🗺️ Topology & Architecture


🛡️ Key Security Features Implemented

    MAC Address Limit: Strictly enforced maximum allowed MAC addresses (maximum 1).

    Dynamic Sticky Learning: Dynamically learned MAC address converted into running-config (mac-address sticky).

    Violation Strategy: Hardware shutdown of interface upon detecting unauthorized frame source (violation shutdown).

    Automatic Mitigation Recovery: Automated interface restoration after a predefined quiet period (errdisable recovery).

💻 CLI Configuration
1. Hardening Access Port
Plaintext

interface <access-interface>
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown

2. Configuring Errdisable Automatic Recovery
Plaintext

errdisable recovery cause psecure-violation
errdisable recovery interval 30

🧪 Verification & Output Analysis
Inspect Port Security State
Plaintext

SW1# show port-security interface <access-interface>

    Port Security: Enabled

    Port Status: Secure-up / Secure-shutdown (when violated)

    Violation Mode: Shutdown

Verify Active Security Table
Plaintext

SW1# show port-security address

Check Auto-Recovery Status
Plaintext

SW1# show errdisable recovery


---


🛡️ Key Security Features Implemented

    MAC Address Limit: Strictly enforced maximum allowed MAC addresses (maximum 1).

    Dynamic Sticky Learning: Dynamically learned MAC address converted into running-config (mac-address sticky).

    Violation Strategy: Hardware shutdown of interface upon detecting unauthorized frame source (violation shutdown).

    Automatic Mitigation Recovery: Automated interface restoration after a predefined quiet period (errdisable recovery).

💻 CLI Configuration
1. Hardening Access Port
Plaintext

interface <access-interface>
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown

2. Configuring Errdisable Automatic Recovery
Plaintext

errdisable recovery cause psecure-violation
errdisable recovery interval 30

🧪 Verification & Output Analysis
Inspect Port Security State
Plaintext

SW1# show port-security interface <access-interface>

    Port Security: Enabled

    Port Status: Secure-up / Secure-shutdown (when violated)

    Violation Mode: Shutdown

Verify Active Security Table
Plaintext

SW1# show port-security address

Check Auto-Recovery Status
Plaintext

SW1# show errdisable recovery


---

