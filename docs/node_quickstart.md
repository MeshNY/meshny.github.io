Quick Site Navigation [Home](/index.html)  [Setup](/setup.html)  [Basic Node Settings](/node_configuration.html)  [Build Resources](/build_resources.html)

# nyme.sh Quickstart Guide

This quickstart guide is meant to help you get started with your Meshtastic experience. This quickstart guide will be written generically as there are some differences between the hardware nodes and the software apps, but should get you going in a good direction.  As always, feel free to reach out on the [nyme.sh Discord](https://discord.nyme.sh) for help along the way.

This guide will be broken into the following sections:
- Documentation
  - Official Documentation (you should really read these when you can)
- Hardware
  - Picking your first node
- Software
  - Using an app to connect to your node
- Connect
  - connect to the mesh and start chatting

# Documentation

There is plenty of Meshtastic documenation to read.  Listed below is offical documentation from Meshtastic
- [https://meshtastic.org/docs/introduction/](https://meshtastic.org/docs/introduction/)

Unofficial documentation listed below
- [https://makernexuswiki.com/wiki/Meshtastic](https://makernexuswiki.com/wiki/Meshtastic)
# Hardware

There are plenty of hardware nodes to choose from.  Popular manufacturers in this space include, but are not limited to:

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

# Software

Depending on what computing devices you have, pick an app to use as your primary interface to the hardware node. One thing to keep in mind is one hardware node is meant to be paired with one software app to keep a consistant node databas and message log.
- Android - [Google Play Store](https://play.google.com/store/apps/details?id=com.geeksville.mesh&hl=en_US).
- Apple iOS - [Apple App Store](https://apps.apple.com/us/app/meshtastic/id1586432531)
- [Linux Native](https://meshtastic.org/docs/hardware/devices/linux-native-hardware/)
- MacOS - [Apple App Store](https://apps.apple.com/in/app/meshtastic/id1586432531)
- Official Meshtastic Web Client - [https://client.meshtastic.org](https://client.meshtastic.org)
- [Python CLI](https://meshtastic.org/docs/software/python/cli/)

# Connect to the mesh!

You have made it this far, now it is time to chat with your locals! Check out the [basic node settings for nyme.sh](https://nyme.sh/node_configuration.html) and if you have any questions, feel free to reach out on the [nyme.sh Discord](https://discord.nyme.sh).

************ old shit below here ************

linebreak

linebreak

linebreak

linebreak

linebreak

linebreak

************ old shit below here ************

# Documentation
- [Getting Started](https://meshtastic.org/docs/getting-started/) - Official Meshtastic.org Getting Started Guide. This guide has the following sections:
  - [Install Serial Drivers](https://meshtastic.org/docs/getting-started/serial-drivers/)

  - [Initial Configuration](https://meshtastic.org/docs/getting-started/initial-config/)
  
# Software Setup

These instructions have been written for connecting to a Sense Cap T1000-E (v2.6.11) via Bluetooth, but should be similar for other devices as well.  Please see the [Getting Started](https://meshtastic.org/docs/getting-started/) guide for more information.

Your T1000-E may arrive with an older version of the Meshtastic firmware. Upgrading this device "over the air" is not currently supported from mobile, so you'll need a computer to do this. Please see the [Getting Started - Flash Firmware](https://meshtastic.org/docs/getting-started/flashing-firmware/) guide for more information.

## Web Client

[https://client.meshtastic.org/](https://client.meshtastic.org/)

#### Configure

[https://meshtastic.org/docs/software/web-client/](https://meshtastic.org/docs/software/web-client/) - Official Documentation

#### Backup

- Let the interface remind you!
  - There will be a pop-up in the lower right hand corner asking you to backup your keys, remind you in 7 days, or to never remind you.  Back your keys up, it takes <15 seconds.
- Navigation > Radio Config > Security > Private Key
  - Copy and paste into backup file of your choosing.
- Navigation > Radio Config > Security > Public Key
  - Copy and paste into backup file of your choosing.

#### Restore

- Navigation > Radio Config > Security > Private Key
  - Copy private key from backup file and paste here.
- Navigation > Radio Config > Security > Public Key
  - Copy public key from backup file and paste here.

#### Misc

## Meshtastic UI (MUI)

[https://meshtastic.org/docs/software/meshtastic-ui/](https://meshtastic.org/docs/software/meshtastic-ui/) - Meshtastic UI (MUI) is an independent user interface for Meshtastic devices, designed to provide direct interaction with the network without requiring a phone app for most basic settings.

#### Configure
#### Backup
#### Restore
#### Misc

## Python CLI

[https://meshtastic.org/docs/software/python/cli/](https://meshtastic.org/docs/software/python/cli/) - Offcial Documentation

#### Configure
#### Backup

```bash
meshtastic --export-config > MyNodeNameOrWhatever_config_04072025.yaml
```

#### Restore

```bash
meshtastic --configure MyNodeNameOrWhatever_config_04072025.yaml
```

#### Misc Node DB Export
```bash
meshtastic --nodes › MyNodeNameOrWhatever_nodedb_04072025.yaml
```
#### Misc UTF-8 Error
If you use [the Python CLI](https://meshtastic.org/docs/software/python/cli/) and have seen the following error:
```Python
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe0 in position 8: 'utf-8' codec can't decode byte 0xe0 in position 8: unexpected end of data in field: meshtastic.protobuf.User.long_name```
```
What is happening is someone managed to use a non-UTF8 char in their device name (both long and short) so the fix is to run:
```bash
meshtastic --remove-node '!0c3a9bb0' && meshtastic --set-ignored-node '!0c3a9bb0'
```

## Linux Native

#### Configure

- [https://meshtastic.org/docs/hardware/devices/linux-native-hardware/](https://meshtastic.org/docs/hardware/devices/linux-native-hardware/) - "This page outlines the setup of Meshtastic on Linux-native devices, utilizing portduino to run the Meshtastic firmware under Linux."

#### Backup
#### Restore
#### Misc

- [https://github.com/chrismyers2000/MeshAdv-Mini/tree/main/Data/Misc/Installer%20Scripts](https://github.com/chrismyers2000/MeshAdv-Mini/tree/main/Data/Misc/Installer%20Scripts) - "This is a helper script designed to help you choose which channel (beta/alpha/daily) of meshtasticd to install for raspberry pi OS"
