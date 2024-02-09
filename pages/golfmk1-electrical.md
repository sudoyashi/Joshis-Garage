---
layout: page
title: Volkswagen Mk1 Electrical Notes
permalink: /golfmk1-electrical
---

Got a Volkswagen? Check your grounds!

## Table of Contents

- [Terms](https://www.sudoyashi.com/electrical#electrical-terms)
- [Tools](https://www.sudoyashi.com/electrical#tools)
- [Concentric twisting](https://www.sudoyashi.com/electrical#stronger-wires-concentric-twisting)
- [Wire protection](https://www.sudoyashi.com/electrical#wire-protection)
- [Volkswagen connectors, terminals, and other parts](https://www.sudoyashi.com/electrical#volkswagen-connectors-terminals-and-other-parts)

## Terms

- **Plug**, the male end of a connector. Terminals sometimes referred to as pins or spades. They push into a receptacle.
- **Receptacle,** the female end of a connector. Terminals can receive pins or spades of a plug.
- **Connector**, end pieces that aggregate wires/cables. For example, a 3-wire hall sensor needs a 3-wire connector. There are many types of connectors and a variety of named brands like WayPak, Deustch, Delphi, and so on. Cheap ones are loose and have bad tolerances, they may not be weathertight. Premium connectors have firmer connections, better mechanical locks, and can come with insulation and weatherproofing options.
- **Wire**, a single conductor usually made with copper. Wires come in many sizes (gauges).
- **Cable**, a group of conductors. Four wires twisted together to make a cable.
- **Gauge** refers to the size of a wire. In North America, we use the [AWG standard](https://www.powerstream.com/Wire_Size.htm) for sizes. The smaller the number, the larger the wire. The larger the number, the smaller the wire. Example: Size 0 wires are usually used for cables connected directly to the battery. Size 16 wires can be used for sensors and other small applications. Size is dependent on the amps needed to carry over a distance. Guess what, there's a chart for that too: [Wire sizing chart](https://info.waytekwire.com/wire_sizing).
- **Crimp**, a solderless cold connection that clamps the wires to other wires or connectors. Or both! Some might argue they are less secure than soldered joints, but I'll argue GOOD crimps can outlast soldered connections, but you need to use the right tools and parts to make a reliable crimp. Remember to add heat shrink before you put the terminal on! Soldered joints, even proper ones, are subject to cracking over time.
- **CMA**, Circular Mil Area. The cross-sectional area of a wire. If we took a wire and cut it, then looked at the copper of the wire, that circular area is the CMA. This helps especially when splicing multiple, different sized wires together. Have you ever just stuff a 12AWG splice with a bunch of wires and hope it and crimps fine? Using CMA (read math) and specific CMA splices can give the best results. They come in a range of sizes giving you options on what to use.

## Tools

- Hozan P-707 open barrel crimper; per SuperFastMatt recommendation.
- Titan automotive crimpers
- [Klein Tools 11063W Wire Stripper/Cutter](https://www.kleintools.com/catalog/combination-cutting-tools/katapult-wire-stripper-and-cutter-solid-and-stranded-wire)
- [Klein tools 11065](https://www.kleintools.com/catalog/combination-cutting-tools/solid-and-stranded-copper-wire-stripper-and-cutter) 
- Scissors, you always need them
- 6" pliers
- 6" wire cutters
- Assortment of alligator jumpers
- Assortment of jumper wires

## Concentric twisting, it's cool but we don't NEED it.

Wire twisting, concentric wiring, and twisted pairs. These terms are the same: it means twisting multiple wires together for strength and flexibility. [HPA has a video explaining it all](https://www.youtube.com/watch?v=dsgUhNH7F7k), where I learned it from.

Wires are physically used and abused; we depend on them to work almost 100% of the time. Twisting is a preventative measure to improve the durability of wires. Similar to braiding rope, braiding or twisting individual strands together will make them work together, evenly distributing tension between wires. The cable will stretch as a unit and not just a single strand. And it is as simple as twisting a few wires together. For more consistent twisting, put one end of the cables in a drill, hold the end down and spin to win.

BUT, in the scales of time and execution, let's be frank, you do not need to be twisting every single wire out there. It takes time. You should be driving your car, not worrying about if I should be twisting this and that wire. Unless you're really going for competition motorsports, your time is better spent finishing your project, not perfecting it. This doesn't mean to skimp the process either. 

Find a balance between convenience and perfection in your work and you'll finish your projects in due time.

## Wire protection

Protecting your wires is a step above most DIY wiring projects. Here are a few material options and where they stand:

- X = good! <br>
- = is aight
- blank = nah, not worth your time

| Material                                | Easy-to-use | Engine Bay | Cabin and Trunk | Undercarriage | Resistance to fluids |
| --------------------------------------- | ----------- | ---------- | --------------- | ------------- | -------------------- |
| Electric tape                           | X           |            |                 |               |                      |
| Tesa 51036 | -           | X          | X               | X             |                      |
| Tesa 51068           | -           |            | X               |               |                      |
| Split wire plastic loom                      | X            |           | X                |              |                     |
| Split wire braided loom                         |             | X          | X               | X             | -                    |
| Raychem DR-25 | | X | X | X | X |
| Kapton tape | X |  |  |  |  |

**Don't buy electrical tape, buy Tesa tape.**

1. Electric tape is your last resort for quick repair. However, electric tape is known for its weak adhesive. It can eventually melt out and make a sticky mess around the wires because it wasn't meant for the harsh car environment. In short, only use it if you have to.

2. [Tesa tape 51036](https://www.tesa.com/en-us/industry/tesa-supersleeve-51036-pv6.html) is the premium alternative to electric tape. It's flexible, easy to use, and can withstand most applications. Don't get it confused with the softer, fuzzy Tesa tape 51068. Use this tape inside the car and in other softer environments.

3. Split wire plastic conduit or loom looks like plastic gutter stuff. This is the bulkiest item on the list, and while there are different diameters, it is stiff and can only bend so much without opening the crack. It can do the job, but it's bulky and doesn't offer the best protection as its susceptible to heat, UV, and overall not meant for long-term use.

4. The split wire braided loom is the premium alternative to the conduit. Similar to the loom above, but this one is more flexible and comes in different diameters. It's easier to manipulate since it's braided strands instead of plastic tubing. Still, fluids could permeate the loom because of its fabric.

5. Raychem, the holy grail for automotive wiring. This heat shrink tubing takes time to put together, not to mention it's costly, but if you're building a serious car then use this.

6. Kapton tape, I use it to hold wires together while building a loom.

What's the best way to protect wires? All of the above?! But at what cost?

Tesa tape with the plastic loom will make for a very stiff loom where you need it, whereas Tesa tape and the braided loom will give you flexibility. Zip ties and bits of electric tape can also be added into the mix for making wiring harnesses at your discretion, but that's where my experience stops. There are more things to learn when making a harness, but this should be good enough for general wiring. All materials have pros and cons, so weigh your wallet and options, then make an adult decision and go for it.

## Volkswagen connectors, terminals, and other parts

Did you know there are different terminal sizes? Most spade terminals are 6.3mm (1/4") wide. The wires inside a relay may be the standard 6.3mm or the smaller 2.8mm (1/8") wide terminal. 

Buy wisely; buy pricey. Good terminals will last if done well.

| Terminal width (mm) | Terminal width (in) | Application |
| ------------------- | ------------------- | ----------- |
| 2.8mm               | 1/8"                |             |
| 6.3mm               | 1/4"                |             |

| Part Name | Image                                                        | Wire | VW Part number | Usage                   | Notes                    | Equivalent part                                              |
| --------- | ------------------------------------------------------------ | ---- | -------------- | ----------------------- | ------------------------ | ------------------------------------------------------------ |
|           | ![](https://sudoyashi.com/assets/img/cabby/electrical/vw-female-receptacle.jpg) |      |                | Mk2 spotlights, sensors | You still need the boot! | [Delphi 15327868-PT](https://www.automotive-connectors.com/delphi-15327868-pt-full-assembled-037-906-240-2-way-black-2-8-timer-sealed-female-connector-assembly.html?___store=english&gclid=CjwKCAjwkYDbBRB6EiwAR0T_-rnlYzVOibuWk0x1E-h-TN55IqMm1N_qt_1sTWyExnTHmwYaYYxWJBoCcksQAvD_BwE) |
|           | ![](https://sudoyashi.com/assets/img/cabby/electrical/vw-male-plug.jpg) |      | 025 906 231    |                         | You still need the boot! | [DeyTrade 282190-1-PT](https://www.automotive-connectors.com/full-assembled-tyco-106462-1-2-way-male-junior-power-timer-connector.html) |
