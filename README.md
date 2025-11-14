# Lab VLAN & Inter-VLAN Routing (Router-on-a-Stick)

## Objectifs
- Créer 4 VLAN sur 2 réseaux distincts
- Configurer un trunk sur le switch
- Configurer des sous-interfaces sur le routeur (Router-on-a-Stick)
- Tester la communication intra-VLAN et inter-VLAN

## Topologie
- Réseau 1 : VLAN 10 & VLAN 20
- Réseau 2 : VLAN 30 & VLAN 40
- Routeur connecté en trunk à chaque switch
- PC1 → PC8 connectés aux VLAN appropriés

## Adressage IP

| VLAN | PC | IP | Gateway |
|------|----|----|---------|
| 10 | PC1 | 192.168.10.10 | 192.168.10.1 |
| 10 | PC2 | 192.168.10.11 | 192.168.10.1 |
| 20 | PC3 | 192.168.20.10 | 192.168.20.1 |
| 20 | PC4 | 192.168.20.11 | 192.168.20.1 |
| 30 | PC5 | 192.168.30.10 | 192.168.30.1 |
| 30 | PC6 | 192.168.30.11 | 192.168.30.1 |
| 40 | PC7 | 192.168.40.10 | 192.168.40.1 |
| 40 | PC8 | 192.168.40.11 | 192.168.40.1 |

## Commandes principales

### Switch
```bash
vlan 10
vlan 20
vlan 30
vlan 40
interface range fa0/1 - 6
switchport mode access
switchport access vlan 10
interface range fa0/7 - 12
switchport mode access
switchport access vlan 20
interface g0/1
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 10,20
interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
interface g0/1.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
interface g0/1.40
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0
no shutdown
