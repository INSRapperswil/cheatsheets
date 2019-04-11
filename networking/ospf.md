# Table of Contents

[OSPF](#ospf)

* [OSPFv2 Confguration](#ospfv2_configuration)
* [OSPFv3 Configuration](ospfv3_configuration)
* [OSPF Point to Point](#p2p)
* [Verification](#verification)
* [OSPF Debugging](#ospf_debug)

# <a name="ospf"></a>OSPF

## <a name="ospfv2_configuration"></a>OSPFv2 Configuration

### Single Area

```
router ospf 1
  auto-cost reference-bandwidth 1000
  network 192.168.0.0 0.0.0.3 area 0
  network 192.168.0.12 0.0.0.3 area 0
```

### Multi-Area

```
router ospf 1
  network 192.168.0.0 0.0.0.3 area 1
```

### <a name="interface2ospf"></a>Add Interface to OSPF
```
ip ospf <process-id> area <area-id>
```
**Hint:** When the network is already declared with `router ospf ...` then there is no need to add the interface directly

## <a name="ospfv3_configuration"></a>OSPFv3 Configuration

## <a name="verification"></a>Verification

```
show ip [route | protocols]
show ip ospf interface
show ip ospf neighbor
show ip ospf border-routers
show ip ospf virtual-links
```

## <a name="p2p"></a>Point to Point OSPF
```
ip ospf network point-to-point
```

## <a name="ospf_debug"></a>OSPF Debugging

```
debug ip ospf ?
```
