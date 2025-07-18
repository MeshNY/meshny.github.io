# Documentation
- [Getting Started](https://meshtastic.org/docs/getting-started/) - Official Meshtastic.org Getting Started Guide. This guide has the following sections:
  - [Install Serial Drivers](https://meshtastic.org/docs/getting-started/serial-drivers/)
  - [Flash Firmware](https://meshtastic.org/docs/getting-started/flashing-firmware/) - There’s constant releases with bug-fixes, general improvements and new features. Please update often to stable releases!
  - [Initial Configuration](https://meshtastic.org/docs/getting-started/initial-config/)

- [Meshtastic Documentation](https://meshtastic.org/docs/introduction/)
- [Simple one-page documentation](https://makernexuswiki.com/wiki/Meshtastic)
  
# Meshtastic Official Tools
- [https://flasher.meshtastic.org](https://flasher.meshtastic.org) - Meshtastic web flasher (firmware updater)
- [https://client.meshtastic.org/](https://client.meshtastic.org/) - Meshtastic web client
  
# Node Setup Tips 
- Number of hops
  - Default: 3
  - Set your Number of hops to `3` or `4`
  - `Meshtastic App > LoRa > Number of hops`
    
> **_NOTE:_**  The default of `3` should be sufficient in a healthy mesh.  "Really, 3 is fine." `4` or `5` if running CLIENT_MUTE and/or having particular difficulties, but with such a small and densely packed geographic area you are quite likely to have those higher hopped packets leave the Metro area and end up rebroadcasting over 100 miles away! Hello Catskills! This prevents the reverse of the effect we occasionally encounter where Meshes in North PA or CT will show up on the Mesh in NYC, even though they're 100 miles away, because they're running `7` hops.

- MQTT Server Information
    - Address: mqtt.nyme.sh
    - Port: 1883
    - Username: meshdev
    - Password: large4cats
    - Topic: msh/US/NY
    - `Meshtastic App > MQTT > Enabled`

> **_NOTE:_**  Enable the ‘Uplink Enabled’ option on your default channel to share info about nodes seen (only packets with the OK to MQTT flag will be sent)The ‘Downlink Enabled’ option will not work with this server by design. We want the mesh to stay in radio

- Device Role
  - Default: Client
  - Set your Device Role to `CLIENT` or `CLIENT_MUTE`
  - `Meshtastic App > Device > Device Role`

> **_NOTE:_**  Unless you have access to 100th floor of 1 World Trade Center or Empire State Building, you should not be using an "infrastructure" role such as `REPEATER`, `ROUTER`, `ROUTER_CLIENT` or `ROUTER_LATE`. While you may have the most honest and pure of intentions in choosing such a role the reality is they will pre-empt the large and ever-increasing number of clients`s from retransmission resulting in an over-all diminishment of the mesh's full potential. Please, don't be that person and read up on the [importance of choosing the right device role](https://meshtastic.org/blog/choosing-the-right-device-role/).

- Rebroadcast Mode
  - Default:  All
  - Set to `Core Portnums Only` to only rebroadcasts packets with standard portnums: NodeInfo, Text, Position, Telemetry, and Routing.
  - `Meshtastic App > Device > Rebroadcast Mode`
 
> **_NOTE:_**  Ignores packets from non-standard portnums such as: TAK, RangeTest, PaxCounter, etc. Should help lower high channel utilization.

# Software Setup

These instructions have been written for connecting to a Sense Cap T1000-E (v2.6.11) via Bluetooth, but should be similar for other devices as well.  Please see the [Getting Started](https://meshtastic.org/docs/getting-started/) guide for more information.

Your T1000-E may arrive with an older version of the Meshtastic firmware. Upgrading this device "over the air" is not currently supported from mobile, so you'll need a computer to do this. Please see the [Getting Started - Flash Firmware](https://meshtastic.org/docs/getting-started/flashing-firmware/) guide for more information.

## Mobile App Setup (iOS & Android)

### Install the App

#### iOS (iPhone, iPad)
- Download the Meshtastic app from [Apple App Store](https://apps.apple.com/in/app/meshtastic/id1586432531).

#### Android
- Download the Meshtastic app from [Google Play Store](https://play.google.com/store/apps/details?id=com.geeksville.mesh&hl=en_US).
- Optional: You can join the beta channel to test the latest features and improvements.

### Connect to your Node

The iOS and Android apps have a similar interface. The following instructions are for iOS, but are also similar for Android. You may be prompted with a Bluetooth security warning when connecting to your node for the first time. Accept it to proceed.

1. Open the Meshtastic app and read the introduction screens.

2. Enable Bluetooth on your device and connect to your node:
   - Within the Meshtastic app, tap the lower right corner button to connect to a node.
     - Select: Bluetooth > Available Radios > scan/select node > enter pair code
     - If your node does not have a screen, the PIN is '123456'
     - If your node has a screen, look at it for the PIN

### Configure Your Node

Once connected, you should see the node's name in the upper right corner of the app. Tap the name to view the node's details. Scroll down and tape "Remote Administration" to access the configuration options.

1. Set LoRa Region
   - Options
     - Set LoRa Region (LoRa Config) > Options > Region > United States (required)
     - Use Preset: Enabled
     - Presets: Long Range - Fast
   - Advanced
     - Ignore MQTT: (default: Disabled)
     - Ok to MQTT: (default: Disabled)

   > **_NOTE:_**  For MQTT configuration information, please visit https://nyme.sh/setup.html

     - Transmit Enabled: Enabled
     - Number of hops: 3 or 4
     - Frequency Slot: 20

   > **_NOTE:_**  If you have Frequency Slot set to 0, you must name your primary channel 'LongFast'

2. Scroll to bottom and tap Save

3. Node will disconnect, reboot and reconnect.

   Your node now has a basic LongFast configuration.

4. Recommended: Set your Bluetooth Password (for devices without a screen)
   - The default password on most devices without a screen is '123456', for devices with a screen it is randomly generated and shown on the screen.
   - If you would like to change this, tap the Bluetooth button, and enter a new password.
   - You will need to reconnect with the new password after the node reboots.

5. Optional: Change your node's name
   - In the Remote Administration screen, tap the User button, and enter a new name for your node.

### Backup and Restore

#### iOS - Backup

Private Key - backup your private key to your iCloud keychain.
1. Within the Meshtastic app, select: Settings > Key Backup > Backup
2. If successful, 'Private Key saved successfully to iCloud keychain' will appear in green.

#### iOS - Restore

Private Key - restore your private key from your iCloud keychain.
1. Within the Meshtastic app, select: Settings > Key Backup > Restore
2. If successful, 'Private Key restored successfully from iCloud keychain' will appear in green.

#### iOS - Delete Backup

Private Key - delete your private key in your iCloud keychain.
1. Within the Meshtastic app, select: Settings > Key Backup > Delete icon
2. If successful, 'Private Key deleted successfully from iCloud keychain' will appear in green.

#### Android - Backup/Restore

For Android devices, backup and restore functionality may vary by app version. Check the app settings for available backup options.

## macOS Desktop App

The macOS desktop app provides the same functionality as the iOS app but is designed for Mac computers.

### Install
1. Download the Meshtastic app from the [Mac App Store](https://apps.apple.com/in/app/meshtastic/id1586432531).

### Configure
Configuration steps are similar to the mobile app:
1. Connect to your node via Bluetooth
2. Follow the same LoRa region and configuration steps as outlined in the mobile app section

### Backup/Restore
The macOS app uses the same iCloud keychain backup functionality as iOS:
- Backup: Settings > Key Backup > Backup
- Restore: Settings > Key Backup > Restore
- Delete: Settings > Key Backup > Delete icon

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
