# Table of Contents

[IP Address Configuration](#ip-address-configuration)
* [IPv4](##IPv4)
  * [Switch Interfaces](#switch-interfaces)
  * [Router Interfaces](#router-interfaces)
  * [Loopback Interface](#loopback-interfaces)
* [IPv6](##IPv6)
  * [Switch Interfaces](#switch-interfaces-1)
  * [Router Interfaces](#router-interfaces-1)
  * [Loopback Interface](#loopback-interfaces-1)
  * [Security](#security)
* [Routing](#routing)
[VRF](#vrf)
* [Connectivity](#connectivity)
* [Verification](#verification)

# IP Address Configuration
## IPv4
### Switch Interfaces
#### Layer-3-Switch switchport access vlan
**Note:** _First you have to disable ip routing on the switch with the_ `no ip routing` _command._
```cisco
L3-Switch(config)# interface <interface>
L3-Switch(config-if)# no shutdown
L3-Switch(config-if)# description <interface description>
L3-Switch(config-if)# switchport mode acces
L3-Switch(config-if)# switchport access vlan <vlan-number>
```
#### Layer-3-Switch routed port
**Note:** _First you have to change your switchport into a routed port with the_ `no switchport` _command._
```cisco
L3-Switch(config)# interface <interface>
L3-Switch(config-if)# no switchport
L3-Switch(config-if)# description <interface description>
L3-Switch(config-if)# ip address <ip-address> <subnetmask>
```
#### Switched Virtual Interface (SVI)
```cisco
Switch(config)# interface vlan <vlan-number>
Switch(config-if)# description <vlan-interface description>
Switch(config-if)# ip address <ip-address> <subnetmask>
```
### Router Interfaces
```cisco
Router(config)# interface <interface>
Router(config-if)# description <interface description>
Router(config-if)# ip address <ip-address> <subnetmask>
```

### Loopback Interfaces
**Note:** _An loopback interface is a stable virtual interface on which you can assign layer 3 addresses. It can be used on Cisco switches and routers._
```
Switch-or-Router(config)#interface Loopback <loopback number>
Switch-or-Router(config-if)# ip address <ip-address> <subnetmask>
```

## IPv6

### Switch Interfaces
#### Layer-3-Switch routed port
**Note:** _First you have to change your switchport into a routed port with the_  `no switchport` _command._
```cisco
Switch(config)# interface <interface>
Switch(config-if)# no switchport
Switch(config-if)# description <interface description>
Switch(config-if)# ipv6 address <ip-address>/<subnetmask>
Switch(config-if)# ipv6 address <link-local ip-address> link-local
```

#### Switched Virtual Interface (SVI)
```cisco
Switch(config)# interface vlan <vlan-number>
Switch(config-if)# description <interface description>
Switch(config-if)# ipv6 address <ip-address>/<subnetmask>
Switch(config-if)# ipv6 address <link-local ip-address> link-local
```

### Router Interfaces
```cisco
Router(config)# interface <interface>
Router(config-if)# description <interface description>
Router(config-if)# ipv6 address <ip-address>/<subnetmask>
Router(config-if)# ipv6 address <link-local ip-address> link-local
```

### Loopback Interfaces
**Note:** _An loopback interface is a stable virtual interface on which you can assign layer 3 addresses. It can be used on Cisco switches and routers._
```cisco
Switch-or-Router(config)#interface Loopback <loopback number>
Switch-or-Router(config-if)# ipv6 address <ip-address>/<subnetmask>
Switch-or-Router(config-if)# ipv6 address <link-local ip-address> link-local
```

### Security
#### IPv6 RA Attack
**Note:** _Sets the IPv6 RA preference to high:_
```cisco
L3-Switch-or-Router(config-if)# ipv6 nd router-pref high
```

### IPv6 RA Guard
**Note:** _Creates the specific RA role for access switch ports:_
_The host role will block all RAs and router redirect messages._
_The router role defines what the router is allowed to put into its RAs._
```cisco
L3-Switch-or-Router(config)# ipv6 nd raguard policy HOST
L3-Switch-or-Router(config-nd-raguard)# device-role host
L3-Switch-or-Router(config)# ipv6 nd raguard policy ROUTER
L3-Switch-or-Router(config-nd-raguard)# device-role router
```
_Assignes the plicies of the roles to the switch port:_
```cisco
L3-Switch-or-Router(config-if)# ipv6 nd raguard attach-policy <policy-name>
```

_Output will show the RA guard settings:_
```cisco
L3-Switch-or-Router# show ipv6 nd raguard policy
```

# Routing
## IPv4

### Enable IPv4 Routing Functionality
```cisco
L3-Switch-or-Router(config)# ip routing
```

### Create a IPv4 static route
**Note:** _To provide connectivity between two networks, you always have to establish a route to the destination network and another one from the destination network back to the source network. Only when the so called back-route is configured, the packet will find their way back to the source network and the connection is established._
```cisco
ip route <destination> <mask> <nexthop>
```


## IPv6

### Enable IPv6 Routing Functionality
```cisco
L3-Switch-or-Router(config)# ipv6 unicast-routing
```
### Default Route to its IPv6 Gateway
```cisco
L3-Switch-or-Router(config)# ipv6 route ::/0 <destination>
```

### Create a IPv6 static route
```
ipv6 route <destination>\<prefix length> <nexthop>
```

### IPv6 Prefix Delegation with DHCP client
**Note:** _Configures the interface of the device that connects to the ISP router:_
```cisco
L3-Switch-or-Router(config-if)# ipv6 dhcp client pd <prefix-name>
L3-Switch-or-Router(config-if)# ipv6 address autoconfig default
```

**Note:** _Configures IPv6 addresses on host with the received prefix:_
```cisco
L3-Switch-or-Router(config-if)# ipv6 address <prefix-name> <ip-address>/<subnetmask>
```

### Host interface to use stateful DHCP
```cisco
L3-Switch-or-Router(config-if)# ipv6 nd managed-config-flag
```

### Host interface to use stateless DHCP
```cisco
L3-Switch-or-Router(config-if)# ipv6 nd other-config-flag
```


# VRF

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

### Overview Interface IP Addresses
Gives an overview of all router interfaces, its status and its IP addresses:
```cisco
show ip interface brief
```
### Overview IP Protocols
Displays the configured routing protocols and its parameters:
```cisco
show ip protocols
```

### Display Routing Table
Shows the routing table without VRFs:
```cisco
show ip route
```
Shows the routing table of a specific VRF:
```cisco
show ip route vrf <vrf name>
```

