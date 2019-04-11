# Table of Contents

* [Configuration](#configuration)
  * [Fundamental](#fundamental)
  * [VRF](#vrf)
* [Verification](#verification)

# <a name="mpls"></a>MPLS

## <a name="configuration"></a>Configuration
### <a name="fundamental"></a>Fundamental
**Change MPLS Label Range**
```bash
mpls label range <startvalue> <endvalue>
```
**Activate MPLS on Interface**
```bash
interface <interface>
mpls ip
```
**Override PHP**
```bash
mpls ldp explicit-null
```

### <a name="vrf"></a>VRF
**VRF Definition**
```bash
vrf definition <vrf name>
  rd <ip address>:<AS>
  route-target export <rt>
  route-target import <rt>
  address-family <version (ipv4, ipv6)>
  exit-address-family
```

## <a name="verification"></a>Verification

```bash
!Data-plane FIB
sw01-pod-1#show ip cef
Prefix               Next Hop             Interface
0.0.0.0/0            no route
0.0.0.0/8            drop
0.0.0.0/32           receive
10.0.0.0/24          10.0.1.254           GigabitEthernet1/0/22
10.0.1.0/24          attached             GigabitEthernet1/0/22
10.0.1.0/32          receive              GigabitEthernet1/0/22
10.0.1.1/32          receive              GigabitEthernet1/0/22
10.0.1.254/32        attached             GigabitEthernet1/0/22
10.0.1.255/32        receive              GigabitEthernet1/0/22
10.0.2.0/24          10.0.1.254           GigabitEthernet1/0/22
10.0.3.0/24          10.0.1.254           GigabitEthernet1/0/22
10.0.4.0/24          10.0.1.254           GigabitEthernet1/0/22
10.0.5.0/24          10.0.1.254           GigabitEthernet1/0/22
10.0.6.0/24          10.0.1.254           GigabitEthernet1/0/22
```



```bash
sw01-pod-1#show mpls ldp neighbor
    Peer LDP Ident: 10.255.1.3:0; Local LDP Ident 10.255.1.1:0
	TCP connection: 10.255.1.3.54557 - 10.255.1.1.646
	State: Oper; Msgs sent/rcvd: 3058/3048; Downstream
	Up time: 1d20h
	LDP discovery sources:
	  GigabitEthernet1/0/24, Src IP addr: 10.1.13.3
        Addresses bound to peer LDP Ident:
          10.1.13.3       10.255.1.3
    Peer LDP Ident: 10.255.255.255:0; Local LDP Ident 10.255.1.1:0
	TCP connection: 10.255.255.255.44172 - 10.255.1.1.646
	State: Oper; Msgs sent/rcvd: 1628/1622; Downstream
	Up time: 23:26:02
	LDP discovery sources:
	  GigabitEthernet1/0/22, Src IP addr: 10.0.1.254
        Addresses bound to peer LDP Ident:
          10.255.255.255  10.10.10.10     10.0.0.254      10.0.1.254
          10.0.2.254      10.0.3.254      10.0.4.254      10.0.5.254
          10.0.6.254      10.0.7.254      10.0.8.254      10.0.9.254
```

```bash
! Control-plane LIB
sw03-pod-1#show mpls ldp bindings
  lib entry: 10.0.0.0/24, rev 32
	local binding:  label: 1318
	remote binding: lsr: 10.255.1.1:0, label: 1117
  lib entry: 10.0.1.0/24, rev 8
	local binding:  label: 1306
	remote binding: lsr: 10.255.1.1:0, label: exp-null
  lib entry: 10.0.2.0/24, rev 30
	local binding:  label: 1317
	remote binding: lsr: 10.255.1.1:0, label: 1116
  lib entry: 10.0.3.0/24, rev 28
	local binding:  label: 1316
	remote binding: lsr: 10.255.1.1:0, label: 1115
  lib entry: 10.0.4.0/24, rev 26
	local binding:  label: 1315
	remote binding: lsr: 10.255.1.1:0, label: 1114
```

```bash
!Data-plane LFIB
show mpls forwarding-table
Local      Outgoing   Prefix           Bytes Label   Outgoing   Next Hop
Label      Label      or Tunnel Id     Switched      interface
1300       explicit-n 10.255.1.1/32    0             Gi1/0/24   10.1.13.1
1301       No Label   2001:DB8:1A:1::/64[V]   \
                                       2520          aggregate/Cust_A
1302       No Label   2001:DB8:1B::/64[V]   \
                                       2304          aggregate/Cust_B
1303       No Label   2001:DB8:1B:ABBA::/64[V]   \
                                       0             Gi1/0/1    FE80::CE98:91FF:FE1A:864
1304       No Label   2001:DB8:1B:BEEF::/64[V]   \
                                       0             Gi1/0/1    FE80::CE98:91FF:FE1A:864
1305       No Label   2001:DB8:1B:CAFE::/64[V]   \
                                       0             Gi1/0/1    FE80::CE98:91FF:FE1A:864
1306       explicit-n 10.0.1.0/24      0             Gi1/0/24   10.1.13.1
1307       1104       10.255.255.255/32   \
                                       0             Gi1/0/24   10.1.13.1
Local      Outgoing   Prefix           Bytes Label   Outgoing   Next Hop
Label      Label      or Tunnel Id     Switched      interface
1308       1107       10.255.255.0/32  3186          Gi1/0/24   10.1.13.1
1309       1108       10.10.10.0/24    0             Gi1/0/24   10.1.13.1
```



```bash
sw01-pod-1#show ip bgp vpnv6 unicast rd 10.255.255.0:0 detail
Route Distinguisher: 10.255.255.0:0
BGP routing table entry for [10.255.255.0:0]2001:DB8::/64, version 12
  Paths: (1 available, best #1, no table)
  Not advertised to any peer
  Refresh Epoch 2
  Local
    ::FFFF:10.255.255.0 (metric 3) (via default) from 10.10.10.10 (10.255.255.255)
      Origin incomplete, metric 0, localpref 100, valid, internal, best
      Extended Community: RT:0:0
      Originator: 10.255.255.0, Cluster list: 10.255.255.255
      mpls labels in/out nolabel/127
      rx pathid: 0, tx pathid: 0x0
BGP routing table entry for [10.255.255.0:0]2001:DB8:ABBA::/64, version 13
  Paths: (1 available, best #1, no table)
  Not advertised to any peer
  Refresh Epoch 2
  Local
    ::FFFF:10.255.255.0 (metric 3) (via default) from 10.10.10.10 (10.255.255.255)
      Origin incomplete, metric 0, localpref 100, valid, internal, best
      Extended Community: RT:0:0
      Originator: 10.255.255.0, Cluster list: 10.255.255.255
      mpls labels in/out nolabel/128
      rx pathid: 0, tx pathid: 0x0
```
