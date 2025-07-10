# Node Setup Tips
- Update your firmware
- Role
  - Set your Role to CLIENT or CLIENT_MUTE
  - more stuff
- Max Hops
  - Set your Max Hops to 3 or 4
  - more stuff
- MQTT
  - more stuff
- Rebroadcast Mode
  - more stuff

# Software Setup

## Android App

### Configure
### Backup
### Restore
### Misc

## Apple Apps

### Configure
### Backup
### Restore
### Misc

## Web Client

### Configure
### Backup
### Restore
### Misc

## Meshtastic UI

### Configure
### Backup
### Restore
### Misc

## Python CLI

### Configure
### Backup
### Restore
### Misc
If you use [the `meshtastic` python-cli](https://meshtastic.org/docs/software/python/cli/) and have been seeing the following error:
```Python
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe0 in position 8: 'utf-8' codec can't decode byte 0xe0 in position 8: unexpected end of data in field: meshtastic.protobuf.User.long_name```
```
What is happening is someone managed to use a non-UTF8 char in their device name (both long and short) so the fix is to run:
```bash
meshtastic --remove-node '!0c3a9bb0' && meshtastic --set-ignored-node '!0c3a9bb0'
```

## Meshtastic Site Planner

### Configure
### Backup
### Restore
### Misc

## Integrations

### Configure
### Backup
### Restore
### Misc

## Meshtasticator (Simulator)

### Configure
### Backup
### Restore
### Misc

## Linux

### Configure
### Backup
### Restore
### Misc

## InkHUD

### Configure
### Backup
### Restore
### Misc
