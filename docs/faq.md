---
title: FAQ
---

# Frequently Asked Questions

Also see the [Glossary](/glossary.html) for common terminology.


## Hardware

Complete nodes that work well in our experience:

Personal handheld nodes:

  - [Muzi R1 Neo](https://muzi.works/products/r1-neo-complete-meshtastic-device)
  - [Muzi H2T](https://muzi.works/products/h2t-complete-device-heltec-t114-with-gps-running-meshtastic)
  - [Seeed Wio Tracker L1](https://www.seeedstudio.com/Wio-Tracker-L1-Pro-p-6454.html)
  - [Seeed SenseCAP T1000E](https://muzi.works/products/seeed-t1000e)
  - [RAK WisMesh Tag](https://store.rokland.com/products/wismesh-tag-from-rakwireless-mokosmart-meshtastic-compatible-card-sized-node-us915-mhz)

Fixed solar nodes:

  - [Seeed SenseCAP Solar](https://www.seeedstudio.com/SenseCAP-Solar-Node-P1-Pro-for-Meshtastic-LoRa-p-6412.html)


### What antenna?

Most nodes are very low power, typically transmitting at only 150 mW. This can go quite far, but an efficient antenna is essential for getting heard. Unfortunately, nodes often come with crummy little stubs that are not even properly tuned for the desired band.

Antennas this group has experience with and recommends:

- Personal nodes:
  - [Muzi Whip](https://muzi.works/products/whip-antenna-17cm) / aka Gizont Whip on Amazon: SMA, excellent SWR, a favorite ([technical review](https://discord.com/channels/1395794339329998970/1395794340823040197/1462276878890172521))
  - [ZBM2 Mesh Whip V2](https://zbm2industries.com/products/v2-mesh-whip): large but durable, needs BNC adapter
- Fixed nodes:
  - [Alfa 5 dBi](https://muzi.works/products/alfa-outdoor-antenna): compact, great VSWR, good for lower nodes ([technical review](https://discord.com/channels/1395794339329998970/1395794340823040197/1455987107917988084))
  - [Rokland 5.8 dBi large profile](https://store.rokland.com/collections/802-11ah-wi-fi-halow/products/5-8-dbi-n-male-omni-outdoor-915-mhz-antenna-large-profile-32-height-for-helium-rak-miner-2-nebra-indoor-bobcat): _big_ but well performing ([technical review](https://discord.com/channels/1395794339329998970/1395794340823040197/1461036965595054230))

These antennas all have good reflection loss characteristics (low VSWR) and will transmit your signal efficiently.

**Caution:** do NOT power on your node without an antenna attached. This can permanently damage the radio. If you want to hot-swap an antenna, turn off the radio under `Settings > Lora > TX Enabled`. (Don’t forget to turn it back on!)

**Caution:** many nodes and antennas use SMA, and many use RP-SMA. These can be physically coupled but will not make electrical contact, damaging the radio if you try to transmit. Check the connectors and make sure there are a pin and a socket in the right places. You can get adapters to flip the polarity if needed.

**A note about gain:** antenna gain above 5 dBi is likely going to perform _worse_ than a lower gain antenna in an urban environment. Antennas boost their gain by concentrating their beam in particular directions. A 10 dBi omni antenna has a narrow beamwidth about 20°, a flat donut radiating toward the horizon. Mounted high up, this is perfect for sending a signal far distances to another high antenna, but it will overshoot much of the more immediate terrain. This is a problem in densely built areas where multipath propagation is dominant and antenna altitudes vary significantly. A high gain antenna will likely be unable to hear many signals because it’s only listening to a narrow slice of space. Also, consumer-grade antennas often are marketed with gains much, much higher than reality. The Alfa 5 dBi is actually closer to 2 or 3 dBi in [testing](https://antennatestlab.com/helium-network-antenna-reviews/alpha-network-ada-915-5acm-helium-antenna-5dbi) and favors a high angle, but this means it ends up being very well suited for urban contexts.


## Meshtastic

### What role do I chose?

There is a lot of nuance to Meshtastic role selection that depends on the node hardware, its location, its intended usecase, and its relation to the mesh you intend to connect it to.

These are the recommended starting points for connecting to a city-wide mesh:

- Portable/mobile nodes, like handheld or on a car: `CLIENT_MUTE`
- Base nodes, at home (even rooftop): `CLIENT`
- Rooftop nodes, even a fairly tall apartment: `CLIENT`

If you have multiple nodes at home, only set at most one to `CLIENT`; multiple `CLIENT` nodes in close proximity can cause undesired behavior without care, not just for the broader mesh but even for yourself.

Once the node is up-and-running and you are reliably connecting to other nodes and operators, you will be able to evaluate its contribution to the mesh and consider infrastructure roles like `ROUTER` and `ROUTER_LATE`. These roles have particular characteristics relative to `CLIENT`, and require a careful understanding of how the node relates to its mesh neighbors to be beneficial. And importantly, it requires an ability to readily maintain the node as the mesh evolves.

The general guideline is an infrastructure node needs to have a great view of the surrounding area, able to hear and be heard by a lot of other nodes that _cannot hear each other_, and regularly participate in paths between nodes. An effective infrastructure node also has much more substantial hardware requirements. It’s entirely possible your balcony or the rooftop of your building is a very good site for an infrastructure node, but it is essential to coordinate this role with the rest of the mesh. Stop by the [#infrastructure](https://discord.com/channels/1395794339329998970/1426696399235321906) channel in Discord with any and all questions about node roles.


### How do I show up on the [map](https://meshview.nyme.sh/map)?

Enable Lora settings > OkToMQTT, and check that you are sharing positions in Channels > Primary.

See the [MQTT instructions](/mqtt.html).


### Why do messages show negative hops?

This happens when a packet is relayed by a node with old firmware that lacks support for the `hop_start` attribute in the packets. This causes the next receipt of it to zero out the attribute. When clients go to calculate the number of hops a message took, it becomes `0 - hop_limit`, making it show 0 or negative hops. Some clients may also show this as direct, but the SNR you see will be the last hop before you not from the sender.


### Why do traceroutes show `!ffffffff` or `^all`?

When a traceroute passes through a node with outdated firmware, or without a common channel key, or Skip Decoding enabled, it will not add itself to the traceroute list. When the next node picks up the traceroute and detects that the preceding node is not in the list, it inserts `!ffffffff` as a placeholder. This may also happen if the `relay_node` information is malformed when the next node receives it so it mistakenly inserts the placeholder.


### Why am I not getting Acks?

Clients show “Acknowledged” or checkmarks for messages in channels that come from the sending node hearing its message being retransmitted by another node, the _implicit ack_. If you get “Max retransmission reached”, it means your node did not hear any of these repeats within a certain time. This does not necessarily mean another node didn’t hear it, only that you didn’t hear the next retransmission. Remember that `CLIENT_MUTE` does not retransmit packets. Also, RF conditions can be dynamic or asymmetrical. This is especially true with certain hardware that is much better at RX than TX. In a congested mesh, a well-placed `CLIENT` or `ROUTER_LATE` node may have to wait _minutes_ before it gets clear airtime to relay a packet.

Conversely, just because you hear an ack doesn't mean the message made it to the wider mesh. The next relay of it may not have been received by anyone. This is especially common if there are multiple clients in close proximity. See “What role do I chose?” above.

#### Acknowledged by another node

This status in direct messages means your node heard the _implicit ack_ of another node repeating its message. The client will display this until your node receives the explicit ACK packet from the intended recipient. Like the implicit acks, _not_ receiving the ACK is not confirmation the recipient failed to receive the message. It only means _you_ have not received confirmation they did. That said, it does very likely mean they did not receive it.


### Why is my node sending so many NODEINFO and POSITION packets?

It may be in a reboot loop. Check that it has a reliable power supply, and try reflashing the firmware. Higher output nodes like the Heltec V4 especially can be demanding of their power inputs.

Nodes also perform `NODEINFO` handshakes when they encounter a new node. This can result in a large number of such packets being exchanged when a new node connects to a large mesh. Or when node lists cycle.



## Other


### What are these things on light poles?

[Flood sensors](https://www.floodnet.nyc/methodology)! They also use LoRa, but as LoRaWAN instead of P2P mesh.


### Why does Flatbush not connect to the rest easily?

Glaciers. Seriously. Long Island was formed out of a glacial moraine left behind by several glacial retreats over various glaciations. The high point runs from Prospect Park, through the various neighborhoods with “hills” and “heights” in their names, and down the middle of Long Island.

It doesn’t seem like much, but it’s a substantial elevation change that makes connectivity between the north and south sides of Long Island difficult.

