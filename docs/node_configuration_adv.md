[Home](/index.html)  [nyme.sh Quickstart Guide](/node_quickstart.html)  [nyme.sh Basic Node Settings](/node_configuration.html)  [nyme.sh Advanced Node Settings](/node_configuration_adv.html)  [Build Resources](/build_resources.html)

# nyme.sh Advanced Node Configuration

## Position
- somebody fill me in one day please :)

## Range Test
- somebody fill me in one day please :)

## Local Weather

Would you like to send or get weather station messages over the mesh?  If so, you can add the weather channel to your channels. Have questions?  Answers on our [Discord weather channel](https://discord.com/channels/1395794339329998970/1426995670207824033).
- **Name:** Wx
- **Key Size:** 1 byte
- **Key:** WQ==
- **Channel Role:** Secondary
- **Allow Position Requests:** Disabled
- **MQTT Uplink Enabled:** Disabled
- **MQTT Downlonk Enabled:** Disabled

## Python CLI

[https://meshtastic.org/docs/software/python/cli/](https://meshtastic.org/docs/software/python/cli/) - Offcial Documentation

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

#### Misc

- [https://github.com/chrismyers2000/MeshAdv-Mini/tree/main/Data/Misc/Installer%20Scripts](https://github.com/chrismyers2000/MeshAdv-Mini/tree/main/Data/Misc/Installer%20Scripts) - "This is a helper script designed to help you choose which channel (beta/alpha/daily) of meshtasticd to install for raspberry pi OS"

# nyme.sh Infrastructure Node Guidelines
[nyme.sh Infrastructure Node Guidelines](/node_infrastructure.html)
