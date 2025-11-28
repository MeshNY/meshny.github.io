Quick Site Navigation [Home](/index.html)  [nyme.sh Quickstart Guide](/node_quickstart.html)  [nyme.sh Basic Node Settings](/node_configuration.html)  [Build Resources](/build_resources.html)

# nyme.sh Quickstart Guide

This quickstart guide is meant to help you get started with your Meshtastic experience. This quickstart guide will be written generically as there are some differences between the hardware nodes and the software apps, but should get you going in a good direction.  As always, feel free to reach out on the [nyme.sh Discord](https://discord.nyme.sh) for help along the way.

This guide will be broken into the following sections:
- Documentation
  - Official Documentation (you should really read this)
- Hardware
  - Picking your first node
- Firmware
  - Update your hardware to current firmware
- Software
  - Using an app to connect to your node
- Connect
  - connect to the local mesh and start chatting

# Documentation

There is plenty of Meshtastic documenation to read.  Below is offical documentation from Meshtastic
- [https://meshtastic.org/docs/introduction/](https://meshtastic.org/docs/introduction/)

Please take the time now if you have not already done so and read through the [Official Meshtastic Getting Started Documentation](https://meshtastic.org/docs/getting-started/). It goes into detail about [Installing Serial Drivers](https://meshtastic.org/docs/getting-started/serial-drivers/), [Flashing Firmware](https://meshtastic.org/docs/getting-started/flashing-firmware/) and [Initial Configuration](https://meshtastic.org/docs/getting-started/initial-config/).

Unofficial documentation
- [https://makernexuswiki.com/wiki/Meshtastic](https://makernexuswiki.com/wiki/Meshtastic)
# Hardware

There are plenty of hardware nodes to choose from. Nodes range from turnkey solutions (Seed Studio T1000-e for example) to DIY solar nodes with a RAK Wisblock core and a high gain antenna. Popular manufacturers in this space include, but are not limited to:

- Heltec [https://heltec.org](https://heltec.org)
- RAK Wireless [https://www.rakwireless.com](https://www.rakwireless.com)
- Seed Studio [https://www.seeedstudio.com](https://www.seeedstudio.com)

As 2025 draws to a close, the [nyme.sh MQTT stats](https://meshview.nyme.sh/stats) show these are the top 3 hardware nodes:

- [RAK WisBlock 4631](https://store.rakwireless.com/products/wisblock-meshtastic-starter-kit?variant=43884034621638)
- [Heltec V3](https://heltec.org/project/wifi-lora-32-v3/)
- [Seed Studio T1000-e](https://www.seeedstudio.com/SenseCAP-Card-Tracker-T1000-E-for-Meshtastic-p-5913.html)

# Firmware

To update the firmware of your node, you will need to use a Chromium based web-browser such as Google Chrome or Microsoft Edge.
Mozilla Firefox and Apple Safari will NOT work.
- [https://flasher.meshtastic.org](https://flasher.meshtastic.org) - Meshtastic web flasher (firmware updater)
  - [Official Flasher Documentation](https://meshtastic.org/docs/getting-started/flashing-firmware/)

Please update often to stable releases! Overview is as follows:
- Select your target device
- Select firmware
- Flash

> **_NOTE:_**  yes, you can install WITH CAUTION alpha firmware with the The Konami code: ↑ ↑ ↓ ↓ ← → ← → B A

# Software

Depending on what computing devices you have, pick an app to use as your primary interface to the hardware node. One thing to keep in mind is one hardware node is meant to be paired with one software app to keep a consistant node database and message log.
- Android - [Google Play Store](https://play.google.com/store/apps/details?id=com.geeksville.mesh&hl=en_US)
- Apple iOS - [Apple App Store](https://apps.apple.com/us/app/meshtastic/id1586432531)
- [Linux Native](https://meshtastic.org/docs/hardware/devices/linux-native-hardware/)
- MacOS - [Apple App Store](https://apps.apple.com/in/app/meshtastic/id1586432531)
- Official Meshtastic Web Client - [https://client.meshtastic.org](https://client.meshtastic.org)
  - [Official Meshtastic Web Client Documentation](https://meshtastic.org/docs/software/web-client/)
- [Python CLI](https://meshtastic.org/docs/software/python/cli/)

# Connect to the mesh!

You have made it this far, you have hardware with current firmware, an app to connect to your node, now it is time to chat with your locals! Check out the [basic node settings for nyme.sh](https://nyme.sh/node_configuration.html) and if you have any questions, feel free to reach out on the [nyme.sh Discord](https://discord.nyme.sh).
