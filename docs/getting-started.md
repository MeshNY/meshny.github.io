---
title: Getting Started
---

# Getting Started


## Hardware

You will need at least a personal, handheld node that will be your direct connection to the mesh. Additionally, most people need a “roof” node to create a reliable first hop to the area infrastructure.

If you don’t already have a device, see our list of [recommended complete nodes](/faq#hardware).

<br>

## Meshtastic

To connect to the wide-area Meshtastic networks in the NYC area…

1. Ensure your node is on the [latest Beta or Alpha firmware](https://flasher.meshtastic.org)<span class="js-mt-firmware"></span>
2. (optional) Enable LoRa &gt; Ok To MQTT to show on the [map/chat](https://meshview.nyme.sh/map)
3. Configure your node as described below, based on how you use it:

### Personal node configuration

These are nodes that you send messages from. Either fixed or mobile.

#### Handheld node config

These are nodes that you carry with you, in your pocket, bag, belt, mounted on your car, and so on.

1. Role: <u>CLIENT_MUTE</u>
2. Position: <u>disabled</u>, or
    - <u>enable</u> smart position
        - smart interval <u>30 minutes</u> or more
        - update distance <u>100 m</u> or more
    - <u>disable</u> altitude
    - GPS polling interval: <u>30 minutes</u> or longer
3. Telemetry: <u>off</u>
4. Device info: <u>18 hour</u> interval or longer
5. LoRa <span class="js-konami" data-alt="bunny">hop</span> limit: <u>7</u>

<details class="small">
  <summary>Explanation of the settings</summary>
  <p><code>CLIENT_MUTE</code> is the preferred starting point for mobile nodes because it avoids unexpected relay behavior in an infrastructure-based mesh. Personal or mobile nodes often experience worse SNRs than fixed nodes, which causes them to relay first and potentially stop a better-placed node from relaying. It’s also important if you have two nodes in close proximity, avoiding the <a href="https://nyme.sh/faq/#what-role-do-i-chose">“false ack”</a> problem that can hide connection issues.</p>
  <p>Smart position is preferred because it reduces the broadcasts if position hasn’t changed. However, it has trouble with altitude so it’s best to disable this—altitude is usually not helpful for mobile nodes. Generally, position doesn’t need to be sent more frequently than 30 minutes.</p>
  <p>Telemetry is disabled because we don’t need to know your battery level or channel utilization on a regular basis. Neither are meaningful to the rest of the mesh.</p>
  <p>Reducing automatic device info broadcasts avoids the throttling that inhibits the request user info features, and it makes room for more useful packets generally. Also, nodes have the ability to send node info on-demand if the operator needs to advertise their info.</p>
  <p>Personal nodes usually need more <span class="js-konami" data-alt="bunnies">hops</span> to work through the infill to get to and from the network backbone. The next-gen MediumSlow network relies on this being the maximum of <em>7</em> because the network adopts <a href="/nymesh-2/">packet-level resiliency</a> instead of link-level, and needs the additional <span class="js-konami" data-alt="bunnies">hops</span> to allow for retries and path diversity.</p>
</details>
<br>

#### Stationary personal node config

These are your base station nodes that live on your desk or your roof, _that you also send messages from_. They are nodes you connect directly to, rather than use as a relay. (If you _do not_ send messages directly from the roof node, see [below](#infrastructure-node-configuration).)

1. Role: <u>CLIENT</u>
2. Position: <u>disabled</u>, or
    - <u>disable</u> smart position
    - <u>enable</u> altitude
    - fixed position recommended
    - GPS polling interval (if applicable): <u>24 hours</u>
    - broadcast interval: <u>24 hour</u> interval or longer
3. Telemetry: <u>off</u>.
4. Device info: <u>18 hour</u> interval or longer
5. LoRa <span class="js-konami" data-alt="bunny">hop</span> limit: <u>7</u>

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

Nodes that are in a fixed location and intended solely for relay purposes. These nodes are _not_ used to send messages directly. They typically are solar builds in remote locations. (If you _do_ send messages from the node, see [above](#stationary-personal-node-config).)

1. Role: <u>CLIENT_BASE</u><sup><a href="/faq#what-role-do-i-chose">*</a></sup>
2. Rebroadcast mode: <u>Core Portnums Only</u>
3. Is Unmessagable: <u>true</u>
4. Position:
    - <u>disable</u> smart position
    - <u>enable</u> altitude
    - fixed position recommended
    - GPS polling interval (if applicable): <u>24 hours</u>
    - broadcast interval: <u>24 hour</u> interval or longer
5. Telemetry: at least <u>6 hour</u> interval
6. Device info: <u>48 hour</u> interval
7. LoRa <span class="js-konami" data-alt="bunny">hop</span> limit: <u>2</u>
8. (Optional, _strongly recommended_) Enable <a href="https://meshtastic.org/docs/configuration/remote-admin/">remote admin</a>

<details class="small">
  <summary>Explanation of the settings</summary>
  <p><code>CLIENT_BASE</code> helps differentiate the infrastructure nodes from personal nodes. It also enables handy infrastructure behaviors through favoriting adjacent routers and personal nodes, features that work best when the node is in a static position. <code>CLIENT_BASE</code> is also the recommended starting point even if the node is well sited.</p>
  <p><code>Core Portnums Only</code> will prevent propagation of custom packets or noisy applications like TAK that should not be used on a wide-area mesh, and ensure airtime remains available for text.</p>
  <p>Altitude is useful for line-of-sight estimates. But smart position has trouble with altitude if it changes due to GPS variation and can spam position unnecessarily. 24 hours is sufficient to stay on the map.</p>
  <p>Position is highly recommended for infrastructure nodes so users can understand which nodes provide coverage for them. (It doesn’t have to be exact, but should be a useful approximation.) Fixed position is recommended even if there is GPS present. The GPS is still useful for keeping the node's clock accurate, but it can cause unexpected position variations due to errant GPS signal reception. 24 hours is sufficient to maintain the clock without a meaningful drain on the battery of solar nodes.</p>
  <p>Telemetry broadcasts are useful to monitor the health of the node, but more frequent than 6 hours is excessive and takes up useful airtime.</p>
  <p>Device info is significantly curtailed because it’s not necessary for the nodes to route packets, and takes up airtime.</p>
  <p><span class="js-konami" data-alt="Bunny">Hop</span> limit: fixed nodes should focus on advertising to their immediate vicinity. They also should be within direct or single-<span class="js-konami" data-alt="bunny">hop</span> range of infrastructure, and don’t need as many <span class="js-konami" data-alt="bunnies">hops</span> to reach through the infill — they <em>are</em> the infill.</p>
</details>
<br />


### Radio settings

There are currently two different Meshtastic networks operating in the NYC area. Joining a network requires configuring your radio to use the same LoRa settings. You are free to join whichever one you can reach, or both if you have multiple devices.

<div class="callout -primary" id="mediumslow">
  <p><strong>Be a good mesh citizen:</strong> <em>Please</em> ensure your node follows the <a href="#personal-node-configuration">above configuration</a> before connecting to the network. Please do not use high-traffic applications like Reticulum or TAK on this network; they saturate the mesh and make it unusable for everyone. Sustained encrypted traffic will be detected and blocked by the infrastructure to protect the limited airtime.</p>
  <p>Current primary mesh radio settings:</p>
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
    <strong>Personal nodes: increase LoRa <span class="js-konami" data-alt="bunny">hop</span> limit to <u>7</u>.</strong> (Yes, really.)
  </p>
  <p class="small">
    This network is <a href="/preset-testing/">actively forming</a>. Not all infrastructure has moved yet. You may find it difficult to reach some parts of the network during the transition. Network status and help is available in the <a href="https://discord.nyme.sh">Discord chat</a>.
  </p>
</div>

<div class="callout" id="longfast">
  <p>Legacy network settings (LongFast):</p>
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
  <p class="small">
    These settings are the default, out-of-the-box Meshtastic settings. A bit of infrastructure is maintained on these settings to catch newcomers, travelers, and stragglers. Some users continue with this network since it provides the greater range that they need (at the expense of severe congestion).
  </p>
</div>

<details>
  <summary>Explanation of the settings</summary>
  <p>The above settings are necessary to keep the network in a high-performing state. The Meshtastic default settings are oriented toward small-scale meshes that require frequent background packets to be effective. However, on large meshes these defaults are unnecessary and quickly create congestion that compromises the utility of the network for everyone. Reducing this extraneous background traffic as much as possible is essential for preserving the usefulness of the mesh.</p>
</details>

<br>

## MeshCore

To connect to the wide-area MeshCore network in the NYC area:

1. Ensure your companion is on the [latest firmware](https://flasher.meshcore.io) <span class="js-mc-companion-firmware"></span>

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

1. Ensure your repeater is on the [latest firmware](https://flasher.meshcore.io) <span class="js-mc-repeater-firmware"></span>
2. Set zero-hop auto advert interval to <u>360 minutes</u> or more
3. Set flood auto advert interval to <u>24 hours</u> or more


<script>
  (function () {
    // Some Konami nonsense just for fun.
    const KEY_UP = 38;
    const KEY_DOWN = 40;
    const KEY_LEFT = 37;
    const KEY_RIGHT = 39;
    const KEY_B = 66;
    const KEY_A = 65;
    const COMBO = [
      KEY_UP,
      KEY_UP,
      KEY_DOWN,
      KEY_DOWN,
      KEY_LEFT,
      KEY_RIGHT,
      KEY_LEFT,
      KEY_RIGHT,
      KEY_B,
      KEY_A,
    ];
    let combo;
    function resetCombo () {
      combo = [...COMBO];
    }
    function checkCombo (event) {
      if (combo[0] === event.which) {
        combo.shift();
        if (combo.length === 0) {
          Array.from(document.querySelectorAll('.js-konami')).forEach(el => {
            const replacement = el.dataset.alt;
            el.textContent = replacement;
          });
          window.removeEventListener('keydown', checkCombo);
        }
      } else {
        resetCombo();
      }
    }
    resetCombo();
    window.addEventListener('keydown', checkCombo);
  })();
</script>

<script>
  (async function () {
    const req = await fetch('https://prod-operator.fly.dev/api/firmware/latest');
    const { meshtastic, meshcore } = await req.json();
    if (meshtastic?.stable) {
      const el = document.querySelector('.js-mt-firmware');
      el.textContent = ` (${ meshtastic.stable.replace(/\.[\w]+$/,'') }+)`;
    }
    if (meshcore?.companion) {
      const el = document.querySelector('.js-mc-companion-firmware');
      el.textContent = ` (${ meshcore.companion.replace(/\.[\w]+$/,'') }+)`;
    }
    if (meshcore?.repeater) {
      const el = document.querySelector('.js-mc-repeater-firmware');
      el.textContent = ` (${ meshcore.repeater.replace(/\.[\w]+$/,'') }+)`;
    }
  })();
</script>
