#nyme.sh basic node configuration with nyme.sh MQTT

#Radio Configuration
##LoRa - for more information https://meshtastic.org/docs/configuration/radio/lora/
- Region: United States
- Use Preset: Enabled
- Presets: Long Range - Fast (conversationally known as LongFast, LF20 or LF)
- Ignore MQTT: Disabled (user wants to be apart of MQTT gathered metrics)
- Ok to MQTT: Enabled (user wants to be apart of MQTT gathered metrics)
- Transmit Enabled: Enabled (user wants the node to be able to transmit)
- Number of hops: 3 or 4
- Frequency Slot: 20 (if this is set, it overrides the Channel Name.  0 will automatically calculate based on Channel Name.
- RX Boosted Gain: Enabled (This is an option specific to the SX126x chip series which allows the chip to consume a small amount of additional power to increase RX sensitivity.)

##Channels - for more innformation https://meshtastic.org/docs/configuration/radio/channels/
to connect with your fellow New Yorkers, you need at least one Channel. It should be configured as follows:
- Name: Long_Fast (this will set the correct Frequency Slot if set to 0)
- Key Size: Default
- Key: AQ==
- Channel Role: Primary
- Allow Position Requests: Disabled (disables position requests)
- MQTT Uplink Enabled: Enabled (user wants to be apart of MQTT gathered metrics)
- MQTT Downlink Disabled: Disabled (the nyme.sh MQTT server has this disabled anyway)

##Security - for more information https://meshtastic.org/docs/configuration/radio/security/
- Key Backup: highly recommended to backup your private key

##Share QR Code
A Meshtastic QR Code contains the LoRa config and channel values needed for radios to communicate.  You can share a complete channelconfiguration using the Replace Channels option, if you choose Add Channels your shared channels will be added to the channels on the receiving  radio.

#Device Configuration - for more information https://meshtastic.org/docs/configuration/radio/device/
##User
- Long Name: PizzaDeliveryDude (can be up to 36 bytes long)
- Short Name: PDD0 (can be up to 4 bytes long)
- Unmessagable: Disabled (cannot Direct Message the node. Used for infrastructure nodes)
- Licensed Operator: Disabled (leave disabled unless you are an Aamateur radio licensed operator)
##Bluetooth
- Enabled: Enabled (probably)
##Device
- Device Role: Client or Client_Mute
- Rebroadcast Mode: Core Portnums Only (Ignores packets from non-standard portnums such as: TAK, RangeTest, PaxCounter, etc. Only rebroadcasts packets with standard portnums: NodeInfo, Text, Position, Telemetry, and Routing.)
- Node Info Broadcast Interval: Six Hours
- Time Zone: EST5EDT,M3.2.0/2:00:00,M11.1.0/2:00:00

#Module Configuration
##MQTT
- https://nyme.sh/mqtt.html - dracoling's quick guide to MQTT in the nyme.sh

#nyme.sh advanced node configuration
##Position
##Range Test
