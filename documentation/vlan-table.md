# VLAN Plan

The project separates each office into department VLANs. VLAN IDs, names, and subnets below follow the supplied project README.

## VLAN allocation

| Network | Office | VLAN ID | VLAN name | Subnet | Inter-VLAN routing method |
|---|---|---:|---|---|---|
| 1 | Main Office | 10 | HR | `192.168.1.0/26` | Router-on-a-Stick (R1) |
| 1 | Main Office | 20 | IT | `192.168.1.64/27` | Router-on-a-Stick (R1) |
| 1 | Main Office | 30 | Finance | `192.168.1.96/28` | Router-on-a-Stick (R1) |
| 2 | Branch Office | 40 | Sales | `172.16.0.0/26` | Separate router interface (R2) |
| 2 | Branch Office | 50 | Marketing | `172.16.0.64/27` | Separate router interface (R2) |
| 2 | Branch Office | 60 | Support | `172.16.0.96/28` | Separate router interface (R2) |
| 3 | Administration Office | 70 | Accounting | `10.0.0.128/26` | Layer 3 switch SVI |
| 3 | Administration Office | 80 | Security | `10.0.0.192/27` | Layer 3 switch SVI |
| 3 | Administration Office | 90 | Management | `10.0.0.0/25` | Layer 3 switch SVI |

## Trunk and native VLAN details

- The Main Office uses trunks between SW1 and SW2 and between SW2 and the router-facing switch connection. The allowed VLAN list in the README is `10,20,30`.
- The Administration Office trunk between the multilayer switch and SW4 allows VLANs `70,90`.
- The native VLAN on the Administration Office trunk is VLAN `999`; it is configured on both ends in the supplied configuration.
- VLAN 80 (Security) is described as existing only on the multilayer switch. It is not allowed on the trunk to SW4 and is not created on SW4.
- The Branch Office design uses separate router interfaces connected to access ports, one VLAN per router interface. The README specifies no subinterfaces and no trunks for this design.

## Switch configuration files

| Device | Configuration file |
|---|---|
| SW1 | [`../configs/switches/SW1.txt`](../configs/switches/SW1.txt) |
| SW2 | [`../configs/switches/SW2.txt`](../configs/switches/SW2.txt) |
| SW3 | [`../configs/switches/SW3.txt`](../configs/switches/SW3.txt) |
| Multilayer switch | [`../configs/switches/MLS.txt`](../configs/switches/MLS.txt) |
| SW4 | [`../configs/switches/SW4.txt`](../configs/switches/SW4.txt) |

See the [main README](../README.md) for the full topology and device configurations.
