# Table of Contents

[IS IS](#is-is)
* [Configuration](#configuration)
* [Redistribution](#redistribution)
* [Route Leaking](#route-leaking)
* [Verification](#verification)



# IS IS
## Verification
```
Switch-or-Router# show isis database level-1 verbose
Switch-or-Router# show isis database level-2 verbose
```

```
Switch-or-Router# show isis neighbors

System Id      Type Interface   IP Address      State Holdtime Circuit Id
R1             L1   Fa0/0       10.0.13.1       UP    8        R1.02
R2             L1L2 Se0/0/0     10.0.23.2       UP    21       00
SW2            L2   Fa0/1       10.0.203.20     UP    8        SW2.01
```

## Configuration
**Note:** _Use for the NET-ID (Network Entity Title) a combination of AFI (Authority and Format Identifier) and the Device ID._
### Routers
```
Router(config)# router isis
Router(config-router)# net <net-id>
Router(config-router)# is-type level-1          <-! for a Level2-Router: level-1-2
Router(config-router)# log-adjacency-changes

Router(config)# interface <interface-number>
Router(config-if)# ip address <ip-address> <subnet-mask>
Router(config-if)# ip router isis
Router(config-if)# no shutdown
```

### Layer 3 Switches
```
Switch(config)# ip routing
Switch(config)# router isis
Switch(config-switch)# net <net-id>
Switch(config-switch)# log-adjacency-changes

Switch(config)# interface <interface-number>
Switch(config-if)# no switchport
Switch(config-if)# ip address <ip-address> <subnet-mask>
Switch(config-if)# ip router isis
Switch(config-if)# no shutdown
```

## Redistribution
### Route-maps
**Note:** Route-maps have always an implicit deny entry at the end.
```
Switch-or-Router(config)# ip access-list standard <acl-name>
Switch-or-Router(config-acl)# permit <ip-address>

Switch-or-Router(config)# route-map <route-map-name> permit <acl-number>
Switch-or-Router(config-route-map)# match ip address <acl-name>

Switch-or-Router(config)# router isis
Switch-or-Router(config-router)# redistribute connected route-maped <route-map-name> level-1
```

## Route Leaking
```
Switch-or-Router(config)# ip access-list standard <leak-acl-name>
Switch-or-Router(config-acl)# permit <ip-address>

Switch-or-Router(config)# route-map <leak-route-map-name> permit <acl-number>
Switch-or-Router(config-route-map)# match ip address <leak-acl-name>

Switch-or-Router(config)# router isis
Switch-or-Router(config-router)# redistribute isis ip level-2 into level-1 route-map <leak-route-map-name>
````
