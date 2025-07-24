# Welcome to nyme.sh!

## Connect with us
**New York City and other New York State regions**

- nyme.sh Discord - [https://discord.gg/tk5a6sSdyS](https://discord.gg/tk5a6sSdyS)
  - (If your local mesh needs a local channel, stop by and let's chat)

see u there ;)

**Long Island Suffolk/Nassau/Queens**

- Visit us on the [Meshtastic Discord](https://discord.com/invite/ktMAKGBnBs)
Under [_Social -> connect -> US NY - Long Island Suffolk/Nassau/Queens_](https://discord.com/channels/867578229534359593/1292647069256913031)

**Capital Region and Hudson Valley**

- Visit us on the [Meshtastic Discord](https://discord.com/invite/ktMAKGBnBs)
Under [_Social -> connect -> US - NY Capital Region and Hudson Valley_](https://discord.com/channels/867578229534359593/1282698033657811105)

**Rochester**

- Visit us on the [Meshtastic Discord](https://discord.com/invite/ktMAKGBnBs)
Under [_Social -> connect -> US-Rochester, NY_](https://discord.com/channels/867578229534359593/1292647069256913031)

**Sullivan County and the Southern Catskills**

- Kaatskills Mesh [https://kmesh.us/](https://kmesh.us)

- Join the [Hudson Hams Discord server](https://discord.gg/2J6BuhR) to get in touch

**Westchester County**

- Visit us on the [Meshtastic Discord](https://discord.com/invite/ktMAKGBnBs)
Under [_Social -> connect -> US - NY - Westchester County_](https://discord.com/channels/867578229534359593/1383046714763509910)

**If you would like to be added to this list, [submit a pull request](https://github.com/MeshNY/meshny.github.io/pulls)**

## Coordinated Testing – July 2025

After testing **MediumFast** then **MediumSlow** we're now testing **LongFast** with a non-default frequency.

We ran a community test to see if **MediumFast** or **MediumSlow** would be a better fit for NYC than LongFast. The test originally began with MF on **July 1, 2025** and continued for a few weeks until we decided neither Medium preset was working as well as we had hoped in the challenging RF Environment of NYC.  While there were noticeable gains in the mesh's responsiveness from the faster transmissions times reliability remained illusive.

## How to Join the Test

1. **Back up your keys**
   `Meshtastic App > Security > Key Backup`

2. **Make sure you're on firmware 2.6.x or later**
   [Firmware flasher within 'Node Setup Instructions'](https://nyme.sh/setup.html).

3. **Change your Primary channel**
   `Meshtastic App > Settings > Channel > Primary`:
    - Name: `nyme.sh`
    - PSK/Key: `AQ==`

4. **Change your LoRa preset**
   `Meshtastic App > Settings > LoRa >`
    - Presets: **`Long Range - Fast`** or **`LONG_FAST`**<br />
   Make sure **Frequency Slot** is set to `24` (or `0` if you're on iOS/macOS though fine to explicitly set `24`)

   If you use the `meshtastic` python-cli to manage your node(s) can set them all in one go:<br />
   `meshtastic --ch-set name nyme.sh --ch-set psk default --ch-index 0 --set lora.channel_num 24`



## Node Setup Instructions
The community has compiled a list of [Setup](https://nyme.sh/setup.html) resources to help everyone get nodes setup correctly.  Please take the time to review [this information](https://nyme.sh/setup.html).  This is also a great reference to aid in troubleshooting your software configuration.

## MQTT nyme.sh Stats & Information
  - mesh-metrics
    - [https://dash.nyme.sh](https://dash.nyme.sh) u: guest p: guest
    - source: [https://github.com/tcivie/meshtastic-metrics-exporter](https://github.com/tcivie/meshtastic-metrics-exporter)
  - meshinfo
    - [https://meshinfo.nyme.sh](https://meshinfo.nyme.sh)
    - source: [https://github.com/MeshAddicts/meshinfo](https://github.com/MeshAddicts/meshinfo)
- meshview
    - [https://meshview.nyme.sh](https://meshview.nyme.sh)
    - source: [https://github.com/pablorevilla-meshtastic/meshview](https://github.com/pablorevilla-meshtastic/meshview)

> **_NOTE:_**  All of these stats are powered by MQTT, if you wish to appear on the stats or maps you must enable "OK to MQTT" on your radio.

## Services on the mesh
- hops
    - [https://w2asm.com/hops/](https://w2asm.com/hops/)
    - source: [https://github.com/morria/hops](https://github.com/morria/hops)
