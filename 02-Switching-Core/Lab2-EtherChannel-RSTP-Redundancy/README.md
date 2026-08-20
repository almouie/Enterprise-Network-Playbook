Markdown

# Lab 2: Enterprise Switching Redundancy: LACP EtherChannel & Rapid PVST+ (RSTP)

## 📝 Objective
The objective of this lab is to build a highly available and resilient Layer 2 enterprise switching architecture. It combines link aggregation using **LACP EtherChannel** for high bandwidth with **Rapid PVST+** for fast loop prevention, alongside edge port security (**PortFast & BPDU Guard**).

## 🗺️ Network Topology
```text
           [ SW1 - Root Primary ]
            //               \
      (EtherChannel           (Single Trunk Link)
       Port-Channel 1)          |
          //                    \
       [ SW2 ] ---------------- [ SW3 ]
   (Root Secondary)  (Single Trunk)   \ (Access Port)
                                       [ PC1 ]

🔑 Key Technologies & Concepts

    Link Aggregation (LACP): Bundled physical links into a logical Port-channel 1 between SW1 and SW2 using standard LACP (active mode) for increased bandwidth and redundancy.

    Full 802.1Q Trunking: Standardized trunking across all inter-switch interfaces to ensure proper BPDU transport per VLAN and prevent topology calculation errors.

    Rapid PVST+ (802.1w): Upgraded STP operation mode to achieve sub-second convergence.

    Root Bridge Manipulation: Explicitly configured SW1 as Primary Root Bridge (priority 24576) and SW2 as Secondary Root (priority 28672).

    Edge Port Security: Applied PortFast and BPDU Guard on SW3 access interfaces to ensure instantaneous endpoint transition while preventing unauthorized rogue switch attachment.

⚙️ Configuration Snippets
1. LACP EtherChannel Configuration (SW1 & SW2)
Plaintext

Switch(config)# interface range Ethernet 0/0 - 1
Switch(config-if-range)# switchport trunk encapsulation dot1q
Switch(config-if-range)# switchport mode trunk
Switch(config-if-range)# channel-group 1 mode active
Switch(config-if-range)# exit

Switch(config)# interface port-channel 1
Switch(config-if)# switchport mode trunk

2. Rapid PVST+ & Root Bridge Configuration
Plaintext

! Enable Rapid PVST+ on all switches
Switch(config)# spanning-tree mode rapid-pvst

! SW1 (Primary Root)
SW1(config)# spanning-tree vlan 1 root primary

! SW2 (Secondary Root)
SW2(config)# spanning-tree vlan 1 root secondary

3. Edge Security Configuration (SW3 Endpoint Interface)
Plaintext

SW3(config)# interface Ethernet 1/1
SW3(config-if)# switchport mode access
SW3(config-if)# spanning-tree portfast
SW3(config-if)# spanning-tree bpduguard enable

✅ Verification & Validation

    EtherChannel Status: Verified via show etherchannel summary. Po1 displays SU status (Layer 2 & In-use).

    Trunking Verification: Confirmed active trunk links across all inter-switch interfaces via show interface trunk.

    STP Topology Stability: Confirmed via show spanning-tree on SW3 that e0/3 is designated as Root Port (FWD) and e0/2 remains stably in Alternate/Blocking (BLK) state, keeping the topology loop-free during edge link state updates.


---
