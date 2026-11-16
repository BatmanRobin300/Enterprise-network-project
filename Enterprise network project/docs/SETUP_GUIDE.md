# Packet Tracer Setup Guide

1. Download/install Packet Tracer from Cisco Networking Academy: https://www.netacad.com/resources/lab-downloads
2. Launch Packet Tracer, sign in if prompted, and choose File > New.
3. Bottom-left Network Devices > Routers: drag a **2911** router onto the canvas. Rename it **R1**.
4. Network Devices > Switches: drag a **2960** switch onto the canvas. Rename it **SW1**.
5. End Devices > PC: add six PCs and rename them IT-PC1, IT-PC2, HR-PC1, HR-PC2, SALES-PC1, SALES-PC2.
6. Connections (lightning bolt) > Copper Straight-Through: connect router GigabitEthernet0/0 to switch GigabitEthernet0/1.
7. Connect the six PCs' FastEthernet0 interfaces to switch Fa0/1 through Fa0/6 in the order in README.md.
8. Click SW1 > CLI. Press Enter. Type `enable`, then `configure terminal`. Paste switch configuration from `configs/SW1_switch.txt` in small blocks. Its last two commands (`end` and `write memory`) leave configuration mode and save the switch.
9. Click R1 > CLI. Press Enter. Type `enable`, then `configure terminal`. Paste router configuration from `configs/R1_router.txt` in small blocks. Its last two commands save the router.
10. Wait for green link indicators. On every PC, select Desktop > IP Configuration > DHCP. Verify each PC gets a 192.168.X address for its VLAN.
11. Follow `TEST_PLAN.md` and save with File > Save As > `Enterprise_Network_Simulation.pkt`.

Troubleshooting: If a command is rejected, check the device model and interface names. On the router use `show ip interface brief`; on the switch use `show vlan brief` and `show interfaces trunk`. In Packet Tracer, large paste operations can lose commands, so paste smaller sections.
