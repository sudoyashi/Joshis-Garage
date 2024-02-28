---
layout: post
title: "Introducing the Megasquirt 2 plan"
author: "Joshua Domingo"
date:   2024-01-09 00:00:00 -1000
tags: cabby golfmk1 goflcabriolet vw efi megasquirt ecu
categories: cars cabby
image: /cabby/megasquirt/megasquirt-1.jpg
---
The silly journey to put EFI on a 100HP car.

**Quick links.**
TLDR: here's the wiring diagram and parts list.

- [Golf MK1 MS2 Wiring Diagram](https://drive.google.com/file/d/1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5/view?usp=sharing)
- [Parts list shortcut](https://www.sudoyashi.com/megasquirt2#bulkhead-parts-list)

## Introduction

![img](https://www.megamanual.com/ms2/v3components.gif)

The cab has overheated. The cab has caught on fire. And these things made me very sad. So, In the pursuit of not being sad and having to worry about breaking down on a car cruise, the goal is to make this car reliable. Like actually, seriously, for real this time. I want to save this car because I still think it's the coolest car I've ever owned and because I want to prove to myself that I can do it.

The Golf MK1 came with mechanical fuel injection that was reliable until it wasn't. When it failed me back in 2021, the cost to fix the parts ($700) was too much to justify a fix to an already archaic system, so I used bike carburetors as a cheap ITB setup. It worked for a couple of years until a fuel bowl gasket failure caused a small fire. It ruined the carbs and part of the engine and at this point, it seemed like a good time to swap it! Carburetors are inefficent and they leave much to be desired in tuning and control. By changing the system from carbs to electronic fuel injection (EFI) and a standalone ECU, this will solve many of the carbs' issues, but with it comes new challenges to complete the setup. Let's save this car one more time.

I'm using the Megasquirt 2 DIY kit on the v3.0 PCB and will not be using the following features:

- Anything related to Idle Air Control, the ITBS come from a 2005 Honda CBR 600RR that uses a wax idle enrichment system that using coolant routed with coolant instead of an IAC
- MS2 "CAN" bus, supposedly it's not good or not real CAN BUS? CAN BUS will be set for another build as I still find CAN BUS very interesting.

This is the Cabby's EFI conversion project I've worked on for the last three month. Let's dive into the ECU and wiring.

## What is a MegaSquirt ECU? The ultimate DIY ECU

A car's ECU is the computer that tells it when to spark and when to squirt fuel based on various data inputs from the engine and environment. It's not magic, it's science. Specifically, the MegaSquirt (MS) ECU is a cheap, DIY alternative to other aftermarket ECUs to make standalone setups more accessible. For about $650, with a wiring harness and test kit, I got my ECU setup ready to go in a couple days. In the nature of DIY, if you don't know what you are doing, like me, there are A LOT of "ifs" and situational aspects in the MegaSquirt setup, and it can take a lot of work to figure out what you want to do. But with time and determination, you can work through the MS ECU.

Below is the original diagram provided by MegaSquirt. There are several versions of this diagram, depending on the version and generation of MS, so this may be different than the ones you could have seen before. The diagram illustrates what the ECU will read (inputs) and what it will control (outputs). With this control on inputs and outputs (I/O), we can tune the engine to behave how we want it to.

![img](https://www.megamanual.com/ms2/V3_ext_wire.gif)

Again, the ECU controls spark and fuel and does it by reading sensors on the car, like air temperature, coolant temperature, and engine speed. The data read by the ECU will read off a table of values and spit out some value to spray a certain amount of fuel and spark at a specific time. Based on a table of values, referred to as a fuel map, the ECU dynamically adjusts to the car and environment on how to modulate fuel and spark.

The ECU has a DB37 connector with 37 possible pins to give and retrieve instructions. I'll refer to the connector as the DB37. After many days of studying, this is the final harness for the Golf 2.0 ABA swap.

### Wire Harness Terminals DB-37 Connector Megasquirt II V3.0

![Wire Harness diagram](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-wiringdiagram.jpg)

View the diagram online [here](https://drive.google.com/file/d/1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5/view?usp=sharing) or visit [https://drive.google.com/file/d/1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5/view?usp=sharing](https://drive.google.com/file/d/1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5/view?usp=sharing).

This table references the terminals for the DB37 connector on the MegaSquirt 2 for a Golf ABA 2.0L engine using the following sensors. More info can be found in the [Sensors](https://www.sudoyashi.com/megasquirt2#sensors) section.

- MS2 On-board MAP sensor to manifold
- GM Intake Air Temperature sensor
- ABA Engine Coolant Temperature sensor
- Honda CBR 600RR throttle position sensor
- AEM Wideband X-Series O2 Sensor
- ABA VR Sensor

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

A bulkhead connector! I've wanted to do a bulkhead because it was what all the racecars had. It looks sick, and as far as reliability and durability are concerned, provides a solid bang for your buck. I was even more excited to learn that it would cost me less than $150 in parts. Wiring and putting together connectors is easy, but the hard part is parts availability and planning. I already have a decent amount of electrical tools and supplies, so this was a decent

It's a challenge in planning and wiring that I wanted to take to prepare myself for future wiring jobs. Crimping the MS2 harness directly to my components would be simpler, but a bulkhead connector would make it easier to service in the long run. Automotive wiring is a challenge for most people, and if I can show others that putting in the time and work will pay dividends in the build's reliability, consistency, and durability. Mapping the diagram forces me to consider every wire going into my car and makes me understand what I'm doing.

Wiring is a frustrating process as a DIYer, but future Josh will thank current Josh multiple times over.

I plan on using the Deutsch HDP connector. The parts list and connections are at the end of this section. Let's simplify the Deutsch connector world, as I'll list the exact part numbers I used in this build, what they do, and how to plan your build.

### Bulkhead firewall (plug) pinout

![Bulkhead pinout](https://www.sudoyashi.com/assets/img/cabby/megasquirt/wiring-bulkhead.jpg)

The plan is to take the wires from the MS2 harness and put it into the bulkhead connector. Since we know how many wires we want to use, I decided on the 29-pin connector. Suppose you need more pins and plan to include wiring for other components, factor that into your new connector. The table below shows the pins I'm using and what function from the MS2 or secondary fusebox it will provide. Find out what wire you want and if you plan to use wire splices.

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

![HDP Pinout 1](https://www.sudoyashi.com/assets/img/cabby/megasquirt/wiring-hdp29pinout-1.jpg)

Let's look into the Deutsch bulkhead connector. Do you know about the different materials and wire ranges between terminals? Here are four things to consider when choosing your connectors:

1. What size pin or socket?
   - You need both the pin and the socket. This creates the wire connection, and the type of pin or socket depends on the connector you have. Refer to the specification ([Deutsch stamped contacts](https://www.te.com/commerce/DocumentDelivery/DDEController?Action=showdoc&DocId=Specification+Or+Standard%7F108-151000%7FG%7Fpdf%7FEnglish%7FENG_SS_108-151000_G.pdf%7F1060-12-0222)) on what contact size you need. There are two types of terminals: stamped and solid. Stamped ones are cheap. Solid contacts are a pricy but durable option.
2. What size AWG are you using?
   - Now, the Deutsch contact size is NOT equal to the exact AWG size. You will see size 12, 16, and 20 contacts, but they come in various AWGs, so there is some flexibility in the wire that you can use. Because of this flexibility, price and availability come into play. You need to know what size wires you are using. In my case, I am using AWG 12, AWG 18, and AWG 20. AWG 12 is for high-power applications like the main relay and fans, while AWG 18-20 is for low-power applications like the ECU, injectors, and sensors.
3. What material?
   - There are multiple to choose from. Consider Gold (Au), Nickel (Ni), Tin (Sn), and Silver (Ag). Let's focus on the most common ones, Gold and Tin. According to this [Molex article](https://www.molex.com/en-us/blog/gold-or-tin-vs-gold-and-tin), essentially, gold connectors are more durable than tin, maintain a durable connection over time and never mix the types of connectors while tin connectors are cheaper, do the job, but may not survive many mating cycles. **Tldr; buy what's available and never don't mix mating materials. Tin is cheap. Gold is highly reliable.** Some connectors may be made of both (AU/SN).
   - Make sure that the pins and sockets are of the same materials when buying your parts. There are gold (Au), tin (Sn), nickel (Ni), and silver (Ag)
4. Is it available to buy?
   Availability is the unspoken bane of car people. The parts exist, but your job is to find out who sells them and who has them for the cheapest price. **Tl;dr: If a kit exists, buy the kit.** Hunting for the same part after the fact will ruin your future days.

What does a budget look like for some parts?

Consider that sometimes you can't buy these parts individually and may need to be in bulk; prices decrease commensurate with bulk and material choice. Cheaper options include tin or nickel options and are usually stamped contacts. This is good enough. You can find that some kits typically have stamped contacts.

**Stamped contacts are cheaper**

| Size | Socket (1062) | Pin (1060) | AWG | Material (XX) | PN | Qty | $ |
| ---- | ------ | ---- | ------------ | -------- | ---- | ------------- | ------------- |
| 12   | X      |      | 12           | Ni/Sn | 1062-12-0166 | 4 | $1 |
| 12   |        | X    | 12           | Ni/Sn | 1060-12-0166 | 4 | $ |
| 16   | X      |      | 18-20        | Sn/Sn | 1062-16-0677 | 19 | $0.69 |
| 16   |        | X    | 18-20        | Ni/Sn  | 1060-16-0622 | 19 | $0.55 |
| 20   | X      |      | 18-20        | Sn            | 1062-20-0377 | 6 | $1.04 |
| 20   |        | X    | 18-20        | Sn   | 1060-20-0177 | 6 | $0.45 |

The premium option is usually solid contacts with gold, which would run me at least $106.99. Sometimes, you can only buy some parts in bulk of 1000 or so, so this does not include shipping, bulk costs, and overhead (mistakes). You can see why materials matter now, lol.

**Solid contacts get expensive real quick**

| Size | Socket (0462) | Pin (0460) | Expected AWG | Material (XX) | Part #        | Qty  | $      |
| ---- | ------------- | ---------- | ------------ | ------------- | ------------- | ---- | ------ |
| 12   | X             |            | 12           | Au            | 0462-210-1231 | 4    | $4.23  |
| 12   |               | X          | 12           | Au            | 0460-220-1231 | 4    | $2.56  |
| 16   | X             |            | 18-20        | PD/Ni/Au      | 0462-004-1631 | 19   | $2.04  |
| 16   |               | X          | 18-20        | PD/Ni/Au      | 0460-002-1631 | 19   | $1.47  |
| 20   | X             |            | 18-20        | Au            | 0462-201-2031 | 6    | $1.16  |
| 20   |               | X          | 18-20        | Au            | 0460-202-2031 | 6    | $1.030 |

XX / Tin(Sn)=309,Gold(Au)=31,Nickel(Ni)=90 or 141

#### Splicing wires with CMA

Bare-metal wire splices were introduced to me by this [article](https://www.hpacademy.com/blog/how-to-splice-practical-splicing-demonstration/) from High Performance Academy. There are three open-barrel splices. These splices don't go by the usual AWG size but by the CMA or Circular Mil Area. Each wire has an estimated density of wires, giving us a particular area. Thinner wires have smaller CMA; thicker wires have larger CMA. This chart is a general reference for wire CMA. The chart below is an average I found on wire CMA, but it's close enough to club-spec. The advantage to these open-barrel types is that it doesn't include insulation and lets me see the wires physically spliced with a good connection without having to guess when putting them into a butt connector.

The issue I had with butt connectors was that I couldn't inspect the crimp after the fact, just pulling on it and hoping it stays. The connectors are slightly bulkier by comparison, but when you have to splice multiple wires in an area, it can look messy. Using the open-barrel splices lets us resolve both issues!

**Table of AWG and its relative CMA**

| Wire size (AWG) | CMA  |
| --------------- | ---- |
| 12              | 6530 |
| 14              | 4110 |
| 16              | 2580 |
| 18              | 1620 |
| 20              | 1020 |
| 22              | 642  |

As we splice more wires together, we want to add them up, and then we can choose a splice. Below are the available splices.

1. 1500 CMA and less of combined wire area: [TE 62759-1](https://www.te.com/usa-en/product-62759-1.html?q=62759-1&source=header) These are too small for me to use.
2. 1500 to 5000 CMA of combined wire area: TE [63130-2](https://www.te.com/usa-en/product-63130-2.html) Example: Two 20AWG wires or two 18AWG wires for ECU splicing.
3. 5000 to 10,000 CMA of combined wire area: TE [62357-1](https://www.te.com/usa-en/product-62357-1.html?q=62357-1&source=header) Example: One 14AWG wire to four 20AWG wires for fuel injector wires.

#### Bulkhead receptacle (the hot socket side)

[Part number: **HDP24**-24-29SE-L017](https://www.te.com/usa-en/product-HDP24-24-29SE-L017.html)
Housing for Female Terminals, Wire-to-Wire, 29 Position, Sealable, Black, Wire & Cable, Power & Signal, Panel Mount, Hybrid

The receptacle, the socket or female end of the connector, is where we'll connect the Megasquirt harness. This will be routed in the car and then mounted on the firewall. As a tip from TE Connectivity, use the socket side as the hot side (the one connected to the battery) so you don't shock yourself.

#### Bulkhead Plug (the cold pokey side)

[Part number: **HDP26**-24-29PE-L017](https://www.te.com/usa-en/product-HDP26-24-29PE-L017.html)
Housing for Male Terminals, Wire-to-Wire, 29 Position, Sealable, Black, Wire & Cable, Power & Signal, Panel Mount, -67 – 257 °F [-55 – 125 °C], Hybrid

The plug side will be mounted on the firewall.

#### Bulkhead Parts list

| Item                                  | Image                                                        | Description                     | Part Number        | Quantity | Subtotal |
| ------------------------------------- | ------------------------------------------------------------ | ------------------------------- | ------------------ | -------- | -------- |
| Deutsch socket                        | ![HDP24-24-29SE](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/5555/MFG_HDP24-24-29SE-L017.jpg) | Bulkhead plastic socket, 29-pin | HDP24-24-29SE-L017 | 1        |          |
| Deutsch plug,                         | ![HDP26-24-29PE](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/432/HDP26-24-29PE-L017.jpg) | Bulkhead plastic plug, 29-pin   | HDP26-24-29PE-L017 | 1        |          |
| Medium splice                         | ![Medium splice](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/805/63130-2.jpg) | Splices for my 18-20AWG         | 63130-2            | 100      | $8.52    |
| Large splice                          | ![Larger splice](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/632/62357-1.JPG) | Splices for my 14AWG            | 62357-1            | 100      | $11.25   |
| Size 12 Solid Receptacle pin (female) | ![12 pin](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2209/0460-204-12141.JPG) |                                 | (1060) 0460-XXX-12 |          |          |
| Size 12 Solid Plug pin (male)         | ![12 plug](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2236/0462-203-12141.jpg) |                                 | (1062) 0462-XXX-12 |          |          |
| Size 16 Solid Receptacle pin (female) | ![Size 16 receptacle](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2236/0462-203-12141.jpg) |                                 | (1060) 0460-XXX-16 |          |          |
| Size 16 Solid Plug pin (male)         | ![Size 16 plug](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/891/MFG_0460-202-16141.jpg) |                                 | (1062) 0462-XXX-16 |          |          |
| Size 20 Solid Receptacle pin (female) | ![Size 20 receptacle](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/799/0460-202-1631.jpg) | 16-20AWG, Gold, 0460-202-1631   | (1060) 0460-XXX-20 |          |          |
| Size 20 Solid Plug pin (male)         | ![Size 20 receptacle](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2282/0462-201-1631.JPG) | 16-20AWG, Gold, 0462-201-1631   | (1062) 0462-XXX-20 |          |          |
| Boot                                  | ![HD30 boot](https://www.te.com/content/dam/te-com/catalog/part/HD3/024/BTB/HD30-24BT-BK-t1.jpg/jcr:content/renditions/product-details.png?w=220) | Protective boot                 | HD30-24BT-BK       | 2        | $3.07    |
| Fuse holder with terminals            | ![DigiKey Fuseholder](https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/12/178.6152.0001.JPG) | Individual fuse holder          | DigiKey, F5194-ND  |          |          |
|                                       |                                                              |                                 |                    |          |          |

### Fuse and relay panel

![I like historic rally Volkswagens](https://collectingcars.imgix.net/011646/DSC-0317.jpeg?fit=clip&w=2000&auto=format,compress&cs=srgb&q=85)
The history of Golf Mk1/Mk2 and Polo rallies has always attracted me from my short time playing Dirt Rally 2.0. This is optional for most builds, but the Golf Mk1 factory wiring is tired, so I'm rewiring some things for reliability.

I couldn't find any fuse box I liked, so I'm making a custom-mounted one. Using individual fuse holders, [178.6152.0001](http://d.digikey.com/dc/mn-w0iJh4uEE_bUitNCuXmOASUNxIUHHNt2ANEnMXZ_AG_WhgOqCceIg4XKIDiTGU5IpRQEyR1t2V-Puo8lFuHzTPtYX6bfJEClHe62PNrZkDz-UHKBnux6j6Cr0l8ucounb-wISKZM8WacqeDnNHnfIeGZ5XxGzspQ5d8Uh5FxYEeWcK4B7IXHW6B16Ip7g/MDI4LVNYSy01MDcAAAGQlqDFwJPDtEc8eI9npTdI25sL8hjJ6yozBRIZwzLlO--b-HK9nX_LRC97znpBDoLWE892rl0=), I'll mount the fuse holders behind an ABS faceplate and mount the fuses like the ones above. I might update this to include more goodies (*AHEM on-board rally intercom*). 

That's enough wiring technicalities. Let's talk about the actual MegaSquirt now.

## MegaSquirt Sensors and you

We need your input!

Sensors give the ECU data so that it can do its job. If a sensor fails or malfunctions, the ECU will fail. Therefore, get the correct sensors and get the correct pinouts for your application. From my experience, you get what you pay for. While eBay and Alibaba sensors might come cheap, I wouldn't count on all of them giving you all of the correct instructions and wiring diagrams needed to do the work. Stick to the tried and true sensors like OEM or GM sensor.

Sensors usually work by changing their physical properties to produce some resistance. It can be a bi-metallic metal, plate, resistance, and so on. Not sure where to start, follow my table here and swap out your sensors accordingly.

| Sensor                           | MS Pin# | MegaSquirt Wire Color | Ground             | Connection                                                 | Existing or Buy       | Part Name or Number                                          | # Total wires | Wires                              |
| -------------------------------- | ------- | --------------------- | ------------------ | ---------------------------------------------------------- | --------------------- | ------------------------------------------------------------ | ------------- | ---------------------------------- |
| Manifold Absolute Pressure (MAP) | none    | none                  | none               | 1/8" vacuum line                                           | Existing, on-board MS | MPX4250                                                      | none          | none                               |
| Intake Air Temperature (IAT)     | 20      | Orange                | Black White DB37/7 | 3/8" NPT                                                   | Buy                   | [GM IAT ](https://www.diyautotune.com/product/gm-open-element-iat-sensor-with-pigtail/)25036751 | 2             | 5V, Signal                         |
| Engine Coolant Temperature (ECT) | 21      | Yellow                | Black White DB37/7 | Four wire: 2 are ground, 1 PCM (ECU IN), 1 to gauge sender | Existing              | VW 357 919 501A                                              | 4             | Ground, signal, Ground, temp gauge |
| Throttle Position (TPS)          | 22      | Light Blue            | Black White DB37/7 | Honda TPS                                                  | Buy (on ITBS)         | Honda 255478286857                                           | 3             | Ground, 5V, signal                 |
| Exhaust Gas Oxygen (O2 or EGO)   | 23      | Pink                  | ECU                | AEM 30-3427                                                | Existing              | AEM 30-0300                                                  | 6             | Multiple, splice only              |
| Ignition (VR)                    | 24      | White/Shield          | Black DB37/1       | ICM/6, replace existing Hall-Effect signal                 | Existing              | VW 021 907 319A                                              | 3             | Ground, Power, shield              |

### MS2 On-board MAP sensor to manifold

Part: [MPX4250 2.5 Bar MAP Sensor](https://www.diyautotune.com/product/mpx4250-2-5-bar-map-sensor/)

![MS MAP](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-map.jpg)

The onboard MAP sensor is connected with a 1/8" vacuum hose to any vacuum port on the intake manifold. Air pressure is one way for the ECU to see engine load. More pressure means more load. Turbo or supercharger? You're going to need this. NA depends on ITBS or not. You'll also have something like this for NA with a big plenum. For ITBS, you probably won't need it,but doesn't hurt to add.

Read more about how the sensor works here: [https://www.nxp.com/docs/en/data-sheet/MPX4250D.pdf](https://www.nxp.com/docs/en/data-sheet/MPX4250D.pdf). There is no pinout because it's already integrated on the ECU. If you're not using this type of sensor, follow your specific part diagram.

### GM Intake Air Temperature sensor

Part: [25036751](https://lowdoller-motorsports.com/products/intake-air-temp-sensor-iat-mat-25036751-25037225-25037034)



![MS IAT](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-iat.jpg)

The GM IAT is a universally accepted sensor that most aftermarket users will opt for if they don't already have an IAT sensor. The sensor only has two pins, sensor ground  and temperature signal. Place the sensor in the intake manifold or plenum, wherever your car gets air.

**Table: IAT pinout**

| IAT Sensor Pin       | MegaSquirt ECU Pin |
| -------------------- | ------------------ |
| 1 Signal ground      | Black White DB37/7 |
| 2 Temperature signal | Orange DB37/20     |

**Table: IAT expected temp resistance values**

| Intake Air Temperature Temperature | Ohms |
| ---------------------------------- | ---- |
| 48F                                | 7000 |
| 87F                                | 1930 |
| 146F                               | 560  |

### ABA Engine Coolant Temperature sensor
Part: Golf MK3 ECT black body yellow ring, 357 919 501A
Related part: Engine cooling fan switch (AC switch) 2-pin, 191 919 369A

[What does the Coolant Temp Sensor do?](https://www.clubgti.com/forums/index.php?threads/coolant-temp-sensor-what-does-it-do.86982/)
![Coolant Temperature Sensor calibration](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-clt.jpg)

Measure resistance between pins 1 and 3 at three different temperatures.
Pin 2 and 4 provide a temp readout to our gauge readout.

**Table: ECT pinout**

| ECT Sensor Pin                | MegaSquirt ECU Pin |
| ----------------------------- | ------------------ |
| 1 Black White Signal ground   | Black White DB37/7 |
| 2  Brown Blue Ground to block | --                 |
| 3 Blue Signal ECU             | Yellow DB37/21     |
| 4 Blue Dash gauge             | --                 |

**Table ECT expected temp resistance values**

| Temperature | Ohms |
| ----------- | ---- |
| 88F         | 1880 |
| 87F         | 1930 |
| 146F        | 560  |

### Honda CBR 600RR throttle position sensor
Part: HONDA 255478286857
Connector: Compatible with Sumitomo HX 040 6189-0887 receptacle

![Megasquirt TPS](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-tps.jpg)

The ECU supplies the sensor with voltage and ground and completes a circuit. The sensor houses a potentiometer, a resistor that changes with position. The TPS is mounted on the throttle linkage and moves with the throttle plates. As the throttle plate opens and closes, the position modulates the resistance and creates a specific voltage output (pin 3). The ECU reads the voltage and digitally tells the ECU the throttle is at the *x* position.

| TPS Sensor Pin  | MegaSquirt ECU Pin |
| --------------- | ------------------ |
| 1 TPS VREF      | Grey DB37/26       |
| 2 Sensor ground | Black White DB37/7 |
| 3 TPS Signal    | Blue DB37/22       |

### AEM Wideband X-Series O2 Sensor

Part: AEM 30-0300 X-Series Wideband UEGO Sensor, AEM 30-0300
Harness: AEM 30-3427
![Megasquirt O2](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-o2.jpg)

**Table: O2 pinout**

| O2 Sensor Pin     | MegaSquirt ECU Pin |
| ----------------- | ------------------ |
| 1 Signal ground   | Black White DB37/7 |
| 2 Ground to block | --                 |
| 3 Signal ECU      | Yellow DB37/21     |
| 4 Dash gauge      | --                 |


### Idle Air Control

In my case, idle will be handled by a warm-up enrichment and wax idle mechanical enrichment on the ITBS.

This means:
- No stepper IAC
- No PWM IAC
- Ignore the following:
  - IAC1A, DB37 pin 25
  - IAC1B, DB37 pin 27
  - IAC2A, DB37 ping 39
  - IAC2B, DB37 pin 31
  - S12C to JS9

### ABA VR Sensor and the Volkswagen Golf MK1 Ignition Control Module

Part: ABA VR sensor, 021 907 319A
Part: Golf MK1 ICM, VW part 191 905 351
Part: Ignition coil, VW part 1 220 522 016

Okay, so ignition is probably the most complicated and important section in any engine setup with an aftermarket ECU. Every setup is going to be slightly different, so use this as a guide to get started.

![MS2 VR Sensor](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-vr.jpg)
https://www.msextra.com/forums/viewtopic.php?t=38492

**Table: O2 pinout**

| VR Sensor Pin    | MegaSquirt ECU Pin |
| ----------------- | ------------------ |
| 1 Signal   | White DB37/24 |
| 2 Sensor ground | Black DB37/1   |
| 3 Shield | SHIELD DB37/2 |

#### How it works

We control the ABA by reading the incoming signal from the 60-2 trigger wheel and a VR sensor.

- The ABA uses 60-2 missing tooth wheel attached to the crank; this is the CRANK(VR) sensor to #24 TACH IN
- Single ignition coil; MEGA #36 IGN to the ICM, Ignition Control Module; refer to amplifiers
- The ignition signal (VR conditioned) Golf ICM gets actuated by ignition signal; spark event to distributor
- Distributor spark to spark plug

As the engine turns runs, the crankshaft turns, whereby the VR sensor sees crankshaft movement by reading the missing tooth wheel. The original configuration uses the hall effect with a trigger window in the distributor to mark the spark events. We aren't using the hall effect to control the spark, so we can disconnect this signal. Instead, with the MegaSquirt, we can use the input `ECU #24 TACH IN` from the VR sensor, which will condition the AC sine wave into a 5V DC square wave, output through `IGN signal (#36 IGN OUT)` to the ICM. The ICM will ground the ignition coil's primary winding, collapsing the magnetic field, producing the high voltage spark at the secondary winding to the distributor, and finally, sending the spark to our spark plug.

You got it?! If not, you can read on in-depth to learn more.

**Tuner Studio settings**
- Toothed Wheel:
  - Physical wheel: missing tooth on crank
  - Trigger Angle/Offset: always zero
  - Angle between main and return: n/a
  - Secondary wheel: none
  - Main wheel speed: Crank
  - 2nd trig every rotation of: n/a
  - GM HEI/DIS options: n/a
  - 420A/NGC alternate cam: n/a
  - Use cam signal if available: n/a
  - Ignition input capture:
  - Spark output
  - Number of coils: 1
  - Spark hardware in use
  - Cam input
  - Trigger wheel arrangement: single wheel with missing tooth
  - Trigger wheel teeth: 60
  - Missing teeth: 2
  - Tooth #1 angle: 
  - Main wheel speed: crankshaft
  - Second trigger active on: no dual wheel
  - Level for phase 1: no dual wheel
  - And every rotation of: no dual wheel
- Trigger
  - Trigger Angle: 82-90
  - 0 offset (for VR systems)
  - Trigger A: 5
  - Trigger return A: 14
  - Trigger B: 35
  - Trigger Return B:44
  - TDC at 14th tooth; 84 degrees
- Single coil and distributor
- **Ignition Input Capture** to 'Rising Edge' or other way if you wired the VR sensor opposite
- **Cranking Trigger** to 'Trigger Return'
- **Coil Charging Scheme** to 'Standard Coil Charging'
- **Spark Output** to 'Going Low (Normal)

#### In-depth on ignition wiring for the Bosch 137 module

[Ignition MegaSquirt](https://www.sudoyashi.com/assets/documents/ms2-ignition.pdf)

![ignition](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-ignition.jpg)

This is the theory behind the ignition system. I haven't officially tested it yet since the engine is still out of the car, but it will probably work for the 60-2 configuration.
We can control ignition by tapping into the existing ICM, and The Golf's Ignition Control Module (ICM) is as follows:

| Golf MK1 ICM Pin | Function                  |
| ---------------- | ------------------------- |
| 1                | ground for ignition coil  |
| 2                | ICM Ground                |
| 3                | Hall-Effect sensor ground |
| 4                | 12V for ignition coil     |
| 5                | Hall-Effect sensor 12V    |
| 6                | Hall-Effect signal        |
| 7                | --unused--                |

Since we don't depend on the HE sensor to get a signal, we swipe that pin and use the MegaSquirt ignition output. Again, MegaSquirt will condition the VR sin wave into the expected (Hall-effect) square wave.

| Hall-Effect (HE) and MK1 ICM Pin | Function  |      | Hall-Effect (HE) and ICM Pin | Function               |
| -------------------------------- | --------- | ---- | ---------------------------- | ---------------------- |
| HE/1                             | GND HE    |      | HE/1                         | GND HE                 |
| HE/2                             | Signal    |      | HE/2                         | **-**                  |
| HE/3                             | Power     |      | HE/3                         | Power HE               |
| ICM/1                            | GND Coil  |      | ICM/1                        | GND Coil               |
| ICM/2                            | GND ICM   |      | ICM/2                        | GND ICM                |
| ICM/3                            | GND HE    |      | ICM/3                        | GND HE                 |
| ICM/4                            | 12V Coil  |      | ICM/4                        | 12V Coil               |
| ICM/5                            | 12V HE    |      | ICM/5                        | 12V Hall-Effect Sensor |
| ICM/6                            | Signal HE |      | ICM/6                        | **DB37/36 IGN OUT**    |
| ICM/7                            |           |      | ICM/7                        | -                      |

The VW ICM should be an intelligent module and have dwell settings implemented, otherwise known as closed-loop control of dwell. The module will automatically adjust the dwell settings based on current. Auto-dwell is superior in that it won't break your shit, usually, and as a beginner in ECU tuning, this is great.

##### Some background info on ignition and dwell

[According to this article](https://web.archive.org/web/20170215145951/http://dtec.net.au/Tech%20Articles/Dwell%20Calibration.pdf), "dwell, or 'dwell time' in ignition systems refers to the period that the coil is on, i.e., that current is flowing through the primary winding and the magnetic field is building up in the coil." Well, what does THAT mean? *Dwell is the time it takes for a coil to produce the spark for a spark plug.* [If we shorten the dwell time too much](https://www.denso-am.eu/news/deneur21_08_ignition-coil-charge-up), the primary winding does not get enough charge-up time, and the spark is weak and shitty and your engine runs rough. If we extend the dwell too long, the primary winding charges too much and can cause overheating and frying the coil.

In addition, [dwell angle is the dwell time measured in degrees of rotation](https://docs.rs-online.com/fb75/0900766b800290e1.pdf), which refers to distributor setups where the rotor and contact points are closed, creating the spark event.

Learn this stuff, and you'll find the answer to how to set up your ignition system a lot easier. Let's continue with my setup.

The Bosch 137 module seems to be cross-listed with the VW part 191 905 351, which is what we have. The 137 is like the 139 module in that it's smart and dynamically sets the dwell settings for us. Without needing to set dwell, we don't have to worry too much about having a shitty spark or cooking our coil. So, we can use these settings in TunerStudio according to DIY AutoTune.

##### Ignition references

- [How to MegaSquirt your Water Cooled VW](https://www.diyautotune.com/support/tech/install/volkswagen/megasquirt-your-water-cooled/)
  - **Trigger offset** = 60 (this will vary, depending on the distributor orientation; see notes at the end of the article)
  - **Ignition Input Capture** to ‘Rising Edge’
  - **Cranking Trigger** to 'Trigger Return'
  - **Coil Charging Scheme** to 'Standard Coil Charging'
  - **Spark Output** to 'Going Low (Normal)

Read more:

- [MegaSquirt Manual MS2/V3.57](https://www.msextra.com/doc/pdf/MS2V357_Hardware-3.4.pdf)

  - *Bosch 0 2227 100 137 This is very similar to the 124, but the spark input signal is on pin 6.*

- [Using MSII to control the xxx 13modules](https://www.msextra.com/forums/viewtopic.php?t=8196)

  - *137 Triggers when it's grounded, i.e. from falling edge.*

- [Sample trigger settings for ABA 2.0](137 Triggers when it's grounded, ie. from falling edge.)

- [Another odd wheel](https://www.msextra.com/forums/viewtopic.php?t=16703)

  - "Yes, a Bosch 137 'smart dwell' module together with one Volvo coil (COP type)"

- [Bosch Ignition Modules components](https://www.pim-engineering.com/tiedostot/ignitionmodules.pdf)

  - Max primary current, 8-10A
  - Type of trigger, Hall effect

- [Dwell on TCi ignition, smart dwell](https://www.vwvortex.com/threads/ignition-control-modules.9363575/)

  - *However I think I located enough listings that I believe to be correct and came to the conclusion the ICM is in fact the same between the "knock box" and "non-knock" ignition systems for that period of VWs. Ha-ha, all of that to find out its the same.*

    *The current part number that I believe to be the correct ICM is: Bosch= 227.100.137, and VW= 191.905.351.B.*

- [Bosch Ign Module 0227 100 139](https://www.msextra.com/forums/viewtopic.php?t=18144)

  - *it is labeled 'Hall Efect Module". Pin 6 is the input, Pin 5 is a 12V supply for a hall sensor and pin 3 is signal ground for the hall sensor if you wire your hall sensor supply to the module instead of MS.*

- [How to tell if a Bosch ignition unit does dwell](https://www.msextra.com/forums/viewtopic.php?t=52201)

  - *As far as I'm away the built-in dwell modules were only used standalone directly connected to a dizzy. Any module that was controlled by an ECU I would expect to require dwell control in Megasquirt.*
    *Nothing wrong with keeping that module either - it should be perfectly matched to the coil.*
    *James*

| *Parameter*            | *Value*                                                      |
| ---------------------- | ------------------------------------------------------------ |
| Ignition Input Capture | **Rising Edge** Signal through optoisolator (U4)             |
| Cranking trigger       | **Trigger Rise**                                             |
| Coil Charging Scheme   | **Standard Coil Charge**                                     |
| Spark Output           | **Going High (Inverted)** for production MS-II('Going High (Inverted)' *for MicroSquirt*) |

## I swear this is going to work.

Making and writing my first wiring diagram was straightforward but time-consuming. WEEKS GONE. But, as I see it, the time spent researching and headaches on the computer is exponentially saved when troubleshooting anything in the car. With something written down and documented, it's clear as day where the potential problems are. That covers just about everything on the ECU side! I'll make changes retroactively as I run into issues during installation, but the theoretical portion is at least solved. In my next post, I'll be working out the fuel system.