
# nyme.sh Basic Node Configuration with MQTT

The human user will have to use a software application (Android, iOS, Linux, etc) to connect and configure a hardware node.  If the firmware has not been updated, please take the time to do that now. [https://flasher.meshtastic.org](https://flasher.meshtastic.org)

Below are the basic settings the node will need to communicate with other nodes.

# Radio Configuration
## LoRa
for more information [https://meshtastic.org/docs/configuration/radio/lora/](https://meshtastic.org/docs/configuration/radio/lora/)
- **Region:** United States
- **Use Preset:** Enabled
- **Presets:** Long Range - Fast (conversationally known as LongFast, LF20 or LF)
- **Ignore MQTT:** Disabled (user wants to be apart of MQTT gathered metrics)
- **Ok to MQTT:** Enabled (user wants to be apart of MQTT gathered metrics)
- **Transmit Enabled:** Enabled (user wants the node to be able to transmit)
- **Number of hops:** 3 or 4
- **Frequency Slot:** 20 (if this is set, it overrides the Channel Name.  0 will automatically calculate based on Channel Name.
- **RX Boosted Gain:** Enabled (This is an option specific to the SX126x chip series which allows the chip to consume a small amount of additional power to increase RX sensitivity.)

> **_NOTE:_**  The default of `3` should be sufficient in a healthy mesh.  "Really, 3 is fine." `4` or `5` if running CLIENT_MUTE and/or having particular difficulties, but with such a small and densely packed geographic area you are quite likely to have those higher hopped packets leave the Metro area and end up rebroadcasting over 100 miles away! Hello Catskills! This prevents the reverse of the effect we occasionally encounter where Meshes in North PA or CT will show up on the Mesh in NYC, even though they're 100 miles away, because they're running `7` hops.

## Channels
for more information [https://meshtastic.org/docs/configuration/radio/channels/](https://meshtastic.org/docs/configuration/radio/channels/)

You need at least one primary Channel, it should be configured as follows:
- **Name:** LongFast (this will need to be set if the Frequency Slot is `0`)
- **Key Size:** Default
- **Key:** AQ==
- **Channel Role:** Primary
- **Allow Position Requests:** Disabled (disables position requests)
- **MQTT Uplink Enabled:** Enabled (user wants to be apart of MQTT gathered metrics)
- **MQTT Downlink Disabled:** Disabled (the nyme.sh MQTT server has this disabled anyway)

## Security
for more information [https://meshtastic.org/docs/configuration/radio/security/](https://meshtastic.org/docs/configuration/radio/security/)
- **Key Backup:** highly recommended to backup your private key

# Device Configuration
for more information [https://meshtastic.org/docs/configuration/radio/device/](https://meshtastic.org/docs/configuration/radio/device/)

## User
- **Long Name:** MyNodeNameOrWhatever (can be up to 36 bytes long)
- **Short Name:** AB12 (can be up to 4 bytes long)
- **Unmessagable:** Disabled (cannot Direct Message the node. Used for infrastructure nodes)
- **Licensed Operator:** Disabled (leave disabled unless you are an Amateur radio licensed operator)

## Device
- **Device Role:** Client or Client_Mute
- **Rebroadcast Mode:** Core Portnums Only (Ignores packets from non-standard portnums such as: TAK, RangeTest, PaxCounter, etc. Only rebroadcasts packets with standard portnums: NodeInfo, Text, Position, Telemetry, and Routing.)
- **Node Info Broadcast Interval:** Six Hours
- **Time Zone:** EST5EDT,M3.2.0/2:00:00,M11.1.0/2:00:00

> **_NOTE:_**  Unless you have access to 100th floor of 1 World Trade Center or Empire State Building, you should not be using an "infrastructure" role such as `REPEATER`, `ROUTER`, `ROUTER_CLIENT` or `ROUTER_LATE`. While you may have the most honest and pure of intentions in choosing such a role the reality is they will pre-empt the large and ever-increasing number of clients from retransmitting resulting in an over-all diminishment of the mesh's full potential. Please, don't be that person and read up on the [importance of choosing the right device role](https://meshtastic.org/blog/choosing-the-right-device-role/).

# Module Configuration
for more information [https://meshtastic.org/docs/configuration/module/](https://meshtastic.org/docs/configuration/module/)

## MQTT
- [dracoling's quick guide to MQTT in the nyme.sh](https://nyme.sh/mqtt.html)
