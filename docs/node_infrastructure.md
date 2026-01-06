{% include nav.html %}

# nyme.sh Infrastructure Node Guidelines

Having infrastructure nodes that are able to reliably communicate with one another is what makes the mesh work best. Following these guidelines will help ensure that we can help the reliability of the greater mesh and provide redundancy for data to travel. Participation is 100% voluntary and we please ask you follow these guidelines if you want to deploy an infrastructure node using roles of `ROUTER` or `ROUTER_LATE`. If you can meet the guidelines below, post in the [Discord infrastructure channel](https://discord.nyme.sh) and see if there is a need for a infrastructure role in your area. 

## Hardware Guidelines

- **Location, location, location!** Rooftop of the tallest building/structure in your area with clear line of sight to other infrastucture node locations. This would also include permission to place the node to begin with.
- **Environment** This node will live outside and will need to be protected from the elements.  A proper sealed and vented enclosure to maintain normal node operation.
- **Power** Infrastructure nodes will need to be supplied with reliable power 24/7.  Nodes of this nature commonly use solar panels and a large (for the node) sized battery.  Check the [Build Resources](/build_resources.html) for more information
- A **Single Board Computer** including Raspberry Pi or other internet based remote admininstration for configuration and firmware updates if access is difficult.

## Software Guidelines

- **Firmware Version:** non-alpha firmware
- **Node Info Broadcast Interval:** 12 hours
- **Position Packet:** 24 hours
- **MQTT:** configure to nyme.sh MQTT server
- **Admin Key:** You will need to be able to remote admin your infrastructure node
- **Secondary Admin Key:** You will need to have secondary remote admin for your node in case you are unable
