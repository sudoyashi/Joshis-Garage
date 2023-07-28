---
layout: post
title:  "Oh baby got back"
date:   2023-07-30 00:00:00 -1000
categories: Volkswagen golf cabby projectcar bikecarburetors
image: /cabby/while-im-in-there/fuelsystem-1.jpg
---

## The Cabby lives again

Thankfully, no catastrophic damage.

I checked everything that I could without doing a full teardown. Compression, hoses, and all seem healthy. A carbon buildup on the spark plugs but that's ok. The car is still on jack stands at the moment because I'm doing more maintenance items before getting back on the road. Don't want more shit breaking on me, now do we. Future Josh will appreciate it. As far as what has been done, this is the breakdown of the issues I found, my solutions, and a short description of what they are.

## Table of Contents

- 1. 

<hr>

## Fuel system - Need an outie for my innie

Estimated time: 6-8 hours
![Cleaned fuel system parts](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/fuelsystem-2.jpg)
You may be surprised to know that my fuel system doesn't have a return line. Why? Because I was lazy... and I also broke the return line's fitting LOL. Other than cleaning them up, I can also make adjustments to the actual carb setup. Since the car is down, I'm making some adjustments to my fuel system.

### Issue: Intermittent car pops on idle - not the good kind

**Solution: Needle jet position leaned out by 1 step. New throttle cable.

When I blip the throttle from a stop, there is a backfire from the intake side. The cause is probably the excess dump of fuel on blip that the car surges and doesn't combust in the engine, so the only way is out the intake in this scenario. Usually, we'd expect it in the rear so I can spit flames! Sadly, not the case. [source1 on diagnosing throttle blips](https://www.vulcanforums.com/threads/lean-popping-from-carb-at-idle-blipping-the-throttle.304374/) [source2 on diagnosing throttle blips](https://www.chopcult.com/forum/showthread.php?t=39845). To fix this, I'm changing the needle jet clip position.

![Needle jet adjustment](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/fuelsystem-4.jpg)

Jet adjustments should be made in parts, adjusting one system at a time to keep your sanity when tuning. However, I was running rich for a while with these carbs from 1/8 - 3/4 throttle. We can correct this with a needle jet adjustment. My last setup had my needle at position 3 plus a shim, so effectively, my needle jet height was in position 4 which leans towards a richer mixture. I'll remove the shim to lower the needle jet.

![New throttle cable](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/throttle-cable-1.jpg)

The throttle cable also got burnt in some spots of the cable, which caused issues with the cable action. This was an easy replacement and just got another motorocycle cable replacement kit. It comes with all the tiny parts to complete the cable. This includes the cable ends, cable length adjustments, and cable sheathe. The new cable took about 40 minutes to put together, scavenging some parts from the old throttle cable to hold down the cable from the factory positions. The smarter idea would be to make a line with exact routing to the throttle actuator, but I don't have time for that!

### Issue: My idle was screwing around

**Solution: Set idle screws back to 2.5 turns out"

![Idle adjustment screws and notes](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/fuelsystem-5.jpg)

To my surprise, my idle adjustment screws were all over the place! From carb 1 through 4, it went from 2, 2.5, 4.5, and then 3.75. They should all be the SAME. Not sure if I was making adjustments or if they got lost. I set them back to 2.5 turns.

**Idle adjustment screw turns out**

|        | Carb 1 | Carb 2 | Carb 3 | Carb 4 |
| ------ | ------ | ------ | ------ | ------ |
| Before | 3.75   | 4.5    | 2.5    | 2      |
| After  | 2.5      | 2.5      | 2.5 turns | 2..5 turns |

The current jet settings for my ZX6R carburetors are:

**ZX6R Carburetor settings**

|                 | Carb 1                         | Carb 2                         | Carb 3                         | Carb 4                         |
| --------------- | ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| Pilot           | 38                             | 38                             | 38                             | 38                             |
| Main            | 160                            | 165                            | 165                            | 160                            |
| Needle          | 3rd position, (middle) no shim | 3rd position, (middle) no shim | 3rd position, (middle) no shim | 3rd position, (middle) no shim |
| Idle Adjustment | 2.5 turns                      | 2.5 turns                      | 2.5 turns                      | 2.5 turns                      |


Intended tune: slightly lean idle, closer to 15AFR than 14.7AFR. I'll inspect idle speed and vacuum to see how it likes it.

### Issue: Vapor lock - I want to be alive! Installing a return line

**Solution: Install a return line.**

![Return line in engine bay with cutter](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/fuelsystem-6.jpg)

I opened up the metal return line with a [tiny metal hose cutter](https://www.homedepot.com/p/RIDGID-1-4-in-to-1-1-8-in-101-Close-Quarters-Copper-Aluminum-Brass-and-Plastic-Tubing-Cutter-Multi-Use-Tubing-Tool-40617/100075014), the Ridgid tool was the perfect tool for the job because it was in such a hard to reach place. Then I used a -6 AN adapter to 5/16" hardline with a -6 AN to 5/16" barb end fitting. 

Initially, I bought a whole $200 AN hose kit to redo my whole fuel system, but later on, I decided to return most of the parts and just used regular fuel hose. AN hose that is NOT PTFE I felt was more money for less return. This isn't a fuel injected car so running the rubber hose would be ok. Carbureted applications don't run much fuel pressure. I'll buy the PTFE hose set if it comes to it. AN lines would be great for other applications, but not for this use case.

![Wix filter in-line to 1/4"](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/fuelsystem-7.jpg)
In engine bay, the fuel IN path is:

- Factory hardline with barbed end
- 5/16" fuel hose
- WIX 33040 fuel filter IN
- 5/16" fuel hose
- Aeromotive Fuel Pressure Gauge, 1-15 PSI
- 5/16" fuel hose
- Carburetors

The fuel OUT or RETURN path is:
- WIX 33040 fuel filter RETURN
- 1/4" fuel hose
- 1/4" to 5/16" brass adapter
- 5/16" barb to 6AN adapter to hardline (3 fittings tied together)
- Factory return line

The 5/16" barb will connect my return line to my new fuel filter, a [WIX 33040](https://www.amazon.com/WIX-Filters-Complete-Line-Filter/dp/B000C9UJAA). This routes extra fuel/vapors back to my fuel tank. This filter worked for my application because it had 5/16" inlet and outlet ports, though the return port was 1/4". Using 1/4" hose, I connected it with a 1/4" to 5/16" adapter, which returned to the newly adapted hardline.

Lastly, I reopened the return lines near the fuel tank return. Using the previously return lines, I connected this hose back to the fuel tank with 5/16" union barbs and secured the dangling hose with some good ol' zip ties.

### Replace the burnt stuff

**Solution: Replace all the shitty, burnt parts**

![Coolant splashed on everything](https://www.sudoyashi.com/assets/img/cabby/badrad/damage3.jpg)
Since the coolant splashed EVERYWHERE it could in the engine bay, the air filter got damaged, vacuum lines, and other parts also got burnt. The following items had to get replaced, cleaned, or repaired:
- All surrounding coolant lines
- Radiator
- Radiator fan
- Carburetor caps
- Various vacuum lines
- Throttle cable
- Air filter
- Headlight wiring harness
- Crankcase vent filter

### Summary of replacement and repaired issues

The work itself was not difficult, but sourcing the parts since almost all of the parts are from off-island makes the repair a lot more challenging. Planning and considering future solutions also come into the mix.

- Purchased parts:
  - Crankcase vent filter
  - Any applicable fittings
  - Throttle cable
- Cleaned and Inspected:
  - Inspect fuel bowls
  - Inspect jets
  - Clean carburetor system
- Adjust:
  - Needle jet clip to 3, no shim
- Install:
  - Fuel filter with inline return
  - Fuel return line, engine bay
  - Fuel return line, rear
  - Throttle cable
  - Replacement hoses


## Future work for future Josh

### Brakes - Just the parking brake!

![New parking brake cables](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/parking-brake-1.jpg)
Estimated time: 1.5 hours

This is going to be the simplest of all the issues that I have, I just have to install these new parking brake cables. The ones on the car are probably the original cables. These cables aren't doing their job that well anymore, I have to yank that brake to its highest click setting in order to lock my car down, not ideal. But, I am tired and I really want to just finish the mandatory work. I swear I'll do this job when I make the time for it next week, haha.

![Parking brake cable to drum](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/parking-brake2.jpg)

New cables will just need to be fed through the bottom, hooked up to the parking brake lever in the drum brake system, and then fastened down from the cabin to ensure proper tension. I'll probably have to make more adjustments after the cables stretch into its normal position.

![Crank that brake](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/parking-brake3.jpg)

## Fluids - Transmission and Cooling

![Transmission fluid draining](https://www.sudoyashi.com/assets/img/cabby/while-im-in-there/transmission-maintenance-1.jpg)
Estimated time: 3 hours or more (depends on bleeding)

### Transmission fluid

Estimated time: 1 hour

Draining and filling transmission fluid is pretty straightforward. You need a 17mm hex socket (like a massive allen wrench). [Here's a VWVortex guide](https://vwgolfmk1.org.uk/forum/index.php?page=topicview&id=how-to_2%2Fguide-changing-your_6). I'm replacing it with 75W-90 Valvoline gear oil.

Cabby info compiled a wealth of information on everything related to the cab. Check out their write-up on [Transmission and Clutch](https://www.cabby-info.com/transmission.htm) here. I use this site for all my references and I'm hoping that my own sudoyashi.com can be a wealth of custom information some day too!

### Water and coolant

Estimate time: 2+ hours

Filling coolant is straightforward... fill the car with coolant. I bought a bunch of distilled water to make sure it's as clean as possible before moving it through the new radiator. I'll be doing the initial coolant job with just the distilled water, maybe with Water Wetter, but once I'm satisfied with how clean the car is, I'll switch to coolant. I'm using G12 coolant to fill the system once the system is as clean as it gets.. From the local VW dealership, it was about $25 per gallon jug. 

## It never ends...

I could have rushed this project to get it back up and running as soon as possible but life and finances get in the way. It's okay, I'm taking my time trying to put together, I know I cut corners as my energy and motivation gets lowere and lower from sprinting to the end. This work was long overdue and I got away with running away from maintenance issues for too long. One way or another the car was going to get fixed lol. 

I'm hoping to wrap this car up by the end of July so that I have a bit of time to enjoy it in August and September. Once the Fall and Winter months start to roll in, we're going for my very first performance mod--a new camshaft.

==== DRAFT ====

## Photograph these things



| Image                                          | Name                           |
| ---------------------------------------------- | ------------------------------ |
|                                                | fuelsystem-1.jpg               |
| Cleaned fuel system parts                      | fuelsystem-2.jpg               | done
| Fuel system diagram 2023                       | fuelsystem-3.jpg               |
| Needle jet adjustment                          | fuelsystem-4.jpg               | done
| New throttle cable                             | throttle-cable-1.jpg           | 
| Idle adjustment screws and notes               | fuelsystem-5.jpg               |
| Return line in engine bay with cutter          | fuelsystem-6.jpg               |
| Wix filter in-line to 1/4"                     | fuelsystem-7.jpg               |
| Coolant splashed on everything                 | damage3.jpg                    |
| New parking brake cables                       | parking-brake-1.jpg            |
| Parking brake cable to drum                    | parking-brake-2.jpg            |
| Crank that brake. Parking brake cable to lever | parking-brake-3.jpg            |
| Transmission fluid draining                    | transmission-maintenance-1.jpg |
| It never ends                                  | maintenance-never-ends.jpg     |