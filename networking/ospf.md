# Table of Contents

[OSPF](#ospf)

* [OSPFv2 Configuration](#ospfv2-configuration)
* [OSPFv3 Configuration](#ospfv3-configuration)
* [Point to Point OSPF](#point-to-point-ospf)
* [Wildcard](#wildcard)
* [Verification](#verification)
* [OSPF Debugging](#ospf-debugging)
* [Remove OSPF Configuration](#remove-ospf-configuration)

# OSPF

## OSPFv2 Configuration
### Router ID
**Note:** _The Router ID is a 32 bit number in dotted-decimal notation like an IP address. It is freely assignable but best practise is to use the device-name number._
```
Router(config)# router-id <device-name-number>
```


### Single Area
**Note:** The area-id in a single-area is usually set to `0`.
```
Router(config)# router ospf <process-id>
Router(config-router)#   auto-cost reference-bandwidth 1000
Router(config-router)#   network <network-address> <wildcard-mask> area <area-id>
```

### Multi-Area
**Note:** The area-id `0` in multi-area is always reserved for the backbone area.
```
router ospf <process-id>
  network <network-address> <wildcard-mask> area <area-id>
```

### Change Area into Stub Area
```
Router(config)# router ospf <process-id>
Router(config-router)# area <area-id> stub
```

### Change Area into Totally Stub Area
```
Router(config)# router ospf <process-id>
Router(config-router)# area <area-id> stub no-summary
```


### Add Interface to OSPF
**Hint:** _When the network is already declared with `router ospf ...` then there is no need to add the interface directly_
```
Router(config-if)# ip ospf <process-id> area <area-id>
```

### Configure a Passive Interface
```
Router(config)# router ospf <ospf-process-id>
Router(config-router)# passive-interface <interface-number>
```

### Set Link Speed on Serial Interface
For example to 32 kbit/s:
```
Router(config-if)# clock rate 32000
Router(config-if)# bandwidth 32
```
To set it back:
```
Router(config-if)# speed auto
```

### Redistribute connected Subnets
```
Router(config)# router ospf <process-id>
Router(config-router)# redistribute connected subnets
```

### Virtual Link
```
Router(config)# router ospf <process-id>
Router(config-if)# area <area-id> virtual-link <neighbour-router-id>
```

## OSPFv3 Configuration

## Wildcard
The wildcard masks are in use to define a range of network addresses, therefore they consist also of 32 bits. To get the mask you have to substract the desired subnt mask from 255.255.255.255:
```
  255.255.255.255
- 255.255.254.0        (desired subnet mask /23)
  ---------------
    0.  0.  1.255      (Wildcard mask)
```

## Verification
```
show ip [route | protocols]
show ip ospf interface
show ip ospf interface brief
show ip ospf neighbor
show ip ospf border-routers
show ip ospf virtual-links
```

## Point to Point OSPF
```
ip ospf network point-to-point
```

## OSPF Debugging
```
debug ip ospf ?
debug ip ospf packet    -> OSPF protocol changes
debug ip ospf adj       -> neighbor adjacency changes
```

## Remove OSPF Configuration
```
Router(config)# no router ospf <process-id>
```