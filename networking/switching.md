# Table of Contents

[Layer 2 Configuration](#layer2_config)

* [Ports](#ports)
* [Verification](#verification)

# <a name="layer2_config"></a>Layer 2 Configuration

## <a name="ports"></a>Ports

### Access Port
```
interface <interface>
  switchport mode access
  switchport access vlan <vlan number>
```

### Trunk Port
```
interface <interface>     
  switchport mode trunk     
```


## <a name="verification"></a>Verification
`show interfaces status`
- displays an overview of all interfaces

`show interfaces trunk`
- displays all trunk interfaces

`show interfaces`
- displays all the statistics of all the interfaces on the router. To view the statistics of a specific interface, enter the show interfaces command followed by the specific interface and port number. For example: Router#show interfaces serial 0/1