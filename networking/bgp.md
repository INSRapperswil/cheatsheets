# Table of Contents

[BGP](#ggp)

* [BGP IPv4](#bpg_ipv4)
* [BGP IPv6](#bgp_ipv6)
* [BGP Disable IPv4 Unicast Default](#bgp_disable)
* [Verification](#verification)

# <a name="bgp"></a>BGP

##<a name="bgp_ipv4"></a> BGP IPv4

```
router bgp <local AS>
  neighbor <IP Address> remote-as <remote AS>
```

## <a name="bgp_ipv6"></a>BGP IPv6

```
router bgp <local AS>
  neighbor <IP Address> remote-as <remote AS>
  address-family ipv4
    no neighbor <IP Address> activate
  exit-address-family
  address-family ipv6
    neighbor <IP Address> activate
  exit-address-family
```

## <a name="bgp_disable"></a>BGP Disable IPv4 Unicast Default

Disable activate ipv4-unicast for a peer by default
```
router bgp <local AS>
  no bgp default ipv4-unicast
```

## <a name="verification"></a>Verification

`show ip bgp summary`
- Summary of BGP IPv4 neighbor status

`show ip bgp ipv4 unicast summary`
- Summary of BGP IPv4 neighbor status

`show ip bgp ipv6 unicast summary`
- Summary of BGP IPv6 neighbor status

`show ip bgp`
- IPv4 BGP Prefixes

`show ip bgp ipv6 unicast`
- IPv6 BGP Prefixes