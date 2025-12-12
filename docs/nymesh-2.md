# nyme.sh 2.0

There’s a crystalizing pattern for functional metro-scale meshes: __favor infrastructure with predictable relay behavior across reliable links, and minimize airtime__.

MeshCore lends itself to this approach through its protocol and defaults. The basic recipe for implementing this with Meshtastic is to make it a lot like MeshCore through configuration. This does mean fighting some of Meshtastic’s tendencies since it is ad hoc-first, but Baymesh and PDX are proving it’s entirely possible to make an infrastructure-driven mesh using Meshtastic, enabled by recent firmware changes they’ve prompted. (A huge thank you to the folks from Baymesh and PDX meshes, and others, for their insights!)


## Background

- Meshtastic: “[Is LongFast Holding Your Mesh Back? Better LoRa Presets for Bigger Meshtastic Networks](https://meshtastic.org/blog/why-your-mesh-should-switch-from-longfast/)”
- Meshtastic: “[Why Meshtastic Uses Managed Flood Routing](https://meshtastic.org/blog/why-meshtastic-uses-managed-flood-routing/)”
- Austin Mesh: “[Meshtastic vs. MeshCore on Austin Mesh](https://www.austinmesh.org/learn/meshcore-vs-meshtastic/)”
- “[Some lessons learned from Bayme.sh for establishing a mesh](https://www.reddit.com/r/meshtastic/comments/1mb9cku/some_lessons_learned_from_baymesh_for/)”
- [Managed flooding simulator](https://k2xap.radio/meshtastic/managed-flooding)
- “[Emergence](https://architectingsystems.com/emergence)” - not mesh-specific but a useful concept to know

### Assumptions

- _The current mesh is not functioning optimally._ It has good days and bad days, sometimes allowing widespread communication across the metro, and other times having lots of missed messages and failing traceroutes.

- _It is desired to have widespread, independent, RF-only communication across the metro._ A text message-centric, collectively operated radio mesh is something people want to make and use.

- _Replacing Meshtastic with MeshCore is not feasible or necessary at this time._ While adopting MeshCore would make certain parts of this easier, getting a critical mass to switch is much more difficult. Also, the current mesh is actually working surprisingly well for default settings. And some do not find MeshCore appealing for various reasons.


### Mesh layers

These aren’t strict definitions, just a broad categorization that is useful when talking about nodes in generalized terms. Each actual node plays its own role in the emergent network.

1. **Backbone**: core infrastructure nodes in good locations that reliably link to each other and are central to the mesh graph. These can usually be heard by many more nodes than they can hear reliably.
2. **Infill**: secondary infrastructure nodes that help lift packets up above the building clutter or push them down into areas not covered by the backbone. These also help with reliability by providing temporal or spatial redundancy of packets.
3. **Personal**: aka street-level; the lowercase-c client nodes people use directly. They can often hear the backbone but may need help reaching it via the infill layer. These usually _should not_ relay packets.



## Baymesh recommendations

This is a summary of learnings from primarily Baymesh, probably the largest Meshtastic mesh in operation. They have switched presets twice, and actually have multiple Meshtastic and MeshCore networks in the San Francisco Bay area. (Where unlinked, the quotes are from private Discord messages.) Other mesh groups have conveyed similar thinking.

1. **Organize, communicate, experiment:** use a reliable channel to coordinate efforts (eg Discord). Use tools to gather data and document results (Meshview/Malla). Don’t be timid, feel free to experiment—so long as it’s not hard to revert settings there is little harm in trying things out. Each mesh and even cluster of the mesh has its own considerations that needs practical experience to work best. The official guidelines are very abstract generalizations.

2. **Move off the default frequencies** (regardless of LoRa parameters). This allows the mesh to avoid outdated and unmaintained nodes, and choose a frequency that is more clear in their particular area. It’s a tiny bit of friction that forces node operators to be minimally engaged enough to cooperate with the mesh and keep their nodes up-to-date. It also keeps the defaults free for people who just want to do their own ad hoc thing without worrying about a beast of a mesh drowning them out.

3. **Don’t be afraid of routers.** Nodes that can see a lot of nodes that can’t see each other should be ROUTER or ROUTER_LATE. Well-placed infrastructure is the only way to reliably deliver packets. (These are not necessarily mountain-top or tower-only, they can be anything that provides useful connections. The key is to monitor and pay attention, experiment.) SNR-based conditional relay could make sense in an ad hoc mesh between portable nodes, but is terrible for reliability in infrastructure meshes since it inherently favors poorly situated nodes.

    > Any node with height, and a view … that can obviously reach things many miles away…shows up in paths with many directs… router
    >
    > the best ~10-15% of your nodes… and they’re spread out as is practical …(SNR based timers are really bad  and route things right into black holes… we gave up on client role almost entirely)
    >
    > The meshes that failed and then went to MeshCore… were the ones that were scolded to make every single node a Client and never use router ever.

4. **Don’t be afraid of hops.** The admonition about hop increases being exponential is driven from simulations of evenly-spaced “ideal” meshes. Real-world meshes tend to be clusters, which makes for propagation that is [less-than-linear](https://discord.com/channels/867578229534359593/1161490210165628998/1433086232421990531) to hop count when accounted for in simulations. The recently introduced [0-hops for favorites](https://github.com/meshtastic/firmware/pull/7992) feature was devised by Baymesh specifically to get around the low hop limit. It lets them establish a reliable, frictionless backbone for packets that goes from [San Luis Obispo to Tahoe](https://meshview.bayme.sh/packet/4140053132). Packets can save their hops for the infill layer getting to and from the backbone.

    To the extent that high hop counts are a problem and create swirling tangles of propagation, it’s because there is no router to cancel all the clients that shouldn’t be passing the message, and because of a slow preset that forces nodes to wait a while for clear airtime. (MeshCore gets away with 64 hops just fine.)

5. **Minimize airtime.** This is essential for reducing the chance of collision, the biggest problem for dense meshes since even a router can't overcome it. [Everybody who has heard we’re still on LongFast has been surprised. Most metros switch well below our scale.]
    - Reduce extraneous transmissions such as telemetry, position, nodeinfo.
    - Use the fastest LoRa settings you can.
        - This is aided significantly by bandpass filters, which can give back the link budget lost by a faster preset.
        - Use careful tweaks to Coding Rate in infrastructure to ease transition, softening the link budget blow until more nodes make the switch.
        > - 1s packet on LF is…
        > - 400ms on MS
        > - 230ms on MF
        > - 100ms on SS
        > - 50ms on SF
        > - 25ms on ST




## Interpretation

3, 4, and 5 are complementary and co-dependent. Moving to faster radio settings with less airtime both _requires and enables_ switching the signal resiliency from link-level to packet-level, the unit of the mesh. Instead of relying a single transmission to tolerate noise through long airtime, recognize that _congestion is also noise_ and increase tolerance by retrying whole packets.

Also note that the link budget is an on-paper calculation for a single transmission. Practical, experienced SNR is impacted by collisions from meshing and other real-world sporadic interference that has a temporal component.
> ST is 12db worse than LF but we did not see that degradation.  We saw about half (8db) and 90% links still worked

Less airtime _improves_ SNR of each transmission by accumulating less background noise and reducing the chance of collision. But, it does decrease the chance that an individual transmission will be heard. Infrastructure compensates for this by using the extra available airtime to improve reliability through packet redundancy—not just through time but through space: each recipient gets a retry of the packet at _different times_ and from _different angles_. A useful spread of `ROUTER` and `ROUTER_LATE` ensures a receiving node gets multiple chances to hear a packet. (MeshCore has an explicit `tx_delay` property for infrastructure to effect the same result.)

Faster airtime means routers typically become additive to mesh performance rather than subtractive. Also, routers _should_ be robust with battery backup and solar etc, but it’s potentially okay if they aren’t: a well formed mesh should be able to tolerate nodes dropping offline and still route packets to their destination by providing multiple redundant paths.


### Aside: dark ~~fiber~~ nodes

An additional improvement that Baymesh hasn’t explicitly recommended but I've seen them and others (like SVMesh) do is co-locate nodes. Where possible, they place multiple nodes at a site, allowing them to either run multiple meshes at once, ease transitions, and/or have backups that can be activated in case of a failure.

For example, [this node](https://meshview.bayme.sh/node/862158404) at a key site was primarily a backup sitting in `CLIENT_MUTE`, but is currently running as a `MediumSlow` router to ease their transition to `MediumFast`.

A good site is a scarce resource much more than node hardware is. Much like how telecom companies lay excess fiber in anticipation of future needs, since the trenching is the expensive part, we should consider placing extra hardware where feasible. This does raise cost and needs careful management of potential interference, but those are solvable problems and having multiple devices greatly simplifies changes and experimentation.


### Aside 2: MQTT backhaul

Something else to consider, not mentioned specifically but observed, is using MQTT for key links that are currently difficult over RF. Even if the desire is RF-only to encourage a fully independent network, judicious use of MQTT can help the network grow and fill certain gaps, to be replaced by RF later. Also, there are techniques to make specific links robust and maintain the resilience aspect of the network in the case of major power or internet outages.


## Considerations about being off-default

- Requires actively directing newcomers to the local settings, with beacons and instructions
  - We already are pretty good about doing this anyway, directing people to the discord
- Cuts off connections beyond the mesh proper and requires bridging to adjacent meshes
  - This is desirable as it avoids a large mesh being too noisy a neighbor but more deliberate linking could be possible
  - This is undesirable because it cuts off outlying folks who rely on uncooperative intermediates, and bridging may not be possible
- Complicates travel since you have to change your settings
  - Less of a concern now that other locations are also switching to their own settings



## Action items

### Spectrum sweeps

Use `rtl_power` with an SDR to check the 33cm band from different areas in the city to get a picture of where the clearest areas of the band are. We have dabbled with this previously—the middle of the 33cm band seems relatively clear compared to the lower portion used by LF20—but it needs a more productive effort.

### Test network

A few realistically situated nodes. Ideally a mix of construction, with and without filters, with a Raspberry Pi or similar attached to run automated pings and collect data. Consider systematically stepping through different LoRa settings and frequencies for comparison. (Frequency tests are tricky given filters.)

### Settle on a frequency

This is a bit of a circular dependency, since a proper test network needs filters but [investing in filters](https://discord.com/channels/1395794339329998970/1441831475602522162) requires choosing a frequency which requires testing presets. SDR sweeps should help.

### Plan actual cutover

TBD
