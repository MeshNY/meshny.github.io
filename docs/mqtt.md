[Home](/index.html)  [nyme.sh Quickstart Guide](/node_quickstart.html)  [nyme.sh Basic Node Settings](/node_configuration.html)  [nyme.sh Advanced Node Settings](/node_configuration_adv.html)  [Build Resources](/build_resources.html)

# dracoling's quick guide to MQTT in the nyme.sh 

MQTT is used by [meshview](https://meshview.nyme.sh) and our other services to collect, collate, and distribute packet information from devices all over the mesh. 

In other meshes and in the original Meshtastic design MQTT is used more for relaying between remote sites. On the NYme.sh MQTT services we have disabled the relaying function as our community has shown a strong desire to maintain the mesh via radio only. 

For more information feel free to read on!

## I don't care about all the technical details, I just want to show up on the map!

Turn on "OK to MQTT" in your LoRa settings. That's all you need to do!

## Okay, maybe I care a little, how does this work?

If your node has network access (either directly or from a connected mobile client), the Meshtastic firmware has the built-in ability to share packets from the mesh to our collector service at mqtt.nyme.sh.

Various services including meshview and the dashboard can then use this collected information to create a live view of the mesh to be published online.

## Yeah, but what are all these settings?
The settings are a bit confusing when you first explore, but really break down into just a few sections. 

### LoRa settings: 
- "Ignore MQTT" setting tells your node to ignore and not relay packets that have come from a MQTT and been relayed into the mesh. We don't use the MQTT service for this, so you can set this however you want. We generally don't see any MQTT packets even from other meshes.
- "OK to MQTT" sets a flag on the packets you transmit saying "its okay to send these to the MQTT server". Without that flag the default firmware will not relay it to an MQTT server unless it's on a non-default channel or the server is on a private network.  You want this turned on if you want your messages, position, and other packets to show up in the collector.

### Module Settings (MQTT):
Enabling the MQTT module will tell your local node to relay specific packets to the configured MQTT service. Meshtastic provides one as default, but to contribute to the local community data we recommend you set this to `mqtt.nyme.sh` instead. To make it easier to enable this we use the same default username and password as Meshtastic.

#### MQTT Server Info for nyme.sh
- Address: `mqtt.nyme.sh`
- Username: `meshdev`
- Password: `large4cats`
- Encryption enabled: `yes`
- Root topic: `msh/US/NY`
- If your node only gets internet through your mobile device client, make sure to enable the "Proxy to client enabled" option.

### Channel Settings: 
Each channel has an Uplink and Downlink setting in the edit menu. These tell your local node to send packets (uplink) or download packets (downlink) for that channel from whatever is set up in its MQTT Module settings. Without the MQTT module enabled these settings will not do anything, but they will be shared as part of the channel setup when sharing via QR code or URL.

Please note that `mqtt.nyme.sh` will not send packets back to your node even if you have Downlink enabled on your channel. If using a different MQTT server you may get packets back, which in large networks could potentially overwhelm your NodeDB or cause your node to get a ton of messages. Please only enable this on other servers if you have checked your topic and other configuration carefully.    

## I still have more questions

- Check out the [Meshtastic documentation](https://meshtastic.org/docs/) for more about the [official Meshtastic MQTT server](https://meshtastic.org/docs/software/integrations/mqtt/), or the [MQTT module](https://meshtastic.org/docs/configuration/module/mqtt/)
- Feel free to ask for dracoling on our discord server if you still have questions or would like to get more involved with data collection and visualization 
