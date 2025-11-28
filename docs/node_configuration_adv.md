Quick Site Navigation [Home](/index.html)  [nyme.sh Quickstart Guide](/node_quickstart.html)  [nyme.sh Basic Node Settings](/node_configuration.html)  [Build Resources](/build_resources.html)

# nyme.sh advanced node configuration

## Position
- somebody fill me in one day please :)

## Range Test
- somebody fill me in one day please :)

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

# nyme.sh infrastructure node configuration
url plz
