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

1. Ensure your node is on the [latest Beta or Alpha firmware](https://flasher.meshtastic.org)<span class="js-mt-firmware"></span>
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
5. LoRa <span class="js-konami" data-alt="bunny">hop</span> limit: <u>5</u>

<details class="small">
  <summary>Explanation of the settings</summary>
  <p><code>CLIENT_MUTE</code> is the preferred starting point for mobile nodes because it avoids unexpected relay behavior in an infrastructure-based mesh. Personal or mobile nodes often experience worse SNRs than fixed nodes, which causes them to relay first and potentially stop a better-placed node from relaying. It’s also important if you have two nodes in close proximity, avoiding the <a href="https://nyme.sh/faq/#what-role-do-i-chose">“false ack”</a> problem that can hide connection issues.</p>
  <p>Smart position is preferred because it reduces the broadcasts if position hasn’t changed. However, it has trouble with altitude so it’s best to disable this—altitude is usually not helpful for mobile nodes. Generally, position doesn’t need to be sent more frequently than 30 minutes.</p>
  <p>Telemetry is disabled because we don’t need to know your battery level or channel utilization on a regular basis. Neither are meaningful to the rest of the mesh.</p>
  <p>Reducing automatic device info broadcasts avoids the throttling that inhibits the request user info features, and it makes room for more useful packets generally. Also, nodes have the ability to send node info on-demand if the operator needs to advertise their info.</p>
  <p>Personal nodes usually need more <span class="js-konami" data-alt="bunnies">hops</span> to work through the infill to get to and from the network backbone. On the next-gen MediumSlow network (see below) this changes to the maximum of <em>7</em> because the network adopts <a href="/nymesh-2/">packet-level resliency</a> instead of link-level, and needs the additional <span class="js-konami" data-alt="bunnies">hops</span> to allow for retries.</p>
</details>
<br>

### Stationary/fixed node configuration

1. Role: <u>CLIENT_BASE</u><sup><a href="/faq#what-role-do-i-chose">*</a></sup>
2. Position: <u>disabled</u>, or
    - <u>disable</u> smart position
    - <u>enable</u> altitude
    - fixed position recommended
    - GPS polling interval (if applicable): <u>24 hours</u>
    - broadcast interval: <u>24 hour</u> interval or longer
3. Telemetry: <u>off</u>, or at least <u>6 hour</u> interval if remote
4. Device info: <u>24 hour</u> interval
5. LoRa <span class="js-konami" data-alt="bunny">hop</span> limit: <u>3</u>
6. (Optional) Enable <a href="https://meshtastic.org/docs/configuration/remote-admin/">remote admin</a>

<details class="small">
  <summary>Explanation of the settings</summary>
  <p><code>CLIENT_BASE</code> helps differentiate the fixed nodes from mobile nodes. It also enables handy infrastructure behaviors through favoriting adjacent routers and personal nodes, features that work best when the node is in a static position.</p>
  <p>Altitude is useful for line-of-sight estimates. But smart position has trouble with altitude if it changes due to GPS variation and can spam position unnecessarily. 24 hours is sufficient to stay on the map.</p>
  <p>Fixed position is recommended even if there is GPS present. The GPS is still useful for keeping the node's clock accurate, but it can cause unexpected position variations due to errant GPS signal reception.</p>
  <p>Telemetry broadcasts on a local node are unnecessary. If the node is remote, 6 hours or longer is sufficient to know its health.</p>
  <p><span class="js-konami" data-alt="Bunny">Hop</span> limit: fixed nodes should focus on advertising to their immediate vicinity. They also should be within direct or single-<span class="js-konami" data-alt="bunny">hop</span> range of infrastructure, and don’t need as many <span class="js-konami" data-alt="bunnies">hops</span> to reach through the infill — they <em>are</em> the infill.</p>
</details>
<br />


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
  <p>Settings to access the <em>experimental</em> next-generation network:</p>
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
    Personal nodes: increase LoRa <span class="js-konami" data-alt="bunny">hop</span> limit to <u>7</u>. (Yes, really.)
  </p>
  <p class="small">
    Note that the <a href="/preset-testing/">migration</a> to the “MediumSlow” network is a work-in-progress. Only some of the infrastructure has moved. You may find it very difficult to reach either network, or experience unreliable message delivery. Network status and help is available in the <a href="https://discord.nyme.sh">Discord chat</a>.
  </p>
</div>

<details>
  <summary>Explanation of the settings</summary>
  <p>The above settings are necessary to keep the network in a high-performing state. The Meshtastic default settings are oriented toward small-scale meshes that require frequent background packets to be effective. However, on large meshes these defaults are unnecessary and quickly create congestion that compromises the utility of the network for everyone. Reducing this extraneous background traffic as much as possible is essential for preserving the usefulness of the mesh.</p>
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
    const req = await fetch('https://api.meshtastic.org/github/firmware/list');
    const { releases } = await req.json();
    if (releases.stable?.[0]?.id) {
      const el = document.querySelector('.js-mt-firmware');
      el.textContent = ` (${ releases.stable[0].id.replace(/\.[\w]+$/,'') }+)`;
    }
  })();
</script>
