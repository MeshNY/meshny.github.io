# Getting Started with Meshtastic and NYMe.sh

Getting started in NYMe.sh's Meshtastic network means both setting up Meshtastic and configuring your nodes to use the community's optimized radio settings for the NYC area and its infrastructure. To send your first message, you'll need to follow the steps below:

1. Obtain compatible hardware (E.g. a radio node paired with a phone or a standalone node).
2. Install Meshtastic software 
3. Configure your radio node for NYMe.sh's optimized network settings.
4. Say Hi!
5. Optimize your node for its intended use on the network (E.g. roles & other settings)

Once you've done the above, we also laid out some additional suggestions to get the most out of the mesh:

6. Review the community's network use best practices
7. See yourself on the network map
8. Consider contributing to the community's infrastructure (routers)

If at any point you have questions or doubts, join us on [Discord](https://discord.nyme.sh) in the [`#troubleshooting`](https://discord.com/channels/1395794339329998970/1395805706082324551) channel for help. 

## 1. Compatible Hardware

You will need at least one personal, handheld node that will be your first connection to the mesh. 

If you don’t already have a device, see our list of [recommended complete nodes](/faq#hardware).

## 2. Install and update the Meshtastic firmware and app

To make full use of the NYMe.sh network, you'll need to make sure your node is on the [latest Beta or Alpha firmware](https://flasher.meshtastic.org)<span class="js-mt-firmware"></span>

## 3. Optimize your Meshtastic radio for NYMe.sh

By default, the Meshtastic software uses the "Long Range - Fast" LoRa radio preset. After [a long period of testing](https://nyme.sh/preset-testing/), the NYMe.sh community decided to migrate to a different radio configuration from the Meshtastic "LongFast" default considering NYC's specificities of an urban environment, high density and particular spectrum usage.

NYMe.sh utilizes the "Medium Range - Slow" preset, with a custom frequency slot (48), or "MS48" for short.

### Configuring radios for NYMe.sh's MS48 network

(**Note**: Throughout this guide, settings not explicitly called out can be left at default values)

1. In your Meshtastic App: Go to `Settings` -> `LoRa`
2. Apply the following settings:
    - `Use Preset` -> `ENABLED`
    - `Presets` -> `Medium Range - Slow`
    - `Ignore MQTT` -> `DISABLED`
    - (optional) `OK to MQTT` -> `ENABLED` (utilize only if you wish to show up on the [Meshview](https://meshview.nyme.sh/map) or [Malla](https://malla.nyme.sh/map) network maps)
    - `Transmit Enabled` ->  `ENABLED`
    - `Number of Hops` -> `7` (Yes, *really*)
    - `Frequency Slot` -> `48`
  
### Set up NYMe.sh's Public Channel

1. In your Meshtastic App: Go to `Settings` -> `Channels`
3. Apply the following settings to your Primary Channel
   - `Channel Name` -> `MediumSlow` or leave blank
   - `Key Size` -> `1 byte`
   - `Key` -> `AQ==`
   - (optional) `Positions Enabled` -> Enable if you'd like to transmit your position to other mesh nodes, and select desired accuracy. [Read here for more from Meshtastic.org on sharing your position through channels](https://meshtastic.org/docs/configuration/tips/#not-sharing-your-location).

## 4. Say Hi on the Public Channel.

You should now be ready to say "Hi" in the public channel, and see the nodes and map tabs in the app populate with other nodes.

## 5. Optimize your node for your use-case

Before we're done, we need to optimize a few settings that differ according how you'll use your node day-to-day. These settings allow us to make the most efficient use of the mesh's airtime and relays, and consider the fixed infrastructure the community has installed in the region. 

We'll cover some typical use-cases for nodes, their different settings and why the settings differ.

### Node use-cases
1. **Handheld node**: a node that you carry with you, in your pocket, bag, belt, mounted on your car, and so on. Typically we want these nodes to receive and transmit, but *not* relay messages.
2. **Stationary node**: a base station node that lives on your desk or your roof. Critically, these are nodes _that you also send messages from_, but generally have a fixed position and that you may some times connect directly to from your other nodes, rather than use solely as a relay.
3. **Infrastructure node**: a node in a fixed location, intended *solely* for relay purposes and that you *do not* send messages from. They typically are solar builds in remote or elevated locations.

If you're in doubt about which role your use-case your node falls into, or want to learn more about why these divisions were chosen, check out the FAQ's ["What role do I choose?"](https://nyme.sh/faq/#what-role-do-i-chose) section. You may need to adapt particular settings to your use-case, but always keep in mind the good use of the mesh's resources.

### Handheld node configuration

Handheld nodes are configured to send and receive messages and position data, but do not relay messages or transmit device telemetry.

In your Meshtastic App:
1. Configure the device's role.
   - Go to `Settings` -> `Device`
   - Apply the following settings `Device` Page
       - `Device Role` -> `Client Mute`
       - `Rebroadcast Mode` -> `All`
       - `Node Info Broadcast Interval` -> `Eighteen Hours`
2. Configure the device's position transmission settings.
   - Go to `Settings` -> `Position`
   - Choose between **disabling** position transmission or using **smart** position transmission
       - To **disable** transmission, apply the following settings:
            - `Broadcast Interval` -> `Never`
            - `Smart Position` -> `DISABLED`
       - To **enable** Smart Position transmission
            - `Broadcast Interval` -> `Thirty Minutes` or longer
            - `Smart Position` -> `ENABLED`
            - `Minimum Interval` -> `Thirty Minutes` or longer
            - `Minimum Distance` -> `100` or higher
            - `Device GPS` -> `ENABLE`
            - `Update Interval` -> `Thirty Minutes` or longer
            - `Altitude` -> `DISABLE`
3. Configure the device's telemetry settings.
    - Go to `Settings` -> `Telemetry`
    - Apply the following settings `Telemetry` Page
        - `Broadcast Device Metrics` -> `DISABLED`
        - `Environment Metrics Enabled` -> `DISABLED`
        - `Power Sensor Options` -> `DISABLED`
 
<details class="small">
  <summary>Explanation of the settings</summary>
  <p><code>CLIENT_MUTE</code> is the preferred starting point for mobile nodes because it avoids unexpected relay behavior in an infrastructure-based mesh. Personal or mobile nodes often experience worse SNRs than fixed nodes, which causes them to relay first and potentially stop a better-placed node from relaying. It’s also important if you have two nodes in close proximity, avoiding the <a href="https://nyme.sh/faq/#what-role-do-i-chose">“false ack”</a> problem that can hide connection issues.</p>
  <p>Smart position is preferred because it reduces the broadcasts if position hasn’t changed. However, it has trouble with altitude so it’s best to disable this—altitude is usually not helpful for mobile nodes. Generally, position doesn’t need to be sent more frequently than 30 minutes.</p>
  <p>Telemetry is disabled because we don’t need to know your battery level or channel utilization on a regular basis. Neither are meaningful to the rest of the mesh.</p>
  <p>Reducing automatic device info broadcasts avoids the throttling that inhibits the request user info features, and it makes room for more useful packets generally. Also, nodes have the ability to send node info on-demand if the operator needs to advertise their info.</p>
  <p>Personal nodes usually need more <span class="js-konami" data-alt="bunnies">hops</span> to work through the infill to get to and from the network backbone. The next-gen MediumSlow network relies on this being the maximum of <em>7</em> because the network adopts <a href="/nymesh-2/">packet-level resiliency</a> instead of link-level, and needs the additional <span class="js-konami" data-alt="bunnies">hops</span> to allow for retries and path diversity.</p>
</details>
<br>

### Stationary node configuration

Stationary nodes are configured to send and receive messages and position data, but do not relay messages or need to transmit device telemetry. These are your base station nodes that live on your desk or your roof

In your Meshtastic App:
1. Configure the device's role.
   - Go to `Settings` -> `Device`
   - Apply the following settings `Device` Page
       - `Device Role` -> `Client`
       - `Rebroadcast Mode` -> `All`
       - `Node Info Broadcast Interval` -> `Eighteen Hours`
2. Configure the device's position transmission settings.
   - Go to `Settings` -> `Position`
   - Apply the following settings `Position` Page
            - `Broadcast Interval` -> `Twenty Four Hours` or longer
            - `Smart Position` -> `DISABLED`
            - `Device GPS` -> `DISABLED`
            - `Fixed Position` -> `ENABLED`
            - `Altitude` -> `ENABLED`
3. Configure the device's telemetry settings.
    - Go to `Settings` -> `Telemetry`
    - Apply the following settings `Telemetry` Page
        - `Broadcast Device Metrics` -> `DISABLED`
        - `Environment Metrics Enabled` -> `DISABLED`
        - `Power Sensor Options` -> `DISABLED`

<details class="small">
  <summary>Explanation of the settings</summary>
  <p><code>CLIENT</code> is the preferred starting point for fixed personal nodes because they are likely to provide useful conditional relay.</p>
  <p>Position is optional, but helpful to understand the physical realities of the mesh. Smart position is not recommended, since the node is not moving. It can have trouble with variations from a GPS fix so it’s best to set an explicit fixed position. Altitude is helpful for understanding coverage.</p>
  <p>Telemetry is preferred disabled because others generally don’t need to know your battery level or channel utilization on a regular basis. Neither are meaningful to the rest of the mesh. The node will still relay its battery info regularly when you connect your app to it.</p>
  <p>Reducing automatic device info broadcasts avoids the throttling that inhibits the request user info features, and it makes room for more useful packets generally. Also, nodes have the ability to send node info on-demand if the operator needs to advertise their info.</p>
  <p>Personal nodes usually need more <span class="js-konami" data-alt="bunnies">hops</span> to work through the infill to get to and from the network backbone. The next-gen MediumSlow network relies on this being the maximum of <em>7</em> because the network adopts <a href="/nymesh-2/">packet-level resiliency</a> instead of link-level, and needs the additional <span class="js-konami" data-alt="bunnies">hops</span> to allow for retries and path diversity.</p>
</details>
<br>


### Infrastructure node configuration

Nodes that are in a fixed location and intended solely for relay purposes. These nodes are _not_ used to send messages directly. They typically are solar builds in remote locations. Here, telemetry and even changing the hop limit are important.

In your Meshtastic App:
1. Configure the device's role.
   - Go to `Settings` -> `Device`
   - Apply the following settings `Device` Page
       - `Device Role` -> `Client Base`
       - `Rebroadcast Mode` -> `All`
       - `Node Info Broadcast Interval` -> `Forty Eight Hours`
2. Configure the device's position transmission settings.
   - Go to `Settings` -> `Position`
   - Apply the following settings `Position` Page
            - `Broadcast Interval` -> `Twenty Four Hours`
            - `Smart Position` -> `DISABLED`
            - `Device GPS` -> `DISABLED`
            - `Fixed Position` -> `ENABLED`
            - `Altitude` -> `ENABLED`
3. Configure the device's telemetry settings.
    - Go to `Settings` -> `Telemetry`
    - Apply the following settings `Telemetry` Page
        - `Broadcast Device Metrics` -> `ENABLED`
            - `Device Metrics` -> `Six Hours` or longer
        - `Environment Metrics Enabled` -> `DISABLED`
        - `Power Sensor Options` -> `ENABLED`
            - `Power Metrics` -> `Six Hours` or longer
4. Configure the device's radio settings.
    - Go to `Settings` -> `LoRa`
    - `Number of Hops` -> `2`

<details class="small">
  <summary>Explanation of the settings</summary>
  <p><code>CLIENT_BASE</code> helps differentiate the infrastructure nodes from personal nodes. It also enables handy infrastructure behaviors through favoriting adjacent routers and personal nodes, features that work best when the node is in a static position. <code>CLIENT_BASE</code> is also the recommended starting point even if the node is well sited.</p>
  <p>Altitude is useful for line-of-sight estimates. But smart position has trouble with altitude if it changes due to GPS variation and can spam position unnecessarily. 24 hours is sufficient to stay on the map.</p>
  <p>Position is highly recommended for infrastructure nodes so users can understand which nodes provide coverage for them. (It doesn’t have to be exact, but should be a useful approximation.) Fixed position is recommended even if there is GPS present. The GPS is still useful for keeping the node's clock accurate, but it can cause unexpected position variations due to errant GPS signal reception. 24 hours is sufficient to maintain the clock without a meaningful drain on the battery of solar nodes.</p>
  <p>Telemetry broadcasts are useful to monitor the health of the node, but more frequent than 6 hours is excessive and takes up useful airtime.</p>
  <p>Device info is significantly curtailed because it’s not necessary for the nodes to route packets, and takes up airtime.</p>
  <p><span class="js-konami" data-alt="Bunny">Hop</span> limit: fixed nodes should focus on advertising to their immediate vicinity. They also should be within direct or single-<span class="js-konami" data-alt="bunny">hop</span> range of infrastructure, and don’t need as many <span class="js-konami" data-alt="bunnies">hops</span> to reach through the infill — they <em>are</em> the infill.</p>
</details>
<br />

## 6. Network use best practices

Some guidelines on specific use cases or technologies that may affect the network differently:

**Reticulum and TAK**: Please do not use high-traffic applications like Reticulum or TAK on this network; they saturate the mesh and make it unusable for everyone. Sustained encrypted traffic will be detected and blocked by the infrastructure to protect the limited airtime.

## 7. Network Map

If you've enabled `OK to MQTT` in the LoRa page of your settings, you'll be able to see your node on NYMe.sh's [Meshview](https://meshview.nyme.sh/map) or [Malla](https://malla.nyme.sh/map) network maps

## 8. Consider contributing to the community's infrastructure

You may have noticed in setting up your nodes that we did not use the `ROUTER` or `ROUTER LATE` roles even for stationary, relay-only nodes. This is because the community actively manages several Router nodes and proactively manages routers around the network based on location and traffic, as discussed in the [FAQ](https://nyme.sh/faq/) page. Join us in the [#infrastructure](https://discord.com/channels/1395794339329998970/1426696399235321906) channel on Discord to see if your stationary node could help as a router or if you're willing to help deploy additional router nodes. 

<br>

## MeshCore

To connect to the wide-area MeshCore network in the NYC area:

1. Ensure your companion is on the [latest firmware](https://flasher.meshcore.io)

<div class="callout" id="meshcore-radio-settings">
  <p>MeshCore radio settings:</p>
  <dl>
    <dt>Preset</dt>
    <dd><u>US/Canada</u></dd>
    <dt>Frequency</dt>
    <dd><u>910.525 MHz</u></dd>
    <dt>Bandwidth</dt>
    <dd><u>62.5 kHz</u></dd>
    <dt>Spread Factor</dt>
    <dd><u>7</u></dd>
    <dt>Coding Rate</dt>
    <dd><u>5</u></dd>
  </dl>
  <p class="small">
    Increase coding rate if you find your messages are not getting received. This setting is cross-compatible.
  </p>
</div>


For repeaters:

1. Ensure your repeater is on the [latest firmware](https://flasher.meshcore.io)
2. Set zero-hop auto advert interval to <u>360 minutes</u> or more
3. Set flood auto advert interval to <u>24 hours</u> or more
