# Cisco Packet Tracer — Multi-Subnet Network Design

A computer networking project created in **Cisco Packet Tracer**, featuring a routed, multi-subnet topology with wired and wireless end devices and dedicated server nodes. The editable simulation is included in [`RETELE_TRACKER.pkt`](RETELE_TRACKER.pkt).

## Network topology

![Network topology shown in Cisco Packet Tracer](images/network-topology.png)

The supplied topology screenshot shows:

- **5 routers** (`R1`–`R5`) interconnecting local and transit segments.
- **6 switches**: five access switches (`N1`–`N5`) and one central switch (`Switch1`).
- A **DHCP server**, **DNS server**, and **web server** located in different parts of the topology.
- A **WRT300N wireless router** connected to a smartphone, a PC, and the web-server segment.
- A separate **wireless access point** with a laptop client.
- Multiple PCs connected to different access networks.

These are components visible in the supplied screenshot. The screenshot alone does not establish which routing protocol or device-service settings are enabled.

## IP addressing plan

The following networks and address assignments are transcribed from the notes visible in the topology screenshot. Prefix lengths are **inferred from the listed network and broadcast addresses**; verify the actual configured masks inside Packet Tracer.

| Segment label | Network (inferred CIDR) | Gateway / router IPs shown | Server / other IPs shown | Broadcast |
| --- | --- | --- | --- | --- |
| `n1` | `214.84.237.128/27` | `R1: 214.84.237.129` | `DHCP: 214.84.237.130` | `214.84.237.159` |
| `n2` | `214.84.237.160/27` | `R2: 214.84.237.161` | `Web: 214.84.237.162` (as labeled) | `214.84.237.191` |
| `n3` | `214.84.237.192/28` | `R3: 214.84.237.193` | `DNS: 214.84.237.194` | `214.84.237.207` |
| `n4` | `214.84.237.208/28` | `R4: 214.84.237.209` | — | `214.84.237.223` |
| `n5` | `214.84.237.224/29` | `R5: 214.84.237.225` | — | `214.84.237.231` |
| `n1345` | `214.84.237.232/29` | `R1: .233`, `R3: .234`, `R4: .235`, `R5: .236` | Shared transit segment | `214.84.237.239` |
| `n12` | `214.84.237.240/30` | `R1: .241`, `R2: .242` | Router-to-router link | `214.84.237.243` |
| `n5w` | `214.84.237.244/30` | `R5: .245`, wireless router: `.246` | Wired-to-wireless-router link | `214.84.237.247` |

In the last three rows, shortened addresses (such as `.233`) have the same `214.84.237` prefix. The address block used in the exercise is **not an RFC 1918 private IPv4 range**; it is documented here as a simulation addressing plan, not a recommendation for deployment in a real private LAN.

## Explore the simulation

1. Install and open **Cisco Packet Tracer**.
2. Open [`RETELE_TRACKER.pkt`](RETELE_TRACKER.pkt) using **File → Open**.
3. Inspect the **Logical** workspace, device settings, server configuration, and interface addressing.
4. Use the **Simulation** workspace to observe packet forwarding and test network behavior.

GitHub stores the `.pkt` file but does not execute the Packet Tracer simulation in the browser.

## Suggested verification checks

The topology screenshot shows the planned network, but does not independently prove end-to-end behavior. You can verify it inside Packet Tracer:

- **Interfaces and routing:** Inspect router interfaces and routing tables with `show ip interface brief` and `show ip route`; identify whether routing is static or dynamic.
- **Inter-subnet reachability:** Ping hosts in different LANs and use `tracert` / `traceroute` where supported.
- **DHCP:** On a client configured for DHCP, request an address and check its IP, subnet mask, gateway, and DNS settings.
- **DNS:** Query configured names from a PC and inspect the DNS server's records.
- **HTTP:** Open the web server's IP address or configured DNS name from an end device's browser.
- **Wireless:** Check the SSID, association, IP configuration, and connectivity of the wireless laptop and smartphone.

These are **checks to perform**, not claims that every test has already passed.

## Repository contents

```text
Cisco-Packet-Tracer-Network-Design/
├── RETELE_TRACKER.pkt          # Editable Packet Tracer simulation
├── README.md                   # Project documentation
└── images/
    └── network-topology.png   # Reference topology screenshot
```

## Tools and concepts

**Tool:** Cisco Packet Tracer  
**Concepts represented in the topology:** router/switch interconnection, IPv4 subnetting, transit networks, wired/wireless LANs, DHCP/DNS/web-server nodes, and simulated network troubleshooting.

> **Scope:** Device inventory and addressing above are based on the supplied topology screenshot. The native `.pkt` file is included for opening and checking the exact saved configurations in Packet Tracer; those configurations were not independently extracted or tested for this README.
