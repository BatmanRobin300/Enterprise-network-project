# Enterprise Network Design & Security Simulation

A Cisco Packet Tracer portfolio lab demonstrating VLAN segmentation, router-on-a-stick inter-VLAN routing, DHCP, and extended ACLs.

**Simulation file:** `Enterprise_Network_Simulation.pkt` (open it in Cisco Packet Tracer)

## Requirements
- Cisco Packet Tracer (Cisco Networking Academy)
- One Cisco 2911 router (R1)
- One Cisco 2960 switch (SW1)
- Six PCs (two per VLAN)
- Copper straight-through cables

## Topology
Connect R1 GigabitEthernet0/0 to SW1 GigabitEthernet0/1. Connect PCs to SW1 FastEthernet0/1 through FastEthernet0/6.

| Device | Switch port | VLAN | Department |
|---|---|---|---|
| IT-PC1 | Fa0/1 | 10 | IT |
| IT-PC2 | Fa0/2 | 10 | IT |
| HR-PC1 | Fa0/3 | 20 | HR |
| HR-PC2 | Fa0/4 | 20 | HR |
| SALES-PC1 | Fa0/5 | 30 | Sales |
| SALES-PC2 | Fa0/6 | 30 | Sales |

## IP plan
- VLAN 10 IT: 192.168.10.0/24, gateway 192.168.10.1
- VLAN 20 HR: 192.168.20.0/24, gateway 192.168.20.1
- VLAN 30 Sales: 192.168.30.0/24, gateway 192.168.30.1

DHCP is provided by R1. All PCs should use DHCP.

## Build and load
1. Open Cisco Packet Tracer and create a new blank project.
2. Add the devices and connect them according to `docs/SETUP_GUIDE.md`.
3. Open SW1 > CLI. Press Enter; enter privileged mode with `enable`, then configuration mode with `configure terminal`.
4. Paste the commands from `configs/SW1_switch.txt` **excluding** its comment lines, `enable`, and `configure terminal` (the file is already written as configuration-mode commands). If Packet Tracer drops pasted commands, paste in smaller blocks.
5. Repeat on R1 with `configs/R1_router.txt`.
6. On each PC: Desktop > IP Configuration > DHCP.
7. Run tests in `docs/TEST_PLAN.md`.
8. Save the Packet Tracer project as `Enterprise_Network_Simulation.pkt` using File > Save As.

**Shortcut:** To skip the build, open `Enterprise_Network_Simulation.pkt` directly in Packet Tracer.

## Security behavior
- IT can reach HR and Sales.
- HR can reach IT but cannot initiate traffic to Sales.
- Sales can reach IT but cannot initiate traffic to HR.
- ACLs are basic stateless IPv4 filtering, not a stateful firewall. Some reply traffic between HR and Sales can also be blocked; validate the exact intended flows in Packet Tracer.

## Files
- `configs/R1_router.txt`: router subinterfaces, DHCP, ACLs
- `configs/SW1_switch.txt`: VLANs, access ports, trunk
- `docs/SETUP_GUIDE.md`: detailed GUI setup
- `docs/TEST_PLAN.md`: validation checklist
- `Enterprise_Network_Simulation.pkt`: the finished Packet Tracer project
- `screenshots/`: topology and test results (see `docs/TEST_PLAN.md`)

## Screenshots
_Add your screenshots to the `screenshots` folder, then link them here:_
`![Topology](screenshots/topology.png)`

## Notes
Interface names may differ by device model. Use `show ip interface brief` on the router and `show interfaces status` on the switch to verify them before pasting commands.
