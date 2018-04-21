# OSPF
## OSPFv2 Configuration
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

## OSPFv3 Configuration

## Verification
```
show ip [route | protocols]
show ip ospf interface
show ip ospf neighbor
show ip ospf border-routers
show ip ospf virtual-links
```
## OSPF Debugging
```
debug ip ospf ?
```