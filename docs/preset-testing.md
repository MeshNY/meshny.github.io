---
title: Radio Preset Testing
---

# Searching for Radio Settings

- Meshtastic: [“Is LongFast Holding Your Mesh Back? Better LoRa Presets for Bigger Meshtastic Networks”](https://meshtastic.org/blog/why-your-mesh-should-switch-from-longfast/)

<a href="https://k2xap.radio/mesh/lora-shapes"><img src="/images/preset-comparison.webp" alt="Series of transmissions at varying widths and lengths, labeled with the preset names." style="max-width: 120px" class="float-right"></a>

During the summer of 2025, many operators decided to undertake an organized test of different radio presets. Concerned with some rogue routers and uncooperative nodes, as well as the growing density, it seemed sensible to explore non-default radio configurations, in effect reforming the mesh. Results were mixed, see below.


## Current Preset Test

As of 2026 February 18 it’s no longer a test. We are beginning to migrate to <u>Medium Range - Slow</u>. See the [configuration info](/getting-started/#mediumslow) to connect.

The rationale for the slot and preset choice (from <a href="https://discord.com/channels/1395794339329998970/1426696399235321906/1472014386896965656">discussion</a>):

> Why move at all?
> - LongFast is very slow, nearly twice as much airtime as MediumSlow, most metros move to faster settings at densities an order of magnitude lower than what we’re at.
> - being on the default means we are constantly dealing with the unfavorable default behaviors or uncooperative operators, and all the legacy nodes
>
> Why MediumSlow not LongFast on 48?
> - MediumSlow works on a lot of the links we’ve tried, and where it didn’t that will likely be solved by participation/density and filtering
> - the reduced airtime is especially necessary for scaling, and making the network more reliable with additional routers
>
> Why not the default for MediumSlow, slot 52?
> - slight bit of additional friction will give us an opportunity to remind people of the appropriate configs via the website
> - allows surrounding regions or personal mesh users to not get automatically swamped by our traffic if they use the MediumSlow preset as well
> - Having an explicit slot avoids the complications of automatic selection based on primary name that have messed people up in previous tests
>
> Why slot 48, 913.875 MHz specifically?
> - Generally, the middle of the 915 band is more clear than either end, based on rtl_power scans: <a href="/images/rtl_power-scan.webp"><img src="/images/rtl_power-scan.webp"  style="max-width: 480px" alt="RF waterfall across the entire 915 MHz ISM band showing columns of RF activity every 300 kHz, lesser columns every 100 kHz. Large hazy portions also in columns along frequencies in the lower and upper portions of the band."></a>
> - Distance from 906.875 (LF20) and 910.525 (MC) means sites can use tight filtering more effectively, either to block remaining LF20 traffic or as dual-nodes
> - avoids the smart meter channels as best as it can without picking an explicit frequency override and/or bandwidth, only overlaps with half a major meter channel on 914.0 MHz <a href="/images/middle-slots.jpg"><img src="/images/middle-slots.jpg" style="max-width: 480px" alt="Meshtastic frequency slots superimposed over an RTL power scan showing how they overlap with different major meter activity."></a>
> - still close enough to the MediumSlow _and_ MediumFast defaults that if we change our mind about using a non-standard channel we don’t have to re-tune any filters
>
> Why not MediumFast?
> - We could try it! It might work at the current density. We don’t know.
>
> Slot 49 would also probably work fine but 48 is just a smidge farther from the MS default (52). 42 & 43 also minimally overlap a meter channel but start to get within filter range of 910.525 (MeshCore default).



## Past Preset Tests

### Test 5

- **Start Date:** 2026 February 5
- **End Date:** 2026 February 6
- **Modem Preset:** MediumSlow
- **Frequency Slot:** 22
- **Outcome:**

    This was a limited test of a few specific links, seeking to confirm we were able to continue managing key infrastructure nodes under shorter-range settings. We also sought to verify that key links could still work. The test was conducted on slot 22 since one of the nodes has a tight cavity filter and would need retuning to move elsewhere. We started on LongFast to get a baseline without congestion. As expected this performed very well. Once all the links were in place they formed a fairly linear chain of links. Without congestion we were having fluid conversations and DMs between JC, Astoria, Brooklyn Navy Yard, Far Rockaway, UES, and Garden City LI.

    The move to MediumSlow had a hiccup. Some nodes made the switch but one of the routers became unresponsive. Instead of just switching to MediumSlow as commanded, it also spontaneously moved to slot 17 and unset its region, taking itself offline. The owner was able to recover it via local connection the next morning.

    Once it was recovered, we resumed testing MediumSlow on slot 22. This also worked fairly well for the most part, but packet deliverability was lower than on LongFast. Traceroutes that did make it through showed excellent SNRs. The speculation is proximity to slot 20 plus general RF interference decreased the success of individual transmissions. Coupled with the lack of multiple paths to provide retries and route around interference, this led to packet loss.

    The takeaways of the test: 1) the high-placed routers can form a fantastic backbone for the whole metro area. 2) The infill layer is crucial to reach up to that backbone and provide packet-level resiliency. 3) The mesh is much stronger when there are multiple routes and ideally people can be direct to at least two infrastructure nodes.


### Test 4

- **Start Date:** 2025 December 8
- **End Date:** 2025 December 9
- **Modem Preset:** MediumSlow
- **Frequency Slot:** 52 (default)
- **Outcome:**

    Where it worked, it _worked_. Good links got very good due to the lack of congestion. Poor links became marginal or impossible due to the drop in link budget and inadequate packet-level redundancy. Overall the test confirmed a lot of the thinking about [how a wide-area mesh can be effective](/nymesh-2/), either through positive or negative outcomes.

    Participation was a bit limited, geographically: Jersey City, a scattering in Manhattan, some in Astoria and out to Corona, and a small handful in Brooklyn. Jersey City had pre-existing MediumSlow links, adding a few more with great success and connecting easily to Midtown. CmW2 also was able to link with P0NY in downtown Brooklyn. 25WA and P0NY provided solid relays for some, but Brooklyn infrastructure participation was otherwise nonexistent. Queens had good connections within its boundaries.

    The biggest impacts were from routers in Midtown, new to the mesh generally since the previous tests. They provided a lot of connectivity for most test participants. Unfortunately, they are unfiltered and suffer from poor sensitivity. High-powered or well situated nodes that previously could reach them when not congested had no trouble punching through the noise. Throughput increased due to the lack of collisions and shorter airtime. Remote admin was downright _snappy_. Text Message reached an 18% share of packets. However, quieter nodes trying to reach Penn experienced a clear -3 dB link budget penalty expected on paper, and the links became intermittent.

    A bit of a cliff between Manhattan and Astoria formed. Without alternate paths through Brooklyn, going from west to east was dependent on a couple of now-marginal links. Even trying new router(late)s was not enough to overcome the noise floor of the Midtown routers. Good range was clearly still possible: one of the farthest one-way links was 27 km from Midtown to North Haledon, NJ. A few packets even made it from Corona there. No packets came back.

    Takeaways:
    - a 3 dB reduction in link budget doesn’t seem like much, but it can be a critical difference for marginal connections
    - reduced congestion, due to airtime or fewer packets/users, makes the network flow well (obvious but nice to see in action)
    - filters are a must for high-placed nodes, regardless of the radio settings but especially with less link budget to work with
    - a mesh requires a critical mass to switch and provide redundant paths


### Test 3
- **Start Date:** Summer 2025
- **End Date:** Summer 2025
- **Modem Preset:** LongFast
- **Frequency Slot:** 24
- **Outcome:** Best of the three tested over the summer of 2025 for many. Those farther out still were unable to stay connected due to lack of participation by uncooperative intermediate nodes. Being off the default frequency allowed the network to escape problematic nodes.

### Test 2
- **Start Date:** Summer 2025
- **End Date:** Summer 2025
- **Modem Preset:** MediumSlow
- **Frequency Slot:** 52 (default)
- **Outcome:** Better than MediumFast but still inadequate linking all around.

### Test 1
- **Start Date:** Summer 2025
- **End Date:** Summer 2025
- **Modem Preset:** MediumFast
- **Frequency Slot:** 45 (default)
- **Outcome:** Fell flat. Even with a fairly substantial participation rate, many links did not work.
