# Welcome to nyme.sh!

## Connect with us on Discord
Visit us on the [Meshtastic Discord](https://discord.com/invite/ktMAKGBnBs)
Under [_Social_ -> _connect_ -> _us - NYC metro_](https://discord.com/channels/867578229534359593/1202833898376138752)

See u there ;)

## Node Setup Tips
- [Update your firmware](https://flasher.meshtastic.org)!
  - There's constant releases with bugfixes, general improvements and new features.

- PLEASE set your **Role** to **CLIENT** or **CLIENT_MUTE** | Radio Config > Device > Roles
  - Unless you have access to 100th flr of 1WTC or Empire State Building, you shouldn't be using an "infrastructure" role such as `REPEATER`, `ROUTER`, `ROUTER_CLIENT` or `ROUTER_LATE`.
  - While you may have the most honest and pure of intentions in choosing such a role the reality is they will pre-empt the large and ever-increasing # of `CLIENT`s from retranmission resulting in an over-all diminishment of the mesh's full potential.
  - Please, don't be that person and read up on the [importance of choosing the right device role](https://meshtastic.org/blog/choosing-the-right-device-role/).

- PLEASE **do not** set your **Max Hops** to **7** | Radio Config > LoRa > Max Hops
  - The default of `3` should be sufficent in a healthy mesh.  "Really, 3 is fine."
  - `4` or `5` if running `CLIENT_MUTE` and/or having particular difficulties, but with such a small and densely packed geographic area you are quite likely to have those higher hopped packets leave the Metro area and end up rebroadcasted over 100 miles away!
  - This prevents the reverse of the effect we occassionally encounter where Meshes in North PA or CT will show up on the Mesh in NYC, even though they're >75miles away, because they're running `7` hops.

- **OK to  MQTT** please set to **false** | Radio Config > LoRa > OK to MQTT
  - Default is false. When set to true, this configuration indicates that the user approves their packets to be uplinked to MQTT brokers. 
  - If set to false, nodes receiving your packets are requested not to forward packets to MQTT.

- **Rebroadcast Mode** to **CORE_PORTNUMS_ONLY** | Radio Config > Device > Rebroadcast Mode
  - Ignores packets from non-standard portnums such as: TAK, RangeTest, PaxCounter, etc. 
  - Only rebroadcasts packets with standard portnums: NodeInfo, Text, Position, Telemetry, and Routing.
  - Should help lower high channel utilization. 

## nyme.sh Stats & Information
- mesh-metrics
  - [https://dash.nyme.sh](https://dash.nyme.sh) u: guest p: guest
  - source: [https://github.com/cordelster/mesh-metrics](https://github.com/cordelster/mesh-metrics)
- meshinfo
  - [https://meshinfo.nyme.sh](https://meshinfo.nyme.sh)
  - source: [https://github.com/MeshAddicts/meshinfo](https://github.com/MeshAddicts/meshinfo)
- hops
  - [https://w2asm.com/hops/](https://w2asm.com/hops/)
  - source: [https://github.com/morria/hops](https://github.com/morria/hops)

## Meshtastic Official Tools
- [https://flasher.meshtastic.org](https://flasher.meshtastic.org)
  - meshtastic web flasher (firwmare updater)
- [https://client.meshtastic.org/](https://client.meshtastic.org/)
  - meshtastic web client

## Meshtastic Documentation
- [Meshtastic Documentation](https://meshtastic.org/docs/introduction/)
