---
layout: post
title: "The engine could be better, so let's fix it."
author: "Joshua Domingo"
date:   2024-03-06 00:00:00 -1000
tags: cars cabby
categories: personal
image: /cabby/aba/check-engine.jpg
---
Inconsistent compression across the board. But why? Let's check the block and head.

## Checking the engine

We're starting with testing the block on a warm January 15, 2024. At this point, no repairs or replacement were made to the engine. Gaskets, head bolts, and timing components as found. I did a bench compression test by connecting the transmission and powering the starter with a battery, then we manually triggered the starter with a wire going to the starter solenoid and battery positive.

### Control results 

![Compression test control](https://www.sudoyashi.com/assets/img/cabby/aba/compression-test1.jpg)

| Cylinder | Dry  | Wet          |
| -------- | ---- | ------------ |
| 1        | 80   | Did not test |
| 2        | 140  | Did not test |
| 3        | 150  | Did not test |
| 4        | 190  | Did not test |

Not good. Two things that jump out to me are:
- 1. Abnormal compression on cylinder one and four
- 2. Inconsistent compression across all four cylinders

**Cylinder specifications**

| Normal Cylinder | Dry  |
| -------- | ---- 
| Compression | 145-189 psi   |
| Wear limit | 109 psi |
| Maximum difference | 44 psi  |

 I saw the readings and was hoping it was just a bad head gasket. I didn't disassemble things yet, so I ordered a new MLS head gasket and timing components to replace. After that, I went ahead I disassembled the engine and checked the head.

## Checking the head

![Check head](https://www.sudoyashi.com/assets/img/cabby/aba/check-head.jpg)

Now that's some good head.

With the long block disassembled, I removed the camshaft and then flipped the head over, sitting upside down. Do not remove anything else other than the camshaft. On a level-ish surface, I poured isopropyl alcohol and filled each chamber. With compressed air, I blew air up the intake port and exhaust port checking to see if there were any leaks in the valves.

With compressed air, blow air into each port to check for bubbles. If there are bubbles, it's a leak. If there are no bubbles, no leaks. The head passed and no leaks were found! It's not a bulletproof test, things are not at temperature and there is no pressure simulating the assembled engine, but still, very good signs. Onto the block.

### New parts, same results

![New parts](https://www.sudoyashi.com/assets/img/cabby/aba/new-parts.jpg)

Stupidly, I ordered the wrong gasket at first and got sent ELRING 915.591, which was supposed to be for the 2.0L gasket, but it didn't fit properly, not lining up with the dowel pin found near cylinder 4. I ordered another part from RockAuto, [APEX AHG904](https://www.rockauto.com/en/moreinfo.php?pk=8188476&cc=1430391&pt=5412&jsn=10) and it fit. Along with that, I got the timing belt kit which includes a new tensioner and head bolts.

Tested on February 27, 2024, on a cold night. Again the engine was tested on the "bench". Outside of the car. This invalidates the hot compression test result we would normally want to see (109+ PSI), but I'm looking for consistency. And well, we got consistency but not the way I wanted.

- New timing belt
- New tensioner
- New head gasket

![Compression test 2](https://www.sudoyashi.com/assets/img/cabby/aba/compression-test2.jpg)

| Cylinder | Dry  | Wet                            |
| -------- | ---- | ------------------------------ |
| 1        | 80   | 130                            |
| 2        | 130  | 155                            |
| 3        | 150  | 160                            |
| 4        | 210  | Did not test, put too much oil |

The wet tests looked better and that leads me to believe the rings are due for a change.

The consistency was that the second test gave us the same compression numbers. The compression tests aren't looking good. I'm getting low compression on cylinder 1, average pressure for 2 and 3, and cylinder 4 is getting monster pressure. The difference between cylinders isn't promising either. The engine could run, but not at full power. The caveat is that the tests were done on a cold engine! Nt accounting for expansion and sealing with a warm block, the tests are only an indicator until the machine shop pulls out the pistons to check on clearances there. So, let's break split the engine and test if it's a bad head.

### Piston rings and talking with Ted's Automotive Machine shop

While I would love to disassemble the whole block, I don't want to cause more issues from my mistakes in installing or incorrect torquing. I spoke to Ted's Automotive machine shop in Kalihi, Hawaii and they recommended I try another "leak" test. Add some transmission oil to the cylinders and see how much leaks past the rings. In theory, it should kind of hold some fluid but if one piston holds less than the other, then we can get more information about the cylinders. 

![Check block](https://www.sudoyashi.com/assets/img/cabby/aba/check-block.jpg)

On March 6, 20204, I filled the cylinders with 75W-90 transmission oil, with the cylinders about halfway up the walls, and left them covered for 24 hours. Afterward, it looked about the same, the level of the fluid didn't go down dramatically. Again, this tells me it's not crazy sealing issues, but it also points to a stock re-ring rather than an oversized bore and piston. Hopefully, lol.

## So, are you going to rebuild the engine?

With these results, yup we should take it to the shop lol. My wallet will hate me, but my sanity will thank me.

I was see-sawing between rebuilding and not rebuilding, ultimately, I think the final decision will come when I speak to my engine builder. In Honolulu, the only places that I heard of engine building were Snyder's and Ted's Automotive. Since I've used Ted's before, I went to them.

After consulting and telling them about my goal and current engine health (OK valves, age of engine, possible piston ring issue) they suggested it would be about $1000 for a clean rebuild. About $400 for the block to re-ring, glaze, and hone the cylinders. About $600 to build the head with new HD (heavy-duty TT) springs, seals, and possibly decking the head. For $1000, not bad! I'm sure it will be a little more expensive, but we're in a good range!

For parts, I'm going to let Ted's Automotive machine shop take care of the block components to see what I need or don't need. For the rest of the parts I'm getting:

- [Engine gasket set for ABA 2.0L with standard MLS gasket 1.65mm](https://techtonicstuning.com/product/complete-gasket-set-for-96-early99-mk3-crossflow-20-8v/)
- Replacement crankshaft bolt, just in case
- Freeze plugs

For the block, I'm going to ask them to order the piston rings, bearings, and other block components in case I need to get different components.

## 7000 Redline Golf.

The goal for the Cabby is to finish this project and not catch on fire. It's in my best interest to give it the best chance I can and if it means I need to sacrifice 4-6 more months to get it, let's get it done.

A choppy idle, with decent high-rev power with the responsiveness of ITBS. The NA ITB nature is something that suits my driving as I like being able to get on and off the throttle at a moment's notice. My aggressive and punchy style suited me a lot better when driving in an NA Miata versus my Turbo Civic.

From the internet estimates from the Vortex, 7500RPM on a healthy engine should work fine. I HOPE. The choppy 276 TT cam will sacrifice some street drivability compared to the OEM cam, but I want to use it for at SCCA as the primary "race car" so I'm not racing the Civic, since it's my daily. This build isn't revolutionary nor will it break any YouTube algorithm, but it's mine and it'll be a fun car! We don't have many other official races out here in Hawaii and I'm not planning for street races, either. This car will lose. LOL.

The specs I am planning for are:

- Engine:
  - Rebuilt block, 96+ ABA
  - Rebuilt head, 96+ ABA with TT HD springs
- Engine upgrades:
  - 276 Techtonics Tuning Camshaft, light chop
  - 40mm ITBS from a 2005 CBR600RR, custom intake flange from Nub Autoworks
  - Megasquirt 2 ECU with new wiring harness with Deutsch 29-pin connector
  - Techtonics Tuning Header back exhaust
- Wheel and Suspension
  - KW V3 suspension
  - Diamond Racing 14" wheels, lightweight "steelies" or other lightweight 14"
  - 185/60/14 Toyo RE71R
- Targets:
  - 120HP? I have no idea about the Dyno and tune. Frankly, I couldn't care less. The main point is a highly responsive NA car, the cab is just under 2100 lbs, I'm not too worried haha.

## For the legacy of a sick whip

![Cabby Mono](https://www.sudoyashi.com/assets/img/cabby/aba/cabby-mono.jpg)

I can't say I "love" the cab like others would with their dear cars. The car is disposable, but it'd be hard to find a replacement for what it does so well. Being a sick convertible car. The color, the convertible, the stories, and the shitty-ness of it, it's enjoyable, and personally want to say I finished this project. A pride thing, really. I'll have a rebuilt engine in it and that's a lot easier to market than saying I have one cylinder with low compression.

My family and friends know this is MY car. This car has become part of my identity whether I like it or not, haha. What I'm able to do and how I view the world can be expressed through my work in this car. The limit is up to my wallet and imagination. 3D printing parts and learning more about the historic Golf MK1, MK2, and MK3 influenced a lot of my choices on what I want to do with this car. It has a good vibe driving it, and especially since I live in Hawaii, it's always a good time.