# Verification and Testing Results

All checks below were run in Cisco Packet Tracer on the final topology. Commands are from the [main README](../README.md).

![Topology](../images/topology.png)

## 1. VLANs (`show vlan brief`)

**SW1**

![SW1](../images/verification/vlan-sw1.png)

**SW2**

![SW2](../images/verification/vlan-sw2.png)

**SW3**

![SW3](../images/verification/vlan-sw3.png)

**Multilayer switch**

![Multilayer switch](../images/verification/vlan-mls.png)

**SW4**

![SW4](../images/verification/vlan-sw4.png)

## 2. Trunks (`show interfaces trunk`)

Every trunk is 802.1q, trunking, native VLAN 999, with only the needed VLANs allowed.

**SW1 (allows 10,20)**

![SW1 (allows 10,20)](../images/verification/trunk-sw1.png)

**SW2 (G0/1 allows 10,20; G0/2 allows 10,20,30)**

![SW2 (G0/1 allows 10,20; G0/2 allows 10,20,30)](../images/verification/trunk-sw2.png)

**Multilayer switch (allows 70,90)**

![Multilayer switch (allows 70,90)](../images/verification/trunk-mls.png)

**SW4 (allows 70,90)**

![SW4 (allows 70,90)](../images/verification/trunk-sw4.png)

## 3. Interfaces (`show ip interface brief`)

**R1 (subinterfaces .10, .20, .30)**

![R1 (subinterfaces .10, .20, .30)](../images/verification/ipint-r1.png)

**R2**

![R2](../images/verification/ipint-r2.png)

**R3**

![R3](../images/verification/ipint-r3.png)

**Multilayer switch (SVIs 70, 80, 90)**

![Multilayer switch (SVIs 70, 80, 90)](../images/verification/ipint-mls.png)

## 4. Routing tables (`show ip route`)

**R1**

![R1](../images/verification/route-r1.png)

**R2**

![R2](../images/verification/route-r2.png)

**R3**

![R3](../images/verification/route-r3.png)

**Multilayer switch (default route via 10.0.0.226)**

![Multilayer switch (default route via 10.0.0.226)](../images/verification/route-mls.png)

## 5. Ping tests

The first ping in some tests times out while ARP resolves. The remaining replies succeed.

| Test | Source | Destination | Expected | Actual | Status |
|---|---|---|---|---|---|
| Gateway reachability | PC1 | 192.168.1.62 (R1) | Successful ping | 4/4 replies | Pass |
| Same VLAN across switches | PC1 (SW1) | PC2 (SW2), 192.168.1.2 | Successful ping | 4/4 replies | Pass |
| Inter-VLAN, Network 1 (ROAS) | PC1 | PC3, 192.168.1.65 | Successful ping | 3/4 replies (first is ARP) | Pass |
| Inter-VLAN, Network 2 | PC7 | PC9, 172.16.0.65 | Successful ping | 3/4 replies (first is ARP) | Pass |
| Inter-VLAN, Network 3 (SVI) | PC13 | PC15, 10.0.0.130 | Successful ping | 3/4 replies (first is ARP) | Pass |
| Network 3 to Network 1 | PC13 | PC1, 192.168.1.1 | Successful ping | 4/4 replies | Pass |
| Network 1 to Network 3 | PC1 | PC13, 10.0.0.1 | Successful ping | 4/4 replies | Pass |
| Network 1 to Network 2 | PC1 | PC8, 172.16.0.2 | Successful ping | 3/4 replies (first is ARP) | Pass |
| Network 3 to Network 2 | PC13 | PC7, 172.16.0.1 | Successful ping | 4/4 replies | Pass |

**PC1 to its gateway**

![PC1 to its gateway](../images/verification/ping-gateway-pc1.png)

**PC1 to PC2, same VLAN across switches**

![PC1 to PC2, same VLAN across switches](../images/verification/ping-same-vlan.png)

**Inter-VLAN, Network 1**

![Inter-VLAN, Network 1](../images/verification/ping-intervlan-n1.png)

**Inter-VLAN, Network 2**

![Inter-VLAN, Network 2](../images/verification/ping-intervlan-n2.png)

**Inter-VLAN, Network 3**

![Inter-VLAN, Network 3](../images/verification/ping-intervlan-n3.png)

**PC13 to PC1**

![PC13 to PC1](../images/verification/ping-pc13-pc1.png)

**PC1 to PC13**

![PC1 to PC13](../images/verification/ping-pc1-pc13.png)

**PC1 to Network 2**

![PC1 to Network 2](../images/verification/ping-pc1-pc7.png)

**PC13 to PC7**

![PC13 to PC7](../images/verification/ping-pc13-pc7.png)

For the addressing plan, see [addressing-table.md](addressing-table.md). For VLAN details, see [vlan-table.md](vlan-table.md).
