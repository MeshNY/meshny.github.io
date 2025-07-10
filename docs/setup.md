## Documentation
- [Getting Started](https://meshtastic.org/docs/getting-started/) - Official Meshtastic.org Getting Started Guide. This guide has the following sections:
  - [Install Serial Drivers](https://meshtastic.org/docs/getting-started/serial-drivers/)
  - [Flash Firmware](https://meshtastic.org/docs/getting-started/flashing-firmware/) - There’s constant releases with bug-fixes, general improvements and new features. Please update often to stable releases!
  - [Initial Configuration](https://meshtastic.org/docs/getting-started/initial-config/)

- [Meshtastic Documentation](https://meshtastic.org/docs/introduction/)
- [Simple one-page documentation](https://makernexuswiki.com/wiki/Meshtastic)
  
## Meshtastic Official Tools
- [https://flasher.meshtastic.org](https://flasher.meshtastic.org) - Meshtastic web flasher (firmware updater)
- [https://client.meshtastic.org/](https://client.meshtastic.org/) - Meshtastic web client
  
## Node Setup Tips 
- Number of hops
  - Default: `3`
  - Set your Number of hops to `3` or `4`
  - Meshtastic App > LoRa > Number of hops
    
> **_NOTE:_**  The default of `3` should be sufficient in a healthy mesh.  "Really, 3 is fine." `4` or `5` if running CLIENT_MUTE and/or having particular difficulties, but with such a small and densely packed geographic area you are quite likely to have those higher hopped packets leave the Metro area and end up rebroadcasting over 100 miles away! Hello Catskills! This prevents the reverse of the effect we occasionally encounter where Meshes in North PA or CT will show up on the Mesh in NYC, even though they're 100 miles away, because they're running `7` hops.

- MQTT
    - Ignore MQTT
    - Default: `Enabled`
    - Meshtastic App > Lora > Ignore MQTT
  - Ok to MQTT
    - Default: `Disabled`
    - Meshtastic App > Lora > Ok to MQTT
- MQTT   Server Information
    - Enabled
    - Default: Disabled
    - Address: mqtt.nyme.sh
    - Port: 1883
    - Username: meshdev
    - Password: large4cats
    - Topic: msh/US/NY
    - Meshtastic App > MQTT > Enabled

> **_NOTE:_**  Enable the ‘Uplink Enabled’ option on your default channel to share info about nodes seen (only packets with the OK to MQTT flag will be sent)The ‘Downlink Enabled’ option will not work with this server by design. We want the mesh to stay in radio

- Device Role
  - Default: `Client`
  - Set your Device Role to `CLIENT` or `CLIENT_MUTE`
  - Meshtastic App > Device > Device Role

> **_NOTE:_**  Unless you have access to 100th floor of 1 World Trade Center or Empire State Building, you should not be using an "infrastructure" role such as `REPEATER`, `ROUTER`, `ROUTER_CLIENT` or `ROUTER_LATE`. While you may have the most honest and pure of intentions in choosing such a role the reality is they will pre-empt the large and ever-increasing number of clients`s from retransmission resulting in an over-all diminishment of the mesh's full potential. Please, don't be that person and read up on the [importance of choosing the right device role](https://meshtastic.org/blog/choosing-the-right-device-role/).

- Rebroadcast Mode
  - Default: `All`
  - Set to `Core Portnums Only` to only rebroadcasts packets with standard portnums: NodeInfo, Text, Position, Telemetry, and Routing.
  - Meshtastic App > Device > Rebroadcast Mode
 
 > **_NOTE:_**  Ignores packets from non-standard portnums such as: TAK, RangeTest, PaxCounter, etc. Should help lower high channel utilization.

## Software Setup

### Android App

#### Configure
#### Backup
#### Restore
#### Misc

### Apple iOS App

#### Configure
#### Backup
#### Restore
#### Misc

### Apple macOS App

#### Configure
#### Backup
#### Restore
#### Misc

### Web Client

#### Configure
#### Backup
#### Restore
#### Misc

### Meshtastic UI

#### Configure
#### Backup
#### Restore
#### Misc

### Python CLI
#### Configure
#### Backup
#### Restore
#### Misc

If you use [the `meshtastic` python-cli](https://meshtastic.org/docs/software/python/cli/) and have been seeing the following error:
```Python
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe0 in position 8: 'utf-8' codec can't decode byte 0xe0 in position 8: unexpected end of data in field: meshtastic.protobuf.User.long_name```
```
What is happening is someone managed to use a non-UTF8 char in their device name (both long and short) so the fix is to run:
```bash
meshtastic --remove-node '!0c3a9bb0' && meshtastic --set-ignored-node '!0c3a9bb0'
```

### Meshtastic Site Planner

#### Configure
#### Backup
#### Restore
#### Misc

### Integrations

#### Configure
#### Backup
#### Restore
#### Misc

### Meshtasticator (Simulator)

#### Configure
#### Backup
#### Restore
#### Misc

### Linux

#### Configure
#### Backup
#### Restore
#### Misc

### InkHUD

#### Configure
#### Backup
#### Restore
#### Misc
