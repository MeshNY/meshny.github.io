# Welcome!

Visit us on [Discord](https://discord.com/invite/ktMAKGBnBs)

Under [_Social_ -> _connect_ -> _us - NYC metro_](https://discord.com/channels/867578229534359593/1202833898376138752)

See u there ;)


## general tips:

- [update your firmware](https://flasher.meshtastic.org)!
  - there's constant releases with bugfixes, general improvements and new features

- set your **role** to `CLIENT` or `CLIENT_MUTE`!
  - unless you have access to 100th flr of 1WTC or Empire State Building, you shouldn't be using an "infrastructure" role such as `REPEATER`, `ROUTER`, `ROUTER_CLIENT` or `ROUTER_LATE`.  while you may have the most honest and pure of intentions in choosing such a role the reality is they will pre-empt the large and ever-increasing # of `CLIENT`s from retranmission resulting in an over-all diminishment of the mesh's full potential.  please, don't be that person and read up on the [importance of choosing the right device role](https://meshtastic.org/blog/choosing-the-right-device-role/)

- **do not** set your `hops` to `7`!
  - the default of `3` should be sufficent in a healthy mesh.  `4` or `5` if running `CLIENT_MUTE` and/or having particular difficulties but with such a small and densely packed geographic area you are quite likely to have those higher hopped packets leave the Metro area and end up rebroadcasted over 100 miles away!  this prevents the reverse of the effect we occassionally encounter where Meshes in North PA or CT will show up on the Mesh in NYC, even though they're >75miles away, because they're running `7` hops
