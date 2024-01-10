---
layout: post
title: "Introducing the Megasquirt 2 plan"
author: "Joshua Domingo"
date:   2024-01-09 00:00:00 -1000
tags: cabby golfmk1 goflcabriolet vw efi megasquirt ecu
categories: cars cabby
image: /cabby/megasquirt/megasquirt-1.jpg
---
The silly journey to put EFI on a 100HP car. This is long, so grab a cup of coffee and a notebook.

**Quick links.**
You won't read this whole guide, it's long lol. So, here's the wiring diagram and parts list. Ya lazy bum.

- [Golf MK1 MS2 Wiring Diagram](https://drive.google.com/file/d/1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5/view?usp=sharing)
- [Parts list shortcut](https://www.sudoyashi.com/megasquirt2#bulkhead-parts-list)

![img](https://www.megamanual.com/ms2/v3components.gif)

## Introduction

My project for the last 3 months so far. After a couple of incidents with the Cabby's unappealing reliability, I've decided to give this car a newer life by introducing a standalone ECU, ITBS, and a whole bunch of wires and sensors to improve the drivability with a bit power.

The Golf MK1 came with mechanical fuel injection that was reliable... when it worked. When it failed me back in 2021, I decided to try carburetors to simplify the fueling to something I can continue working on. I would inevitably continue working on it until a fuel bowl gasket failure caused a small fire. It ruined the carbs and part of the engine, I wanted to get rid of the car after that, but if there's any car that I wanted to learn how to add and work with a standalone ECU, might as well start now!

We are assembling the Megasquirt 2 DIY kit on the v3.0 PCB. I will not be using the following features:

- Anything related to Idle Air Control
- MS2 "CAN" bus

## The original MegaSquirt Wiring Diagram

External Wiring with a V3.0 Main Board

This is the original diagram provided by MegaSquirt, though there are several versions of this diagram, depending on the version and generation of MS, so this may be different than the ones you could have seen before.

![img](https://www.megamanual.com/ms2/V3_ext_wire.gif)

The MegaSquirt ECU is a DIY alternative to other aftermarket ECUs to make standalone setups cheaper. It is NOT easier by any means, and it takes considerable time to work through if you have not worked with an ECU before, let alone electronics. This is not to say that it's not accessible. With a dedicated amount of time and money, anyone can work through the MS ECU if they are determined not to drop $1000 on other aftermarket ECUs.

Let's start with the wires and discuss what the ECU will control! The ECU will control fuel and spark by reading the inputs from sensors on the car. The data read by the ECU will convert into its fuel and spark outputs, which will run and adjust to the car almost instantly.

The DB37 pin #36 is an **output**, used to control an ignition module, or control a coil directly (if the high current ignition driver circuit is installed). It only needs to be connected if you are [controlling ignition timing and dwell](http://www.megamanual.com/ms2/Ignition.htm). The **ignition control signal** from MegaSquirt-II on DB37 pin#36 corresponds to the relay board pin **S5** of the 20-position terminal strip.

The final harness that I ended up with after removing wires I am not using looks like this:

### Wire Harness Terminals DB-37 Connector Megasquirt II V3.0

View the diagram online [here](https://drive.google.com/file/d/1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5/view?usp=sharing) or visit [https://drive.google.com/file/d/1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5/view?usp=sharing](https://drive.google.com/file/d/1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5/view?usp=sharing).

| Terminal or Pin | Color           | Function                                                     | IN/OUT  | Max Amps | Used? |
| --------------- | --------------- | ------------------------------------------------------------ | ------- | -------- | ----- |
| 1               | Black           | Crank sensor ground                                          | GND     | -        | YES   |
| 2               | -               | Crank sensor shield                                          | GND     | -        | YES   |
| 3               | Tan             | CAN High                                                     | (Comms) | -        | NO    |
| 4               | Tan/Red         | CAN Low                                                      | (Comms) | -        | NO    |
| 5               | Tan/Green       | -                                                            | -       | -        | NO    |
| 6               | Tan/Orange      | -                                                            | -       | -        | NO    |
| 7               | Black/White     | On-board sensor ground for, IAT, ECT, TPS                    | GND     | -        | YES   |
| 8               | -               | Spare GND                                                    | GND     | -        | NO    |
| 9               | -               | Spare GND                                                    | GND     | -        | NO    |
| 10              | -               | Spare GND                                                    | GND     | -        | NO    |
| 11              | -               | Spare GND                                                    | GND     | -        | NO    |
| 12              | -               | Spare GND                                                    | GND     | -        | NO    |
| 13              | -               | Spare GND                                                    | GND     | -        | NO    |
| 14              | -               | Spare GND                                                    | GND     | -        | NO    |
| 15              | Black           | Sensor ground, High current power ground                     | GND     | -        | YES   |
| 16              | Black           | Sensor ground, High current power ground                     | GND     | -        | YES   |
| 17              | Black           | Sensor ground, High current power ground                     | GND     | -        | YES   |
| 18              | Black           | Sensor ground, High current power ground                     | GND     | -        | YES   |
| 19              | Black           | Sensor ground, High current power ground                     | GND     | -        | YES   |
| 20              | Orange          | Intake air temperature (IAT)                                 | In      | -        | YES   |
| 21              | Yellow          | Coolant temperature sensor/Engine Coolant Temperature (ECT) | In      | -        | YES   |
| 22              | Light Blue      | Throttle position sensor (TPS)                               | In      | -        | YES   |
| 23              | Pink            | Exhaust Oxygen Sensor (EGO or O2)                            | In      | -        | YES   |
| 24              | White in Shield | TACH IN                                                      | In      | -        | YES   |
| 25              | Blue/White      | IAC1A                                                        | (Out)   | -        | NO    |
| 26              | Gray            | TPS 5V Supply                                                | Out     | 0.5A     | YES   |
| 27              | Blue/Red        | IAC1B                                                        | (Out)   | 0.1A     | NO    |
| 28              | Red             | 12V Supply                                                   | In      | 0.5A     | YES   |
| 29              | Green/White     | IAC2A                                                        | (Out)   | <1A      | NO    |
| 30              | Light green     | PWM Idle (Fan control)                                       | Out     | 0.1A*    | YES   |
| 31              | Green/Red       | IAC2B                                                        | (Out)   | 0.5A     | NO    |
| 32              | Blue            | Injector Bank 1                                              | Out     | 7A       | YES   |
| 33              | Blue            | Injector Bank 1                                              | Out     | 7A       | YES   |
| 34              | Green           | Injector Bank 2                                              | Out     | 7A       | YES   |
| 35              | Green           | Injector Bank 2                                              | Out     | 7A       | YES   |
| 36              | Brown           | Ignition signal out                                          | (Out)   | 7A       | YES   |
| 37              | Violet          | Fuel pump relay output                                       | Out     | 0.1A     | YES   |

### Deutsch bulkhead connector

![REC, 29P, BLK, E, RNG, 12/16/20, S-HDP24-24-29SE-L017](https://www.te.com/content/dam/te-com/catalog/part/HDP/242/429/HDP24-24-29SE-L017-t1.jpg/jcr:content/renditions/product-details.png)

A bulkhead connector! I've wanted to do a bulkhead because it was what all the racecars had. It looks sick and as far as reliability and durability, I wanted to give it a try. I was very excited to learn that it would cost me less than $150 in parts. Wiring and putting together connectors is the easy part, the hard part is parts availability and planning.

It's a challenge in planning and wiring that I wanted to take to prepare myself for future wiring jobs. Yes, it would be simpler to crimp the MS2 harness directly to my components, but I think automotive wiring is a challenge for most people, and if I can show others that if you can put in the time and work, it will pay dividends in reliability, consistency, and durability of the build. Mapping the diagram forces me to consider every wire going into my car and makes me understand what I'm doing.

Wiring can be a frustrating process as a DIYer, but future Josh will definitely thank me multiple times over.

The connector I plan on using is the Deutsch HDP connector. The parts list and connections are at the end of this section. Let's simplify the Deutsch connector world, as I'll list the exact part numbers I used in this build, what they do, and how to plan your build.

### Bulkhead firewall (plug) pinout

![Bulkhead pinout](https://www.sudoyashi.com/assets/img/cabby/megasquirt/wiring-bulkhead.jpg)

The plan is to take the wires from the MS2 harness and put it into the bulkhead connector. Since we know how many wires we want to use, this is how I decided on the 29-pin connector. If you need more pins and plan to include wiring for other components, factor that into your new connector. The table below shows the pins I'm using and what function from the MS2 or secondary fusebox it will provide. Find out what wire you want and if you plan to use wire splices.

[The bulkhead diagram](https://www.sudoyashi.com/assets/documents/ms2-bulkhead.pdf) or visit https://www.sudoyashi.com/assets/documents/ms2-bulkhead.pdf



| Pin  | MS2 Function                                         | Color                | Fusebox                      | AWG    | Splice CMA |
| ---- | ------------------------------------------------ | -------------------- | ---------------------------- | ------ | ---------- |
| 1    | -                                                | Red                  | Fusebox power                | 14     |            |
| 2    | -                                                | Black                | Fusebox ground               | 14     |            |
| 3    | Crank shield + signal, DB37/2,24                 | Shield, Black, White | -                            | Shield |            |
| 4    | Sensor engine ground OUT, DB37/15-19             | Black                | -                            | 14     | Yes, 5100  |
| 5    | Injector 1, DB37/32                              | Blue                 | -                            | 18/20  |            |
| 6    | Injector 2, DB37/33                              | Blue                 | -                            | 18/20  |            |
| 7    | Injector 3, DB37/34                              | Green                | -                            | 18/20  |            |
| 8    | Injector 4, DB37/35                              | Green                | -                            | 18/20  |            |
| 9    | -                                                | Red                  | Bank 1 power, Fusebox Bank 1 | 18/20  |            |
| 10   | -                                                | Red                  | Bank 2 power, Fusebox Bank 2 | 18/20  |            |
| 11   | Crank sensor ground, DB37/1                      | Black                | -                            | 18/20  |            |
| 12   | Ignition Out, DB37/36                            | Brown                | -                            | 18/20  |            |
| 13   | Sensor ground IN (ECT-, TPS-, IAT-, O2-), DB37/7 | Black                | -                            | 18/20  | Yes, 6480  |
| 14   | IAT IN, DB37/20                                  | Orange               | -                            | 18/20  |            |
| 15   | ECT IN, DB37/21                                  | Yellow               | -                            | 18/20  |            |
| 16   | TPS Signal IN, DB37/22                           | Cyan                 | -                            | 18/20  |            |
| 17   | TPS 5V Supply, DB37/26                           | Grey                 | -                            | 18/20  |            |
| 18   | O2 Signal IN, DB37/23                            | Pink                 | -                            | 18/20  |            |
| 19   | Fan control, DB37/30                             |                      | -                            | 18/20  |            |
| 20   | -                                                | Red                  | Fan relay power              | 18/20  |            |
| 21   | -                                                | Red                  | Headlight Llow               | 18/20  |            |
| 22   | -                                                | Blue                 | Headlight Rlow               | 18/20  |            |
| 23   | -                                                | Yellow               | Headlight Lhi                | 18/20  |            |
| 24   | -                                                | Blue                 | Headlight Rhi                | 18/20  |            |
| 25   | -                                                | Yellow               | O2 Sensor Power              | 18/20  |            |
| 26   | unused                                           |                      |                              |        |            |
| 27   | unused                                           |                      |                              |        |            |
| 28   | unused                                           |                      |                              |        |            |
| 29   | unused                                           |                      |                              |        |            |

#### The Deutsch Contact Size and you

![HDP Pinout 1](https://www.sudoyashi.com/assets/img/cabby/megasquirt/hdp29pinout-1.jpg)

Let's look into the Deutsch bulkhead connector. Do you know about the different materials and wire ranges between terminals? Here are 4 things to consider when choosing your connectors:

1. What size pin or socket?
   - You need both the pin and the socket. This creates the wire connection and the type of pin or socket depends on the connector you have. Refer to the specification ([Deutsch stamped contacts](https://www.te.com/commerce/DocumentDelivery/DDEController?Action=showdoc&DocId=Specification+Or+Standard%7F108-151000%7FG%7Fpdf%7FEnglish%7FENG_SS_108-151000_G.pdf%7F1060-12-0222)) on what contact size you need. There are two types of terminals: stamped and solid. Stamped ones are cheap. Solid contacts are a pricy but durable option.
2. What size AWG are you using?
   - Now, the Deutsch contact size is NOT equal to the exact AWG size. You will see size 12, 16, and 20 contacts but they come in various usable AWG, so there is some flexibility in the wire that you can use. Because of this flexibility, price and availability come into play. You need to know what size wires you are using. In my case, I am using AWG 12 AWG 18 and AWG 20. AWG 12 is for more high-power applications like the main relay and fans, while AWG 18-20 is for low-power applications like the ECU, injectors, and sensors.
   - Make sure that the pins and sockets are of the same materials when buying your parts. There are gold (Au), tin (Sn), nickel (Ni), and silver (Ag)
3. What material?
   - There are multiple to choose from. Consider Gold (Au), Nickel (Ni), Tin (Sn), and Silver (Ag). Let's focus on the most common ones, Gold and Tin. According to this [Molex article](https://www.molex.com/en-us/blog/gold-or-tin-vs-gold-and-tin), essentially gold connectors are more durable than tin, maintains a durable connection over time, and never mix the types of connectors while tin connectors are cheaper, do the job, but may not survive many mating cycles. **Tldr; buy what's available and never don't mix mating materials. Tin is cheap. Gold is highly reliable.** Some connectors may be made of both (AU/SN).
4. Is it available to buy?
   - Availability is the unspoken bane of car people. The parts exist, but your job is to find out who sells them and who has them for the cheapest price. **Tl;dr if a kit exists, buy the kit.** Hunting for the same part after the fact will ruin your future days.

After all of that, you should end up with something like this:

The cheaper, tin or nickel option. Usually stamped contacts. Generally cheaper, and you would find kits typically have the stamped terminals.

**Stamped contacts**

| Size | Socket (1062) | Pin (1060) | AWG | Material (XX) | PN | Qty | $ |
| ---- | ------ | ---- | ------------ | -------- | ---- | ------------- | ------------- |
| 12   | X      |      | 12           | Ni/Sn | 1062-12-0166 | 4 | $1 |
| 12   |        | X    | 12           | Ni/Sn | 1060-12-0166 | 4 | $ |
| 16   | X      |      | 18-20        | Sn/Sn | 1062-16-0677 | 19 | $0.69 |
| 16   |        | X    | 18-20        | Ni/Sn  | 1060-16-0622 | 19 | $0.55 |
| 20   | X      |      | 18-20        | Sn            | 1062-20-0377 | 6 | $1.04 |
| 20   |        | X    | 18-20        | Sn   | 1060-20-0177 | 6 | $0.45 |

The premium option is usually solid contacts with gold, which would run me at least $106.99. This is also considering the UNIT cost. Sometimes, you can only buy some parts in bulk of 1000 or so, so this does not include shipping, bulk costs, and overhead (mistakes). You can see why materials matter now, lol.

**Solid Contacts**
| Size | Socket (0462) | Pin (0460) | Expected AWG | Material (XX) | Part #        | Qty  | $      |
| ---- | ------------- | ---------- | ------------ | ------------- | ------------- | ---- | ------ |
| 12   | X             |            | 12           | Au            | 0462-210-1231 | 4    | $4.23  |
| 12   |               | X          | 12           | Au            | 0460-220-1231 | 4    | $2.56  |
| 16   | X             |            | 18-20        | PD/Ni/Au      | 0462-004-1631 | 19   | $2.04  |
| 16   |               | X          | 18-20        | PD/Ni/Au      | 0460-002-1631 | 19   | $1.47  |
| 20   | X             |            | 18-20        | Au            | 0462-201-2031 | 6    | $1.16  |
| 20   |               | X          | 18-20        | Au            | 0460-202-2031 | 6    | $1.030 |

XX / Tin(Sn)=309,Gold(Au)=31,Nickel(Ni)=90 or 141

#### Splicing into existing wires

These wire splices were introduced to me by this [article](https://www.hpacademy.com/blog/how-to-splice-practical-splicing-demonstration/) from High Performance Academy. There are three open-barrel splices, two of which I will be using. In this case, splices won't be by the usual AWG size but by the CMA or Circular Mil Area. Each wire has a general density of wires that we can calculate as an area. More CMA, thicker wires. This chart is a general reference for wire CMA. The chart is an average I found on wire CMA, but it's close enough to club-spec.

| Wire size (AWG) | CMA  |
| --------------- | ---- |
| 12              | 6530 |
| 14              | 4110 |
| 16              | 2580 |
| 18              | 1620 |
| 20              | 1020 |
| 22              | 642  |

Larger wires have more CMA, and smaller wires have less CMA. As we splice more wires together, we want to add them up, and then we can choose a splice.

1. 1500 CMA and less of combined wire area: [TE 62759-1](https://www.te.com/usa-en/product-62759-1.html?q=62759-1&source=header) These are a little too small for me.
2. 1500 to 5000 CMA of combined wire area: TE [63130-2](https://www.te.com/usa-en/product-63130-2.html) Example: Two 20AWG wires or two 18AWG wires for ECU splicing.
3. 5000 to 10,000 CMA of combined wire area: TE [62357-1](https://www.te.com/usa-en/product-62357-1.html?q=62357-1&source=header) Example: One 14AWG wire to four 20AWG wires for fuel injection power.

#### Bulkhead receptacle (the hot socket side)

[Part number: **HDP24**-24-29SE-L017](https://www.te.com/usa-en/product-HDP24-24-29SE-L017.html)
Housing for Female Terminals, Wire-to-Wire, 29 Position, Sealable, Black, Wire & Cable, Power & Signal, Panel Mount, Hybrid

The receptacle, the socket or female end of the connector, is where we'll connect the Megasquirt harness. This will be routed in the car and then mounted on the firewall. As a tip from TE Connectivity, use the socket side as the hot side (the one connected to the battery) so you don't shock yourself.

#### Bulkhead Plug (the cold pokey side)

[Part number: **HDP26**-24-29PE-L017](https://www.te.com/usa-en/product-HDP26-24-29PE-L017.html)
Housing for Male Terminals, Wire-to-Wire, 29 Position, Sealable, Black, Wire & Cable, Power & Signal, Panel Mount, -67 – 257 °F [-55 – 125 °C], Hybrid

The plug side will be mounted on the firewall.

#### Bulkhead Parts list

| Item                                  | Image                                                        | Description                                    | Part Number        | Quantity | Subtotal |
| ------------------------------------- | ------------------------------------------------------------ | ---------------------------------------------- | ------------------ | -------- | -------- |
| Deutsch socket                        | ![HDP24-24-29SE](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/5555/MFG_HDP24-24-29SE-L017.jpg) | Bulkhead plastic socket, 29-pin                | HDP24-24-29SE-L017 | 1        |          |
| Deutsch plug,                         | ![HDP26-24-29PE](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/432/HDP26-24-29PE-L017.jpg) | Bulkhead plastic plug, 29-pin                  | HDP26-24-29PE-L017 | 1        |          |
| Medium splice                         | ![Medium splice](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/805/63130-2.jpg) | Splices for my 18-20AWG                        | 63130-2            | 100      | $8.52    |
| Large splice                          | ![Larger splice](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/632/62357-1.JPG) | Splices for my 14AWG                           | 62357-1            | 100      | $11.25   |
| Size 12 Solid Receptacle pin (female) | ![12 pin](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2209/0460-204-12141.JPG) |                                                | (1060) 0460-XXX-12 |          |          |
| Size 12 Solid Plug pin (male)         | ![12 plug](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2236/0462-203-12141.jpg) |                                                | (1062) 0462-XXX-12 |          |          |
| Size 16 Solid Receptacle pin (female) | ![Size 16 receptacle](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2236/0462-203-12141.jpg) |                                                | (1060) 0460-XXX-16 |          |          |
| Size 16 Solid Plug pin (male)         | ![Size 16 plug](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/891/MFG_0460-202-16141.jpg) |                                                | (1062) 0462-XXX-16 |          |          |
| Size 20 Solid Receptacle pin (female) | ![Size 20 receptacle](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/799/0460-202-1631.jpg) | 16-20AWG, Gold, 0460-202-1631                  | (1060) 0460-XXX-20 |          |          |
| Size 20 Solid Plug pin (male)         | ![Size 20 receptacle](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2282/0462-201-1631.JPG) | 16-20AWG, Gold, 0462-201-1631                  | (1062) 0462-XXX-20 |          |          |
| Boot                                  | ![HD30 boot](https://www.te.com/content/dam/te-com/catalog/part/HD3/024/BTB/HD30-24BT-BK-t1.jpg/jcr:content/renditions/product-details.png?w=220) | Protective boot                                | HD30-24BT-BK       | 2        | $3.07    |
| Terminal 2.8mm                        |                                                              | General terminal for most pins and receptacles |                    |          |          |
| Terminal 6.8mm                        |                                                              |                                                |                    |          |          |
| Fuse holder with terminals            | ![DigiKey Fuseholder](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/12/178.6152.0001.JPG) | Individual fuse holder                         | DigiKey, F5194-ND  |          |          |
|                                       |                                                              |                                                |                    |          |          |

### Fuse and relay panel

The history of Golf Mk1/Mk2 and Polo rallies has always attracted me from my short time playing Dirt Rally 2.0. This is optional for most builds, but the Golf Mk1 factory wiring is pretty tired, so I'm rewiring some things for reliability.

That's enough wiring technicalities. Let's talk about the actual MegaSquirt now.

## Defining the MegaSquirt functions

The MegaSquirt controls our engine by reading a bunch of inputs; it will figure out what's happening, then output the correct fuel and spark accordingly. To do that, we set up the sensors to collect the data, then wire up a way to control the fuel injectors and ignition coil.

## Sensors

Most engines will use the following sensors:

| Sensor                           | MS Pin#                      | MegaSquirt Wire Color        | Ground    | Connection                                                 | Existing or Buy | Part Name or Number                                          | # Total wires | Wires                              |
| -------------------------------- | ---------------------------- | ---------------------------- | --------- | ---------------------------------------------------------- | --------------- | ------------------------------------------------------------ | ------------- | ---------------------------------- |
| Manifold Absolute Pressure (MAP) | none                         | none                         | none      | 1/8" vacuum line                                           | Existing        | none                                                         | none          | none                               |
| Intake Air Temperature (IAT)     | 20                           | Orange                       | ECU       | 3/8" NPT                                                   | Buy             | [GM IAT](https://www.diyautotune.com/product/gm-open-element-iat-sensor-with-pigtail/) | 2             | 5V, Signal                         |
| Engine Coolant Temperature (ECT) | 21                           | Yellow                       | ECU       | Four wire: 2 are ground, 1 PCM (ECU IN), 1 to gauge sender | Existing        | VW Golf MK3 ECT                                              | 4             | Ground, signal, Ground, temp gauge |
| Throttle Position (TPS)          | 22                           | Light Blue                   | ECU       | Honda TPS                                                  | Buy (on ITBS)   | Honda OEM TPS                                                | 3             | Ground, 5V, signal                 |
| Exhaust Gas Oxygen (O2 or EGO)   | 23                           | Pink                         | ECU       |                                                            | Existing        | AEM Wideband X-Series                                        | 6             | Multiple, splice only              |
| Ignition (VR)                    | 24                           | White/Shield                 | ICM       | Hall-effect signal splice                                  | Existing        | TACH IN                                                      | 3             | Ground, 5V, signal                 |

### Manifold Absolute Pressure Sensor

![MS MAP](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-map.jpg)

### Intake Air Calibration

![MS IAT](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-iat.jpg)

| Temperature | Ohms |
| ----------- | ---- |
| 48F         | 7000 |
| 87F         | 1930 |
| 146F        | 560  |

### Coolant Temperature Sensor Calibration

https://www.clubgti.com/forums/index.php?threads/coolant-temp-sensor-what-does-it-do.86982/

![Coolant Temperature Sensor calibration](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-clt.jpg)

Pin 1 A

Pin 2 B

Pin 3 A

Pin 4 B



Measure resistance between pins 1 and 3 at three different temperatures.

Pin 2 and 4 provide a temp readout to our gauge readout.

| Temperature | Ohms |
| ----------- | ---- |
| 88F         | 1880 |
| 87F         | 1930 |
| 146F        | 560  |

### TPS Sensor Calibration

![Megasquirt TPS](Chttps://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-tps.jpg)



### O2 Sensor Notes

![Megasquirt O2](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-o2.jpg)

### Idle Air Control

No idle air control will be modulated on the ITBS. This will only be handled by warm-up enrichment and wax idle mechanical enrichment. 

This means:

- No stepper IAC
- No PWM IAC
- Ignore the following:
  - IAC1A, DB37 pin 25
  - IAC1B, DB37 pin 27
  - IAC2A, DB37 ping 39
  - IAC2B, DB37 pin 31
  - S12C to JS9

### Ignition with the VR sensor

![MS2 VR Sensor](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-vr.png)
VR Sensor 021 907 319A
https://www.msextra.com/forums/viewtopic.php?t=38492

Pin 1 Signal

Pin 2 Ground

Pin 3 Shield

We control the ABA using its OEM configuration, a 60-2 wheel, and a VR sensor. This wiring is SIMILAR to the Bosch 124 module, but not exact.

In the case of the Golf, the wiring is slightly different:

[Ignition MegaSquirt](https://www.sudoyashi.com/assets/documents/ms2-ignition.pdf)

![ignition](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-ignition.jpg)

Similar to the Direct Ignition Coil Control with Bosch 124 (7-pin module), we can control ignition by tapping into the existing ICM. The current Ignition Control Module (ICM) is as follows:

| Pin  | Function                  |
| ---- | ------------------------- |
| 1    | Ground for ignition coil  |
| 2    | ICM Ground                |
| 3    | Hall-Effect sensor ground |
| 4    | 12V for ignition coil     |
| 5    | Hall-Effect sensor 12V    |
| 6    | Hall-Effect signal        |
| 7    | --unused--                |

On the left are the original functions and wiring paths, and on the right are the functions adding the MegaSquirt.

| Pin   | Function  |      | Pin   | Function               |
| ----- | --------- | ---- | ----- | ---------------------- |
| HE/1  | GND HE    |      | HE/1  | GND HE                 |
| HE/2  | Signal    |      | HE/2  | **-**                  |
| HE/3  | Power     |      | HE/3  | Power HE               |
| ICM/1 | GND Coil  |      | ICM/1 | GND Coil               |
| ICM/2 | GND ICM   |      | ICM/2 | GND ICM                |
| ICM/3 | GND HE    |      | ICM/3 | GND HE                 |
| ICM/4 | 12V Coil  |      | ICM/4 | 12V Coil               |
| ICM/5 | 12V HE    |      | ICM/5 | 12V Hall-Effect Sensor |
| ICM/6 | Signal HE |      | ICM/6 | **DB37/36 IGN OUT**    |
| ICM/7 |           |      | ICM/7 | -                      |

Why not eliminate the HE sensor if you aren't using it? Idk; I'm scared to cut it out and find out I need it later, LOL.

The original configuration uses the mechanical events from the trigger window in the distributor to create a signal to the ICM. With the MegaSquirt, we use the input from the VR sensor. This output signal will trigger the ICM and allow us to control the ignition.

Similar to the Bosch 0 227 100 124 'igniter' module (called the "*Bosch 124*" here), the ICM is not a 'smart' module. That is, it DOES NOT control dwell. Because of this, we need to use the HEI settings in MegaSquirt-II to set the dwell, etc. The Bosch 124 fires the coil when the signal from MegaSquirt-II goes from high to low, just like the 7-pin HEI. We will use the following values as shown.

| *Parameter*            | *Value*                                                      |
| ---------------------- | ------------------------------------------------------------ |
| Ignition Input Capture | **Rising Edge** Signal through optoisolator (U4)('Falling Edge' *for MicroSquirt® if using the VR input circuit*) |
| Cranking trigger       | **Trigger Rise**                                             |
| Coil Charging Scheme   | **Standard Coil Charge**                                     |
| Spark Output           | **Going High (Inverted)** for production MS-II('Going High (Inverted)' *for MicroSquirt*) |

## Fuel System

Parts:

- Fuel injectors:
- Fuel pump:
- Fuel pressure regulator: