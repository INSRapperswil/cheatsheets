# Cisco Commands
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
```