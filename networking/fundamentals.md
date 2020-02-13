# Table of Contents

[Fundamental Cisco Commands](#fundamental-cisco-commands)
  * [Debug / Messages](#debug-/-messages)
  * [Port Mirroring](#port-mirroring)
  * [CLI](#cli)
  * [Cleanup](#cleanup)
  * [Verification](#verification)

# Fundamental Cisco Commands
## Debug / Messages
### Loggin Messages In SSH Session
```
Router# terminal monitor
```

### General Configuration
To improve the experience with the CLI:
```
no ip domain-lookup
line console 0
  logging synchronous
  exec-timeout 0 0
  exit
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

## Port Mirroring
### Local Span Port

Mirroring both directions from `<source interface>` to `<destination interface>`
```
monitor session <session number> source interface <source interface>
monitor session <session number> destination interface <source interface> encapsulation replicate
```

## CLI
### Execute Privileged Commnd In Configuration Mode
```
Router(config)# do show ip interfaces brief
```

## Cleanup
```
erase startup-config
delete flash:/vlan.dat
reload
```

## Verification
`show running-configuration`
- displays the configuration currently running in RAM

`show startup-configuration`
- displays the saved configuration located in NVRAM