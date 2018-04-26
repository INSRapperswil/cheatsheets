# Table of Contents

[MPLS](#MPLS)

* [Verification](#verification)

# <a name="mpls"></a>MPLS

## <a name="verification"></a>Verification

```bash
show ip cef
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
show ip bgp vpnv6 unicast rd 10.255.255.0:0 detail
```

