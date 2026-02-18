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
2. (optional) Enable LoRa &gt; Ok To MQTT to show on the [map/chat](https://meshview.nyme.sh/map)

### Personal/handheld/mobile node configuration

1. Role: <u>CLIENT_MUTE</u>
2. Position: <u>disabled</u>, or
    - <u>enable</u> smart position
        - smart interval <u>30 minutes</u> or more
        - update distance <u>100<u> or more
    - <u>disable</u> altitude
    - GPS polling interval: <u>30 minutes</u> or longer
3. Telemetry: <u>off</u>
4. Device info: <u>18 hour</u> interval or longer
5. LoRa hop limit: <u>5</u>

### Stationary/fixed node configuration

1. Role: <u>CLIENT_BASE</u><sup><a href="/faq#what-role-do-i-chose">*</a></sup>
2. Position: <u>disabled</u>, or
    - <u>disable</u> smart position
    - <u>enable</u> altitude
    - GPS updates and broadcasts: <u>24 hour</u> interval or longer
3. Telemetry: <u>off</u>, or at least <u>6 hour</u> interval if remote
4. Device info: <u>24 hour</u> interval
5. LoRa hop limit: <u>3</u>
6. (Optional) Enable <a href="https://meshtastic.org/docs/configuration/remote-admin/">remote admin</a>

### Radio settings

<div class="callout -primary" id="meshtastic-radio-settings">
  <p>Current primary mesh radio settings:</p>
  <dl>
    <dt>Preset</dt>
    <dd><u>Long Range - Fast</u></dd>
    <dt>Frequency slot</dt>
    <dd><u>20</u> or <u>0</u></dd>
    <dt>Public channel name</dt>
    <dd><u>LongFast</u> or blank</dd>
    <dt>Public channel key</dt>
    <dd><u>1 byte</u>, <u><code>AQ==</code></u></dd>
  </dl>
</div>

<div class="callout" id="mediumslow">
  <p><strong>Please ensure your node follows the <a href="#personalhandheldmobile-node-configuration">above configuration</a> before connecting to the network.</strong></p>
  <p><em>Experimental</em> settings to access the next-generation network:</p>
  <dl>
    <dt>Preset</dt>
    <dd><u>Medium Range - Slow</u></dd>
    <dt>Frequency slot</dt>
    <dd><u>48</u></dd>
    <dt>Public channel name</dt>
    <dd><u>MediumSlow</u> or blank</dd>
    <dt>Public channel key</dt>
    <dd><u>1 byte</u>, <u><code>AQ==</code></u></dd>
  </dl>
  <p>
    Personal nodes: increase LoRa hop limit to <u>7</u>. (Yes, really.)
  </p>
  <p class="small">
    Note that the <a href="/preset-testing">migration</a> to the “MediumSlow” network is a work-in-progress. Only some of the infrastructure has moved. You may find it very difficult to reach either network, or experience unreliable message delivery. Network status and help available in the <a href="https://discord.nyme.sh">Discord chat</a>.
  </p>
</div>

<details>
  <summary>Explanation of the settings</summary>
  <p>The above settings are necessary to keep the network in a high-performing state. The Meshtastic default settings are oriented toward small-scale meshes that require frequent background packets to be effective. However, on large meshes these defaults are unnecessary and quickly create congestion that reduces the utility of the network for everyone. Reducing this extraneous background traffic as much as possible is essential for preserving the usefulness of the mesh.</p>
</details>

<br>

## MeshCore

To connect to the wide-area MeshCore network in the NYC area:

1. Ensure your companion node or repeater is on the [latest firmware](https://flasher.meshcore.co.uk)

<div class="callout" id="meshcore-radio-settings">
  <p>MeshCore radio settings:</p>
  <dl>
    <dt>Preset</dt>
    <dd><u>US/Canada recommended</u></dd>
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

1. Set zero-hop auto advert interval to <u>180 minutes</u> or more
2. Set flood auto advert interval to <u>12 hours</u> or more
