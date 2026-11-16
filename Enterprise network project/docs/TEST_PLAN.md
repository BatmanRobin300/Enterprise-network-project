# Validation Test Plan

## CLI checks
Router (R1):
- `show ip interface brief` — physical GigabitEthernet0/0 and subinterfaces should be up/up.
- `show ip dhcp binding` — six DHCP leases should appear after PCs request addresses.
- `show access-lists` — ACL 120 and 130 should appear.

Switch (SW1):
- `show vlan brief` — ports Fa0/1-2 VLAN 10, Fa0/3-4 VLAN 20, Fa0/5-6 VLAN 30.
- `show interfaces trunk` — Gi0/1 should be trunking VLANs 10,20,30.

## PC checks
Each PC: Desktop > Command Prompt > `ipconfig`.
- IT PCs: 192.168.10.21-254, gateway 192.168.10.1
- HR PCs: 192.168.20.21-254, gateway 192.168.20.1
- Sales PCs: 192.168.30.21-254, gateway 192.168.30.1

## Ping tests
Use actual DHCP-assigned target IPs (do not assume fixed host addresses).
- IT-PC1 -> IT-PC2: PASS expected.
- IT-PC1 -> HR-PC1: PASS expected.
- IT-PC1 -> SALES-PC1: PASS expected.
- HR-PC1 -> SALES-PC1: FAIL expected (ACL 120).
- SALES-PC1 -> HR-PC1: FAIL expected (ACL 130).
- Any PC -> its own default gateway: PASS expected.

Note: Initial ping may time out while ARP resolves; retry. ACLs here are stateless, so HR/Sales replies to cross-VLAN traffic may be blocked. The lab does not simulate Internet access.

## Evidence to save
- Screenshot of topology
- `show vlan brief`
- `show interfaces trunk`
- `show ip interface brief`
- `show ip dhcp binding`
- `show access-lists`
- Successful and blocked ping screenshots
