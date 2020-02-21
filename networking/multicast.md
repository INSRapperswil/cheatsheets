# Table of Contents

[Multicast](#multicast)
* [IGMP](#igmp)
* [PIM Dense Mode](#pim-dense-mode)
* [PIM Sparse Mode](#pim-sparse-mode)
* [Source Specific Multicast SSM](#source-specific-multicast-ssm)
* [Verification](#verification)


# Multicast
## Configuration
To enable ip routing on the whole switch:
```
Switch(config)# ip routing
```

To enable multicast routing on the whole switch:
```
Switch(config)# ip multicast-routing
```

## IGMP
### Configuration
To enforce the vlan to join the multicast group:
```
Switch(config)# interface vlan <vlan-number>
Switch(config-if)# ip igmp join-group <multicast-group-address>
```

```
Switch(config-if)# ip igmp version 3
```

### Snooping
```
Switch# ip igmp snooping
Switch# ip igmp snooping vlan <vlan-number>
```

### Verification
```
Switch# show ip igmp snooping groups
Switch# show ip igmp snooping groups vlan <vlan-number>
Switch# show ip igmp snooping querier
```

### Degugging
```
Switch# debug ip igmp <multicast-group-address>
```

## PIM Dense Mode
Activating PIM Dense Mode on the interface:
```
Switch(config)# interface <interface>
Switch(config-if)# ip pim dense-mode
```

Configure the SVI on a switch to act in PIM Dense Mode:
```
Switch# interface vlan <vlan-number>
Switch(config)# ip pim dense-mode
```

### Verification
```
Switch# show ip pim neighbor
```



## PIM Sparse Mode
Activating PIM Sparse Mode on the interface:
```
Switch(config)# interface <interface>
Switch(config-if)# ip pim sparse-mode
```

Configure interface as a RP:
```
Switch(config)# ip pim rp-address <ip-address>
```

## Source Specific Multicast SSM
Global switch configuration:
```
Switch(config)# ip pim ssm default
```

To let the interface join the SSM group:
```
Switch(config-if)# ip igmp join-group <multicast-group-address> source <source-address>
```

## Verification
```
Switch# show mac address-table
```
To see the full content of the IP multicast routing table:
```
Switch# show ip mroute
```

To see the full content of the IP multicast routing table of the group:
```
Switch# show ip mroute <multicast-group-address>
```
