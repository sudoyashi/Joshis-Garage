---
layout: post
title:  "Dual round grille, new power steering linees and G13 coolant"
date:   2022-03-04 00:00:00 -1000
categories: lights
image: dualround.jpg
---

# Finally installing dual round headlights!

I've always lusted for the Euro style quad headlights because it's reminiscence to the classic four-light setup on E30s and classic Mercs. Like popup headlights to JDM cars, the dual round headlights on a Golf Mk1 is the Golf that I imagine in my head.

I picked this grill up from a buddy named Robert in Waipahu, Hawaii. It's weird to name these smaller towns in Hawaii like Waipahu, Kalihi, or Mililani in the form like they're their own city. On the island of O'ahu our true "city" by legal address is generally Honolulu; hence, it is Honolulu, Hawaii. Robert was a very knowledgeable guy that had the parts that I was looking for:
- Spare AC vents that came from a '91 Golf
- The dual round headlight grill from the same parts car

The practical reason I wanted the dual round lights was it could provide with more lighting during the night. These H4 lights aren't as bright as the modern day HID, but replacing these filament bulbs with LEDs would definitely change the look of the car that I think wouldn't look great. I've seen angel eyes and crosshairs on other builds, but those Golf Mk1s were a lot cleaner than mines, haha.

## Tools and Supplies

- Wire crimpers or soldering iron with flux-core solder
- Wire cutters
- Scissors
- Multimeter

- Wires, 12 AWG and 18 AWG
- Fabric, high-heat Tesa tap OR electrical tape OR liquid electric tape
- Wire crimp connectors
- Wire loom
- Vampire clips, t-taps, or splice taps. Whatever you call 'em.

## Dual round installation

There's a couple ways that we could go around this. I went to do my own harness rather than tapping into the current wiring.

I believe the original setup utilized the inner round lights to work in tandem with the high beams. On the low beams, the lights would be off. On the high beams, the lights would be on. This would mean that it would share a common ground and receive power from the high beam positive wire.

In my setup, I separated them to have more control. Also because I'm lazy. I had originally installed lights on my bumper with a separate harness, but they ended up looking terrible. I removed those lights, but left the wiring harness. Now, I can use those wires to simply plug into the lights individually without needing to use vampire clips, t-taps, or whatever you want to call the lazy-man's splice.

### Relay basics and overview of the circuit
The wiring harness is protected by a relay and 10A fuse. In this diagram we have the 4 main terminals of the relay:
- 87 - Switched power to the lights
- 86 - Main ground
- 85 - Switch power relay circuit
- 30 - Main power

What is a relay?

A relay is basically two switches in one.
- First, we have our low power switch: terminal 85 and 86. These two are powered once connected, just like a lightbulb. It grounds to the body and is powered by turning on the car.
- Second, our high power switch: terminal 30 and 87. Terminal 30 is where the 12V battery power comes in and terminal 87 is our *thing* we want to power.
- When we connect terminals 85 and 86 by pressing a button, this low-current circuit then allows terminal 30 and 87 to connect and power our *thing*.

But why do we need two circuits if we only have one item? Protecting the circuit and decreasing the load. There undoubtedly many little circuits in a modern car, and if you're running ALL your circuits from battery power all the time, you'll wear and drain your battery significantly. It's not efficient. By using lighter, low-voltage circuits, we can control when we want to use the higher voltage *things*!

### Hooking up the wires, it's... mostly straightforward

From ground to power, complete the circuit.

DRAW yourself a diagram if you're planning on doing something similar and see where power goes, from ground to positive, understanding where and when power flows through. To start out mapping, start from the end. Where are your lights? Where are the wires going? How many switches do I need?

Most of our bonehead aftermarket solutions tap into a circuit that turns on from Ignition On. Finding ignition on what some people get intimidated about. The first time I heard that, I had no idea what I was looking for.

#### Part 1/3 - Add your new toggle switch, the low power side

SPLICE into ignition on or use a FUSE TAP!

Splicing, more work.

Ignition on circuits are just that, the circuit gets power when you turn your car to the ON (not to the start) position. **In most cases, it's your gauges, switches, radio, or cigarette lighter!** The biggest giveaways are to figure out what is the general color for grounds for your car, then just don't choose those! For these older VWs, it's brown, for others it's probably black.

Once you find a circuit, you can use a multimeter for testing. Look at your suspect wire and find the metal terimnal it's connected to. Take your positive lead (red) and touch the metal. Take your negative lead (black) and touch a body ground. It should read 0V. When you're ready, turn on the car and repeat. If it reads 12V, it's an ignition on circuit! Nice. If it reads anything substantially less than 12V, it's probably ground or something else... You're goal is to determine what wires are power and ground.

A good wire to splice into has enough physical room around it and easy to splice in. You can us any way you want to splice: solder and splice or vampire clips.

Once you've confirmed your power source, tap into it and don't forget to cover it with tape or heat shrink. Run this tapped wired to your toggle switch. The other terminal will run towards the 85 of our relay. You may have a third wire for power to the indicator light on the switch, run another (+)wire to this to give it power for the light when headlights are on, again to find out which one that would be, look for something that turns on when your headlights are on, e.g. dash lights, radio lights, puddle lights.

Method 2: The easier way...

What always gets power you turn the car on? The fuse block!.
Your switch also needs to be connected to power! To do this, tap into the fuse-block

Good, 1/3 of wiring is done.

#### Part 2/3 - Routing to the new lights, the high power side

You should have your new wires from the cabin routed through the firewall, if not... go do that. Label the wires. Don't connect the wires to your relay yet.

Let's look at the main power and main ground of the relay.

On your relay, find terminal 30 and run a wire from terminal 30 to battery (+). This is the main power to the relay.
Then, run a wire from terminal 86 to the body, but do not connect it to your relya yet. Clean up the body ground with a wire brush and fasten it down. This is the main ground to the relay. Leave the main ground disconnected.

Lastly, terminal 87 will be run to your new headlights. We are splitting the wire in two, one wire to each highlight circuit. You can simply strip the wire down enough to wrap to wires around, then cover it with solder and electrical tape. Connect these to the positive terminal of the headlight.

From the headlights, run a wire from the negative terminal to the body. You can choose to combine the wire into one or make two holes in the chassis. It's cleaner if you can combine and tuck them away in the same place. But it's your shitbox, do what you like.

That's all the wires, so what's part 3/3?

#### Part 3/3 - Mounting, taping, and cleaning up wires

For good wiring practice, mounting your relay in a nice place, tape up your wires together with Tesa fabric tape and loom it together. Zip ties would be good to fasten things down along the bay. At this point, you may find loose crimps, bad wiring jobs, or may have acciendtally shocked yourself. When you're finally done, connect your toggle switch terminal 85, headlight power 87, confirm main power terminal 30, and lastly connnect your main ground terminal 86. If all goes well, you should have new working lights.  


It was confusing at first, but after walking through the diagram, and even testing it with a spare motorcycle battery, you can start to understand the process.




What wire? General rules of thumb, 12 AWG for boy power, 18 AWG for the rest. BUT, refer to a wiring chart on your choice of wire. Household Home Depot wire will work, but get some real copper at places like wirebarn.com.

### Installation, finally.
0. Double check your wiring diagram and loosely map your wires.
1. Remove the gril using a philips head screwdriver, or whatever fastener the person used before you. Be gentle with the plastic clips.
2. Install the new grill
3. Install the fog lights, inner lights, whatever you want to call them. If you're going the route of custom mounting points, you may use 5.25" lights to fit into the quad grill, you'll have to figure out a way to fasten it, though.
4. Install your wires. Work from the cabin to the engine bay, feeding your wires through the firewall.
5. Install your wires to positive and ground
6. Check your grounds and test. Clean grounds are the beginning and end of most electrical issues.
7.


Find my (very) periodic posts here. Or something.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
