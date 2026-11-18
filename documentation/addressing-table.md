# IP Addressing Plan (VLSM)

This document records the IP addressing plan from the project README. The project uses three parent networks and assigns subnets according to the host requirements.

## Network 1 — Main Office

Parent block: `192.168.1.0/24`

| Department | VLAN | Hosts needed | Network | Subnet mask | First usable | Gateway (last usable) | Broadcast | Usable hosts |
|---|---:|---:|---|---|---|---|---|---:|
| HR | 10 | 40 | `192.168.1.0/26` | `255.255.255.192` | `192.168.1.1` | `192.168.1.62` | `192.168.1.63` | 62 |
| IT | 20 | 24 | `192.168.1.64/27` | `255.255.255.224` | `192.168.1.65` | `192.168.1.94` | `192.168.1.95` | 30 |
| Finance | 30 | 12 | `192.168.1.96/28` | `255.255.255.240` | `192.168.1.97` | `192.168.1.110` | `192.168.1.111` | 14 |

## Network 2 — Branch Office

Parent block stated in the README: `172.16.0.0/16` (`172.16.0.0/24` used)

| Department | VLAN | Hosts needed | Network | Subnet mask | First usable | Gateway (last usable) | Broadcast | Usable hosts |
|---|---:|---:|---|---|---|---|---|---:|
| Sales | 40 | 50 | `172.16.0.0/26` | `255.255.255.192` | `172.16.0.1` | `172.16.0.62` | `172.16.0.63` | 62 |
| Marketing | 50 | 25 | `172.16.0.64/27` | `255.255.255.224` | `172.16.0.65` | `172.16.0.94` | `172.16.0.95` | 30 |
| Support | 60 | 10 | `172.16.0.96/28` | `255.255.255.240` | `172.16.0.97` | `172.16.0.110` | `172.16.0.111` | 14 |

## Network 3 — Administration Office

Parent block stated in the README: `10.0.0.0/8` (`10.0.0.0/24` used)

| Department | VLAN | Hosts needed | Network | Subnet mask | First usable | Gateway (last usable) | Broadcast | Usable hosts |
|---|---:|---:|---|---|---|---|---|---:|
| Management | 90 | 100 | `10.0.0.0/25` | `255.255.255.128` | `10.0.0.1` | `10.0.0.126` | `10.0.0.127` | 126 |
| Accounting | 70 | 45 | `10.0.0.128/26` | `255.255.255.192` | `10.0.0.129` | `10.0.0.190` | `10.0.0.191` | 62 |
| Security | 80 | 20 | `10.0.0.192/27` | `255.255.255.224` | `10.0.0.193` | `10.0.0.222` | `10.0.0.223` | 30 |

## PC address assignments

The project uses the first usable address for the first PC, the second usable address for the second PC, and the last usable address as the default gateway.

| PC | VLAN | IP address | Subnet mask | Default gateway |
|---|---:|---|---|---|
| PC1 | 10 | `192.168.1.1` | `255.255.255.192` | `192.168.1.62` |
| PC2 | 10 | `192.168.1.2` | `255.255.255.192` | `192.168.1.62` |
| PC3 | 20 | `192.168.1.65` | `255.255.255.224` | `192.168.1.94` |
| PC4 | 20 | `192.168.1.66` | `255.255.255.224` | `192.168.1.94` |
| PC5 | 30 | `192.168.1.97` | `255.255.255.240` | `192.168.1.110` |
| PC6 | 30 | `192.168.1.98` | `255.255.255.240` | `192.168.1.110` |
| PC7 | 40 | `172.16.0.1` | `255.255.255.192` | `172.16.0.62` |
| PC8 | 40 | `172.16.0.2` | `255.255.255.192` | `172.16.0.62` |
| PC9 | 50 | `172.16.0.65` | `255.255.255.224` | `172.16.0.94` |
| PC10 | 50 | `172.16.0.66` | `255.255.255.224` | `172.16.0.94` |
| PC11 | 60 | `172.16.0.97` | `255.255.255.240` | `172.16.0.110` |
| PC12 | 60 | `172.16.0.98` | `255.255.255.240` | `172.16.0.110` |
| PC13 | 90 | `10.0.0.1` | `255.255.255.128` | `10.0.0.126` |
| PC14 | 70 | `10.0.0.129` | `255.255.255.192` | `10.0.0.190` |
| PC15 | 70 | `10.0.0.130` | `255.255.255.192` | `10.0.0.190` |
| PC16 | 80 | `10.0.0.193` | `255.255.255.224` | `10.0.0.222` |
| PC17 | 80 | `10.0.0.194` | `255.255.255.224` | `10.0.0.222` |

## Router-to-router and routed links

| Link | Subnet | Side A | Side B |
|---|---|---|---|
| R1 G1/0 ↔ R2 G4/0 | `192.168.2.0/30` | R1: `192.168.2.1` | R2: `192.168.2.2` |
| R2 G3/0 ↔ R3 G1/0 | `10.0.1.0/30` | R2: `10.0.1.1` | R3: `10.0.1.2` |
| R3 G0/0 ↔ Multilayer SW G0/2 | `10.0.0.224/30` | R3: `10.0.0.226` | Multilayer SW: `10.0.0.225` |

## VLSM sizing reference

The README applies the host-sizing rule `2^n - 2 >= required hosts`.

| Required hosts | Prefix | Usable addresses |
|---:|---:|---:|
| 100 | `/25` | 126 |
| 50, 45, 40 | `/26` | 62 |
| 25, 24, 20 | `/27` | 30 |
| 12, 10 | `/28` | 14 |

For the overall topology and configuration, see the [main README](../README.md).
