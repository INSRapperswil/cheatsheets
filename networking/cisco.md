# Cisco Commands

## IP Address Configuration
### Router
#### IPv4
```
Router(config)# interface <interface>
Router(config-if)# ip address <ip-address> <subnetmask>
```
#### IPv6
```
Router(config)# interface <interface>
Router(config-if)# ipv6 address <ip-address>/<subnetmask>
```
##### Link Local
```
Router(config)# interface <interface>
Router(config-if)# ipv6 address <link-local ip-address> link-local
```
## SVI (Switched Virtual Interface) Configuration

In default setting, an SVI is created for the default VLAN  (VLAN1) to permit remote switch administration. But the VLAN 1 has no interface, you should configure it.

```bash
interface vlan 1
ip address 192.168.0.1 255.255.255.252
ipv6 address 2001:DB8:1::CAFE/64
ipv6 address FE80::BEEF link-local
```

## Loopback Interface Configuration

```bash
int lo3
ip address 172.16.4.1 255.255.255.128
ipv6 address 2003::1/64
description LAN 3
```

## Layer 2 Access Port

This example shows how to configure an Ethernet interface to join VLAN 2:

```bash
interface ethernet 1/7
switchport mode access
switchport access vlan 2
```

## Layer 2 Trunk Port

This example shows how to set Ethernet 3/1 as an Ethernet trunk port:

```bash
interface ethernet 3/1     
switchport mode trunk     
```

## Router

### show commands
`show ip interface brief`
- gives an overview of all router interfaces, its status and its IP address

`show interfaces`
- displays all the statistics of all the interfaces on the router. To view the statistics of a specific interface, enter the show interfaces command followed by the specific interface and port number. For example: Router#show interfaces serial 0/1

`show ip protocols`
- displays the configured routing protocols and its parameters

`show ip route`
- shows the routing table

`show running-configuration`
- displays the configuration currently running in RAM 

`show startup-configuration`
- displays the saved configuration located in NVRAM

## Routing Protocols
### RIP
#### RIPv2 Configuration
```
! Enable RIPv2 IPv4 routing
Router(config)# router rip
Router(config-router)# version 2

! Disable RIPv2 automatic summarization
Router(config-router)# no auto-summary

! Designate RIPv2 interfaces by network
Router(config-router)# network <network>
```

#### RIPng Configuration
```
! Enable IPv6 routing
Router(config)# ipv6 unicast-routing

! Enable RIPng IPv6 routing
Router(config)# ipv6 router rip <rip-instance-name>

! Add a network to Rip
network 192.168.0.0
network 192.168.0.12

! Enable RIPng on the interface
Router(config)# interface <interface>
Router(config-if)# ipv6 rip <rip-instance-name> enable
```

#### RIP Troubleshooting
```
show ip[v6] rip database
show ip[v6] route rip
debug ip rip { database | events }
debug ipv6 rip [interface]

! Disable debugging
undebug all
```

### OSPF
#### Ospf Debug
```bash
debug ip ospf ?
show ip ospf interface
show ip ospf neighbor
show ip route ospf
show ip ospf database
```
#### OSPFv2 Configuration
##### Single Area

```bash
router ospf 1
auto-cost reference-bandwidth 1000 
network 192.168.0.0 0.0.0.3 area 0
network 192.168.0.12 0.0.0.3 area 0
```

##### Multi-Area

```bash
router ospf 1
network 192.168.0.0 0.0.0.3 area 1
```

#### OSPFv3 Configuration

#### OSPF Troubleshooting
```
show ip [route | protocols]
show ip ospf interface
show ip ospf neighbor
show ip ospf border-routers
show ip ospf virtual-links
debug ip ospf […]
```

## Span Ports

### Local Span

Mirroring both directions of GigabitEthernet1/0/1 to GigabitEthernet1/0/2
```
Device(config)# no monitor session 1
Device(config)# monitor session 1 source interface gigabitethernet1/0/1
Device(config)# monitor session 1 destination interface gigabitethernet1/0/2 encapsulation replicate
Device(config)# end
```
## Loggin Messages in ssh session
```bash
terminal monitor
```
## Debug Commands

```bash
debug ?
debug ip ospf 
no debug
no debug ip ospf
undebug all
```

```bash
show ip protocols
show ip route
show ip interfaces
```