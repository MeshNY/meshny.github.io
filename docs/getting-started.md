---
title: Getting Started
---

# Getting Started


## Hardware

You will need at least a personal, handheld node that will be your direct connection to the mesh. Additionally, most people need a “roof” node to create a reliable first hop to the area infrastructure.

If you don’t already have a device, see our list of [recommended complete nodes](/faq#hardware).

<br>

## Meshtastic

To connect to the wide-area Meshtastic network in the NYC area…

1. Ensure your node is on the [latest Beta or Alpha firmware](https://flasher.meshtastic.org)


### Personal/handheld/mobile nodes

1. Role: <u>CLIENT_MUTE</u>
2. Position: <u>disabled</u>, or
    - <u>enable</u> smart position
    - <u>disable</u> altitude
    - GPS updates and broadcasts: <u>30 minutes</u> or longer
3. Telemetry: <u>off</u>
4. Device info: <u>12 hour</u> interval or longer
5. LoRa hop limit: <u>5</u>

### Stationary/fixed nodes

1. Role: <u>CLIENT_BASE</u><sup><a href="#meshtastic-footnote-role">*</a></sup>
2. Position: <u>disabled</u>, or
    - <u>disable</u> smart position
    - GPS updates and broadcasts: <u>24 hour</u> interval or longer
3. Telemetry: <u>off</u>, or at least <u>6 hour</u> interval if remote
4. Device info: <u>24 hour</u> interval
5. LoRa hop limit: <u>3</u>

### Meshtastic radio settings

- Preset: <u>Long Range - Fast</u>
- Frequency slot: <u>20</u> or <u>0</u>
- Public channel name: <u>LongFast</u> or blank
- Public channel key: <u>1 byte</u>, <u><code>AQ==</code></u>
- Ok To MQTT: <u>enabled</u> (optional, to appear on the [map](https://meshview.nyme.sh/map))

<details>
  <summary>Explanation of the settings</summary>
  <p>The above settings are necessary to keep the network in a high-performing state. The Meshtastic default settings are oriented toward small-scale meshes that require frequent background packets to be effective. However, on large meshes these defaults are unnecessary and quickly create congestion that reduces the utility of the network for everyone. Reducing this extraneous background traffic as much as possible is essential for preserving the usefulness of the mesh.</p>
</details>

<p class="small" id="meshtastic-footnote-role">
  <sup>*</sup> If you have access to a truly prominent location, such as a radio tower or rooftop that is 400 ft above the ground and has a clear view around, stop by the <a href="https://discord.com/channels/1395794339329998970/1426696399235321906">#infrastructure</a> channel in <a href="https://discord.nyme.sh">Discord</a> and we can help figure out the appropriate build and role.
</p>

<br>

## MeshCore

To connect to the wide-area MeshCore network in the NYC area:

1. Ensure your companion node is on the [latest firmware](https://flasher.meshtastic.org)
2. Radio settings, <u>US/Canada recommended</u>:

    <a id="meshcore-radio-settings" />

    |-----------------------|---------------------|
    | LoRa settings         |                     |
    |-----------------------|---------------------|
    | Bandwidth             | `62.5 kHz`          |
    | Spread Factor         | `7`                 |
    | Coding Rate           | `5`                 |
    |-----------------------|---------------------|

For repeaters:

1. Set zero-hop auto advert interval to <u>180 minutes</u> or more
1. Set flood auto advert interval to <u>12 hours</u> or more
