# Table of Contents

[RIP](#rip)

* [RIPv2 Configuration](#ripv2_configuration)
* [RIPng Configuration](#ripng_configuration)
* [RIP Troubleshooting](#rip_trouble)

# RIP

## <a name="ripv2_configuration"></a>RIPv2 Configuration

```
! Enable RIPv2 IPv4 routing
Router(config)# router rip
Router(config-router)# version 2

! Disable RIPv2 automatic summarization
Router(config-router)# no auto-summary

! Designate RIPv2 interfaces by network
Router(config-router)# network <network>
```

## <a name="ripng_configuration"></a>RIPng Configuration

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

## <a name="rip_trouble"></a>RIP Troubleshooting

```
show ip[v6] protocols
show ip[v6] rip database
show ip[v6] route rip
debug ip rip { database | events }
debug ipv6 rip [interface]
```
