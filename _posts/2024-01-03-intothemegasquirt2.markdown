---
layout: post
title: "Introducing the Megasquirt 2 plan"
author: "Joshua Domingo"
date:   2024-01-02 00:00:00 -1000
tags: cabby golfmk1 goflcabriolet vw efi megasquirt ecu
categories: cars cabby
image: /cabby/megasquirt/megasquirt-1.jpg
---
Converting the Cabby from the bike carbs to EFI was going to be simple, but one concern for me was the existing wiring for certain circuits. The fire damage left the headlights, starter, and engine harness damaged, so I'm redoing all of them and cleaning up the existing wiring. This is a look at the wiring diagram before I install it into the car, because of that, things might change once I actually install it.

This is part 1 of whatever amount of posts I'm making to put this car together. I'm hoping just for five parts, but "while I'm in there syndrome" might hit.

![Part 1 - ECU](https://www.sudoyashi.com/assets/img/cabby/megasquirt/part1-ecu.jpg)

## The Wiring Diagram
![Wiring diagram snip](https://www.sudoyashi.com/assets/img/cabby/megasquirt/mk1-aba-ms2-wiringdiagram.jpg)
This is MY diagram, some things may not apply to you, so be cautious on copying my diagram lol. However, this should apply to most MK1 JH->ABA swaps using a MegaSquirt.

The diagram won't fit on a single page... just so you know lol.
Live link:[Draw.io Golf MK1 ABA w/MegaSquirt 2 Wiring Diagram](https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=GolfMk1-original%20ignition.drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1PKhUPFUTe5xEFgeondNXi2kL-YfknbU5%26export%3Ddownload)

Lets' breakdown the diagram into its logical parts

1. Starter circuit
2. Ignition circuit
3. Fusebox
4. Headlights
5. MegaSquirt 2 ECU

## Starter Circuit
![Starter circuit](https://www.sudoyashi.com/assets/img/cabby/megasquirt/starter-circuit.jpg)

The starter circuit features two major changes compared to the original wiring setup:

1. Add 40A main relay
2. Add starter relay

The main relay is to give power to the fusebox that we will use for most of the newly installed engine management components. This includes the new fuel pump, ECU, lights, and cooling fan.

The starter relay is to provide a safer route for electricity to pass from our ignition system. This will protect the fragile ignition switch which is prone to failure. I've replaced them three times and it's not that fun lol. The starter relay is always powered from pin 30. By switching the ignition using our key, we complete the the circuit between 85 and 86. This triggers that "click" you hear from relays and provides pin 87 with the power from pin 30. This triggers the solenoid, which attempts to start the car. 

## Ignition circuit

![Ignition circuit](https://www.sudoyashi.com/assets/img/cabby/megasquirt/megasquirt-ignition.jpg)

The ignition circuit is based off the Bosch 124 module, adapted to the MK1 ICM, where the two modules are very similar. However, the pinout is slightly different as seen below. Pinout tested on a 1985 Volkswagen Golf Cabriolet.

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

The ignition circuit works like this:

1. The VR sensor on the engine block detects engine speed from the crank, this is read from the 60-2 crank trigger wheel.
2. The VR sensor sends a signal (DB37/24) to the MegaSquirt 2 (MS2) ECU, indicating the engine speed
3. The ECU sends out a signal (DB37/36) to the ignition control module (ICM/6).
4. The signal will trigger the ignition coil to ground at ICM/1, completing the trigger event and sends the high-current voltage to the distributor, which will send that to the spark plug.

## Fusebox

## Headlights

## MegaSquirt 2 ECU

The MS2 ECU wiring diagram was used as a starting point for my wiring setup. Some components are not used as a result seen in the modified diagram.

### Original diagram for MS2

![img](https://www.megamanual.com/ms2/V3_ext_wire.gif)

### Modified diagram for MS2 on ABA

The main changes I made in my setup are removing the idle wiring, the relay and fuses were routed into a fusebox instead, and the VR sensor wiring is slightly different than what is depicted above.

The DB37 pin #36 is an **output**, used to control an ignition module, or control a coil directly (if the high current ignition driver circuit is installed). It only needs to be connected if you are [controlling ignition timing and dwell](http://www.megamanual.com/ms2/Ignition.htm). The **ignition control signal** from MegaSquirt-II on DB37 pin#36 corresponds to the relay board pin **S5** of the 20 position terminal strip.

The final harness table looks like this:

| DB 37 Terminal | Color           | Function                                                     | IN/OUT  | Max Amps | Use YES | Use NO |
| -------------- | --------------- | ------------------------------------------------------------ | ------- | -------- | ------- | ------ |
| 1              | Black           | Crank sensor ground                                          | GND     | -        | YES     |        |
| 2              | -               | Crank sensor shield                                          | GND     | -        | YES     |        |
| 3              | Tan             | CAN High                                                     | (Comms) | -        |         | NO     |
| 4              | Tan/Red         | CAN Low                                                      | (Comms) | -        |         | NO     |
| 5              | Tan/Green       | -                                                            | -       | -        |         | NO     |
| 6              | Tan/Orange      | -                                                            | -       | -        |         | NO     |
| 7              | Black/White     | On-board sensor ground for, IAT, ECT, TPS                    | GND     | -        | YES     |        |
| 8              | -               | Spare GND                                                    | GND     | -        |         | NO     |
| 9              | -               | Spare GND                                                    | GND     | -        |         | NO     |
| 10             | -               | Spare GND                                                    | GND     | -        |         | NO     |
| 11             | -               | Spare GND                                                    | GND     | -        |         | NO     |
| 12             | -               | Spare GND                                                    | GND     | -        |         | NO     |
| 13             | -               | Spare GND                                                    | GND     | -        |         | NO     |
| 14             | -               | Spare GND                                                    | GND     | -        |         | NO     |
| 15             | Black           | Sensor ground, High current power ground                     | GND     | -        | YES     |        |
| 16             | Black           | Sensor ground, High current power ground                     | GND     | -        | YES     |        |
| 17             | Black           | Sensor ground, High current power ground                     | GND     | -        | YES     |        |
| 18             | Black           | Sensor ground, High current power ground                     | GND     | -        | YES     |        |
| 19             | Black           | Sensor ground, High current power ground                     | GND     | -        | YES     |        |
| 20             | Orange          | Intake air temperature (IAT)                                 | In      | -        | YES     |        |
| 21             | Yellow          | Coolant temperature sensor or Engine Coolant Temperature (ECT) | In      | -        | YES     |        |
| 22             | Light Blue      | Throttle position sensor (TPS)                               | In      | -        | YES     |        |
| 23             | Pink            | Exhaust Oxygen Sensor (EGO or O2)                            | In      | -        | YES     |        |
| 24             | White in Shield | TACH IN                                                      | In      | -        | YES     |        |
| 25             | Blue/White      | IAC1A                                                        | (Out)   | -        |         | NO     |
| 26             | Gray            | TPS 5V Supply                                                | Out     | 0.5A     | YES     |        |
| 27             | Blue/Red        | IAC1B                                                        | (Out)   | 0.1A     |         | NO     |
| 28             | Red             | 12V Supply                                                   | In      | 0.5A     | YES     |        |
| 29             | Green/White     | IAC2A                                                        | (Out)   | <1A      |         | NO     |
| 30             | Light green     | PWM Idle; wired for Fan Control                              | Out     | 0.1A     | YES     |        |
| 31             | Green/Red       | IAC2B                                                        | (Out)   | 0.5A     |         | NO     |
| 32             | Blue            | Injector Bank 1                                              | Out     | 7A       | YES     |        |
| 33             | Blue            | Injector Bank 1                                              | Out     | 7A       | YES     |        |
| 34             | Green           | Injector Bank 2                                              | Out     | 7A       | YES     |        |
| 35             | Green           | Injector Bank 2                                              | Out     | 7A       | YES     |        |
| 36             | Brown           | Ignition signal out                                          | (Out)   | 7A       | YES     |        |
| 37             | Violet          | Fuel pump relay output                                       | Out     | 0.1A     | YES     |        |

### Sensors

| #    | Sensor                                  | ECU Pin IN               | Wire Color                  | Ground | Description                                                  | Existing or Buy    | Part Name or Number                                          | # Total wires | Wires                              |
| ---- | --------------------------------------- | ------------------------ | --------------------------- | ------ | ------------------------------------------------------------ | ------------------ | ------------------------------------------------------------ | ------------- | ---------------------------------- |
| 1    | Crank Position Sensor                   | 1, 2, 24                 | Black, silver shield, white | ECU    | Crank sensor ground, crank sensor shield, 'Crank' input (VR or HALL) |                    | 037906433A                                                   | 3             |                                    |
| 2    | Manifold Absolute Pressure (MAP) Sensor | On-board Vacuum line     | Vacuum line                 | -      | Measure air pressure in intake manifold                      | Existing (MSII)    |                                                              | -             | -                                  |
| 3    | Intake Air Temperature                  | 20                       | Orange                      | ECU    | 3/8" NPT                                                     | Buy                | [GM IAT](https://www.diyautotune.com/product/gm-open-element-iat-sensor-with-pigtail/) 25036751 | 2             | 5V, Signal                         |
| 4    | Engine Coolant Temperature              | 21                       | Yellow                      | ECU    | Four wire: 2 are ground, 1 PCM (ECU IN), 1 to gauge sender   | Existing           | 357919369E, 4-pin                                            | 4             | Ground, signal, Ground, temp gauge |
| 5    | Throttle Position                       | 22                       | Light Blue                  | ECU    | Honda TPS                                                    | Existing (on ITBS) | Honda OEM TPS, 255478286857                                  | 3             | Ground, 5V, signal                 |
| 6    | Exhaust Gas Oxygen                      | 23                       | Pink                        | ECU    |                                                              | Existing           | AEM 30-0300 X-Series Wideband UEGO Sensor                    | 6             | Multiple, splice only              |
| 7    | Ignition (trigger VR Sensor)            | 36                       | Brown                       | -      | Output to ignition coil via ICM                              | Existing           |                                                              | 1             | Ground, 5V, signal                 |
| 8    | Knock                                   | cannot wire at this time | cannot wire at this time    | Block  | cannot wire at this time                                     | Existing           | cannot wire at this time                                     |               |                                    |

#### 1. Crank position sensor

We will be using the ABA's stock crank position sensor, this is referred to as the engine speed sensor in the Bentley manual. In the MegaSquirt manual, we are referencing 5.2.10 and section 6, combining the VR sensor with the ignition coil.

#### 2. MAP Sensor

The on-board MS2 MAP sensor will be connected to our intake manifold with a 1/8" vacuum hose.

#### 3. Intake Air Calibration for GM IAT

There are two wires for the IAT, ground and signal. The intake temperature is given to the ECU as some value generated from the sensor's thermistor, a variable resistor. As the temperature changes, the sensor mechanically reacts and creates a certain resistance. The ECU will read that resistance from the signal wire, convert that resistance, and assign a temperature value. 

Lower temperatures, higher resistance. Higher temperatures, lower resistance. Note that this is probably a non-linear function.

We ground this wire to the ECU, if we ground to the body or battery, the voltage drop may affect our reading. Grounding to the ECU stabilizes the sensor reading. This will apply to all sensors.

##### Calibrating the IAT

Calibrate the IAT using known ambient air temperature values and measure the resistance across the two pins. Using a heat gun, heat the sensor, and record the resistance with a multimeter.

In our case, we're using the GM IAT sensor calibrated with the following table of values:

**GM Intake Air Temperature (IAT) Sensor OE# 25036751 Calibration Values**

| Temperature   | Ohms |
| ------------- | ---- |
| 48 degrees F  | 7000 |
| 87 degrees F  | 1930 |
| 146 degrees F | 560  |

#### 4. Engine Coolant Temperature Sensor

Similar to the IAT, the Engine Coolant Temperature will change its resistance according to the physical change in temperature across the sensor. This signal is sent to the ECU, which will be converted to a real number.

Lower temperatures, higher resistance. Higher temperatures, lower resistance. Note that this is probably a non-linear function.

We ground this wire to the ECU, if we ground to the body or battery, the voltage drop may affect our reading. Grounding to the ECU stabilizes the sensor reading. This will apply to all sensors.

##### Calibrating the Coolant Temperature Sensor

Calibrate the Engine Coolant Temperature (ECT) using known ambient water temperature values and measure the resistance across the two pins. Stick the sensor in some hot water and record the temperature and resistance across the two pins.

In our case, the Bentley manual gave us the following table of temperature ranges.

![Bentley temperature]()

The following table are the measured values from real testing. 

| Temperature | Actual Resistance (ohms) | Expected Resistance (ohms) |
| ----------- | ------------------------ | -------------------------- |
| 48F         | 7000                     | 7000 ()                    |
| 87F         | 1930                     | 1930 ()                    |
| 146F        | 560                      | 560 ()                     |

#### 5. TPS Sensor

The TPS generates a resistance value based on the position of the throttle. As the position changes, a variable resistor in the sensor moves and generates a resistance. The sensor needs a power supply, sensor ground, and a signal wire connected to work properly.

#### 6. Exhaust Gas (O2) Sensor

We are using the AEM 30-0300 X-Series Wideband UEGO Sensor. I'll still have the AFR gauge installed so some wires will be spliced to add the inputs for the MS2.

#### 7.  Ignition

See above on the ignition circuit

## Conclusion

Laying out the wiring diagram was pretty meticulous but not impossible. I don't think this is very beginner-friendly and having the experience of wiring relays and actually splicing and crimping terminals will help with this portion of the plan.