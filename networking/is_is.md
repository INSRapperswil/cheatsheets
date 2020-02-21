# Table of Contents

[IS IS](#is-is)
* [Configuration](#configuration)
* [Redistribution](#redistribution)
* [Route Leaking](#route-leaking)
* [Verification](#verification)



# IS IS
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

## Verification
```
Switch-or-Router(config)# show isis database level-1 verbose
Switch-or-Router(config)# show isis database level-2 verbose
```