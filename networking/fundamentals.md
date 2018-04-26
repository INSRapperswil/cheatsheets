# Table of Contents

* [Fundamental Cisco Commands](#fundamental)
  * [Debug / Messages](#debug)
  * [Port Mirroring](#port_mirroring)
  * [CLI](#cli)
  * [Cleanup](#cleanup)
  * [Verification](#verification)

# <a name="fundamental"></a>Fundamental Cisco Commands

## <a name="debug"></a>Debug / Messages

### Loggin Messages In SSH Session

```
Router# terminal monitor
```

### Start A Debug

```
debug ?
debug ip ospf 
```

### Stop A Debug

```
no debug ip ospf
```

### Disable All Debug

```
undebug all
```

## <a name="port_mirroring"></a> Port Mirroring

### Local Span Port

Mirroring both directions from `<source interface>` to `<destination interface>`
```
monitor session <session number> source interface <source interface> 
monitor session <session number> destination interface <source interface> encapsulation replicate
```

## <a name="cli"></a>CLI

### Execute Privileged Commnd In Configuration Mode

```
Router(config)# do show ip interfaces brief
```

## <a name="cleanup"></a>Cleanup

```
erase startup-config
delete flash:/vlan.dat
reload
```

## <a name="verification"></a>Verification

`show running-configuration`
- displays the configuration currently running in RAM 

`show startup-configuration`
- displays the saved configuration located in NVRAM