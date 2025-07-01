# Welcome to nyme.sh!

## Connect with us on Discord
Visit us on the [Meshtastic Discord](https://discord.com/invite/ktMAKGBnBs)
Under [_Social_ -> _connect_ -> _us - NYC metro_](https://discord.com/channels/867578229534359593/1202833898376138752)

See u there ;)

# MEDIUM FAST COORDINATED TEST - JULY 2025
We are conducting a full on test to see if Medium Fast(45) is a better fit for NYC than Long Fast(20).  If you would like to participate, please do so by following the steps down below.  This test will begin July 1, 2025 and will end when the community decides our next step in the coming weeks.  Check here and our discord channel to stay current and help shape the future of our mesh!

If you are joining us on Medium Fast, please do the following:
- Backup your keys.
  - Meshtastic App > Security > Key Backup
- Firmware version 2.6.x or greater (flasher link below).
- Change your preset:
  - Meshtastic App > Settings > LoRa > 'Medium Range - Fast' or 'MEDIUM_FAST'
  - 
## Node Setup Tips
- [Update your firmware](https://flasher.meshtastic.org)!
  - There's constant releases with bugfixes, general improvements and new features.

- PLEASE set your **Role** to **CLIENT** or **CLIENT_MUTE** -> Radio Config > Device > Roles
  - Unless you have access to 100th flr of 1WTC or Empire State Building, you shouldn't be using an "infrastructure" role such as `REPEATER`, `ROUTER`, `ROUTER_CLIENT` or `ROUTER_LATE`.
  - While you may have the most honest and pure of intentions in choosing such a role the reality is they will pre-empt the large and ever-increasing # of `CLIENT`s from retranmission resulting in an over-all diminishment of the mesh's full potential.
  - Please, don't be that person and read up on the [importance of choosing the right device role](https://meshtastic.org/blog/choosing-the-right-device-role/).

- PLEASE **do not** set your **Max Hops** to **7** -> Radio Config > LoRa > Max Hops
  - The default of `3` should be sufficent in a healthy mesh.  "Really, 3 is fine."
  - `4` or `5` if running `CLIENT_MUTE` and/or having particular difficulties, but with such a small and densely packed geographic area you are quite likely to have those higher hopped packets leave the Metro area and end up rebroadcasted over 100 miles away!
  - This prevents the reverse of the effect we occassionally encounter where Meshes in North PA or CT will show up on the Mesh in NYC, even though they're >75miles away, because they're running `7` hops.

- **OK to MQTT** -> Radio Config > LoRa > OK to MQTT
  - Default is false. When set to true, this configuration indicates that the user approves their packets to be uplinked to MQTT brokers, which will allow your node to be seen on the mesh stats and map.
  - If set to false, nodes receiving your packets are requested not to forward packets to MQTT.

- **Rebroadcast Mode** to **CORE_PORTNUMS_ONLY** -> Radio Config > Device > Rebroadcast Mode
  - Ignores packets from non-standard portnums such as: TAK, RangeTest, PaxCounter, etc.
  - Only rebroadcasts packets with standard portnums: NodeInfo, Text, Position, Telemetry, and Routing.
  - Should help lower high channel utilization.

## nyme.sh Stats & Information
Note: All of these stats are powered by MQTT, if you wish to appear on the stats or maps you must enable "OK to MQTT" on your radio.

- mesh-metrics
  - [https://dash.nyme.sh](https://dash.nyme.sh) u: guest p: guest
  - source: [https://github.com/tcivie/meshtastic-metrics-exporter](https://github.com/tcivie/meshtastic-metrics-exporter)
- meshinfo
  - [https://meshinfo.nyme.sh](https://meshinfo.nyme.sh)
  - source: [https://github.com/MeshAddicts/meshinfo](https://github.com/MeshAddicts/meshinfo)
- meshview
  - [https://meshview.nyme.sh](https://meshview.nyme.sh)
  - source: [https://github.com/pablorevilla-meshtastic/meshview](https://github.com/pablorevilla-meshtastic/meshview)
- MQTT server info
  - address: mqtt.nyme.sh
  - port: 1883
  - username: meshdev
  - password: large4cats
  - topic: msh/US/NY
  - enable the 'uplink' option on your default channel to share info about nodes seen (only packets with the OK to MQTT flag will be sent)
  - the 'downlink' option will not work with this server by design. We want the mesh to stay in radio

## Services on the mesh
- hops
  - [https://w2asm.com/hops/](https://w2asm.com/hops/)
  - source: [https://github.com/morria/hops](https://github.com/morria/hops)

## Meshtastic Official Tools
- [https://flasher.meshtastic.org](https://flasher.meshtastic.org)
  - meshtastic web flasher (firmware updater)
- [https://client.meshtastic.org/](https://client.meshtastic.org/)
  - meshtastic web client

## Meshtastic Documentation
- [Meshtastic Documentation](https://meshtastic.org/docs/introduction/)
- [Simple one-page documentation](https://makernexuswiki.com/wiki/Meshtastic)

## Random Troubleshooting
If you use [the `meshtastic` python-cli](https://meshtastic.org/docs/software/python/cli/) and have been seeing the following error:
```Python
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe0 in position 8: 'utf-8' codec can't decode byte 0xe0 in position 8: unexpected end of data in field: meshtastic.protobuf.User.long_name```

What is happening is someone managed to use a non-UTF8 char in their device name (both long and short) so the fix is to run:
```bash
meshtastic --remove-node '!0c3a9bb0' && meshtastic --set-ignored-node '!0c3a9bb0'
```
