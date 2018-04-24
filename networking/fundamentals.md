# Fundamental Cisco Commands
## Debug / Messages
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