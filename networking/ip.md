# IP
## IP Address Configuration
### IPv4
```
interface <interface>
  description Link-to-XY
  ip address <ip-address> <subnetmask>
```
### IPv6
```
interface <interface>
  description Link-to-XY
  ipv6 address <ip-address>/<subnetmask>
  ipv6 address <link-local ip-address> link-local
```

### Interfaces
#### Router
```
interface <interface>
  description Link-to-XY
  ip address ...
```

#### SVI (Switched Virtual Interface)
```
interface vlan <vlan number>
  ip address ...
```

#### L3 Switch Routed Port
```
interface <interface>
  no switchport
  ip address ...
```

#### Loopback Interface
```
interface Loopback <loopback number>
  ip address ...
```

## Routing
### Enable Routing IPv4
```
ip routing
```

### Enable Routing IPv6
```
ipv6 unicast-routing
```

### Static Route
```
ip route <destination> <mask> <nexthop>
ipv6 route <destination>\<prefix length> <nexthop>
```

## VRF
### IPv4 Enabled VRF
```
vrf definition <name>
  address-family ipv4
  exit-address-family
```

### IPv6 Enabled VRF
```
vrf definition <name>
  address-family ipv6
  exit-address-family
```

### Add Interface To VRF
```
interface <interface>
  vrf forwarding <name>
```

### VPN Route Distinguisher
```
vrf definition <name>
  rd <ASN|IP-address|4BASN>:<number>
```
### Route Target
```
vrf definition <name>
  route-target export <ASN|IP-address>:<number>
  route-target import <ASN|IP-address>:<number>
```

## Connectivity
### Ping
```
ping <destination>
```

### Ping With Specific Source
```
ping <destination> source <local IP>
ping <destination> source <interface>
```

### Ping From Specific VRF
```
ping vrf <VRF Name> <destination>
```

### Traceroute
```
traceroute <destination>
```

## Verification
`show ip interface brief`
- gives an overview of all router interfaces, its status and its IP address

`show ip protocols`
- displays the configured routing protocols and its parameters

`show ip route`
- shows the routing table

`show ip route vrf <vrf name>`
- shows the routing table of a specific VRF