CNC Router
----------

Budget
~~~~~~

Although I'm pretty comfortable financially, I don't want my electronics
hobby to impact my family's lifestyle so I decided to try to limit my CNC
budget to $500.00 I received from various family for Christmas this year.

I can go over this if necessary, but it makes a pretty good starting point.

Research
~~~~~~~~

Since I know nothing about CNC, I was pretty much in the dark about what
to look for. I had read articles about things like ShapeOko which was a kit
that sold for $175.00 a few years ago if you were lucky enough to be able
to get your hands on one so I started there, but soon found that the
original ShapeOko is a thing of a short and by-gone era. In fact none of
the links_ from any of the original articles_ I had read even worked.

.. _links: http://www.shapeoko.com/purchase

.. _articles: http://makezine.com/2012/03/16/shapeoko-the-300-cnc-kit/

ShapeOko is apparently now called carbide3d_ and their stuff starts at around
$1099.00 now. *Way* out of my budget!

.. _carbide3d: http://carbide3d.com/shapeoko/

I began surfing Amazon_ and Ebay_ looking at various models of CNC routers and
realized that lots of little Chinese outfits were building a number of small
units for around my price point. One could even get 4-axis machines for not
much more!

.. _Amazon: http://amazon.com

.. _Ebay: http://ebay.com

Unfortunately, I started this documentation project about a month after getting
started and I did not record any of my research, so I'll just
`cut to Hecuba`__:

__ https://en.wikipedia.org/wiki/Cut_to_the_chase

- One should choose a controller with a parallel port interface. it is widely
  accepted in the hobby CNC community that the USB interface does not provide
  accurate enough timing.

- Mach3_ and LinuxCNC_ are the two most popular pieces of software used to
  drive a cnc machine. Mach 3 is a Windows application while LinuxCNC is
  an entire Linux distribution. The primary role of either of these pieces of
  software is to convert "G-code" into the actual control pulses that drive
  the stepper motors on the CNC machine.

.. _Mach3: http://www.machsupport.com/shop/mach3/

.. _LinuxCNC: http://linuxcnc.org
  
- Mach3 is a Windows program that is by far the most popular tool but is
  not open source and costs $175.00.  All of these cheap, Chinese routers
  claim to come with a licensed copy of Mach 3, but I'm not sure I believe it.
  How could they provide the machine so inexpensively and also provide a
  $175.00 worth of software? My guess is that they provide the demonstration
  version.
  
- Mach3 can make use of an external motion controller, which, if
  I understand correctly is an external micro-controller that converts G-code
  into control pulses. In this configuration, Mach3 would act as a handy
  interface tool, but wouldn't be doing any of the heavy lifting. Presumably,
  usb would be a perfectly adequate interface in this case since the timing
  would be done by the micro-controller. There seem to be a number of project
  that use Arduino_ and `Raspberry Pi`_ as micro-controllers.

.. _Arduino: https://www.arduino.cc/

.. _`Raspberry Pi`: https://www.raspberrypi.org/

- LinuxCNC is an entire Linux distribution, entirely open source (GPLv2_),
  and not nearly as popular in the CNC community as Mach3. It will probably
  be my choice since I don't own a computer with Windows on it. LinuxCNC is
  adamant that LinuxCNC is the motion controller. They don't support usb at
  all!

.. _GPLv2: http://www.gnu.org/licenses/old-licenses/gpl-2.0.html

- Most of the CNC machines available for sale have a USB interface. I didn't
  know at the time whether this meant that they had a motion controller on
  board or what. (note: I have since learned that they have a USB/parallel
  converter with some CNC-specific features). I will have to be careful to
  order one with a Parallel port.

Gathering the Equipment
~~~~~~~~~~~~~~~~~~~~~~~

Eventually I settled on this_ machine which was a Chinese build, but already
in America which meant I could get it in a few days instead of a few weeks. It
is a brandless, 30cm x 20cm x 50mm (11" x 8" x 2") 3-axis machine

.. _this: http://www.ebay.com/itm/132045117295?_trksid=p2057872.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT

.. image:: images/cnc-machine.png

The astute observer will note that the linked description is of a USB machine.
And indeed, that is what they sent me! I which I had a screenshot of the
original description, because I swear to God it was for a parallel port
machine. It even had a series of photographs showing how to tell you if your
computer was equipped with a parallel port and several separate warning to
be sure you understood that this thing would not work with USB!

I sent the seller the message shown below:

.. image:: images/msg-to-seller1.png

Since the seller is in China, I had at least a day to wait for a response, so
in the meantime I looked into what I could do about this problem myself.

The controller unit has what appears to be an anti-tampering sticker on it,

.. image:: images/sticker.jpg

so I don't want to open it up and risk losing my warranty.
:download:`By peering through the vent openings in the side
<images/vent-peep.mov>`, I can make out that the USB card is red with
green terminal blocks along the left and back edges and a 10-pin header along
the right edge.

.. image:: images/vent-peep.jpg


A search with Google images (and a *lot* of scrolling) brought
me to the card_ shown below.

.. _card: https://www.aliexpress.com/item/Free-shipping-CNC-MACH3-USB-4-Axis-100KHz-USB-CNC-Smooth-Stepper-Motion-Controller-card-breakout/32704620352.html?spm=2114.01010208.3.22.3YCsJn&ws_ab_test=searchweb0_0,searchweb201602_3_10065_10068_10000009_10084_10083_10080_10082_10081_10060_10062_10056_10055_503_10054_10059_10099_10078_501_10079_426_10103_10073_10102_10096_10052_10053_10050_10107_10051_10106,searchweb201603_2,afswitch_5&btsid=10818071-d18a-498f-a232-8224931290e0

.. image:: images/usb-controller-card.png

Somewhere, and don't ask, because I don't remmber where, I came across a
description of parallel port pins to CNC usage.  I have combined that with
standard parallel port pinout_ information to create the following table:

.. _pintout: http://www.jspayne.com/io/schematics.html

+------+------------------------------+---------------+-----------+
| Port | Description                  | Printer Usage | Direction |
+------+------------------------------+---------------+-----------+
| P1   | ?                            | STROBE        | Out *     |
+------+------------------------------+---------------+-----------+
| P2   | X pulse                      | DATA 0        | Out       |
+------+------------------------------+---------------+-----------+
| P3   | X direction                  | DATA 1        | Out       |
+------+------------------------------+---------------+-----------+
| P4   | Y pulse                      | DATA 2        | Out       |
+------+------------------------------+---------------+-----------+
| P5   | Y direction                  | DATA 3        | Out       |
+------+------------------------------+---------------+-----------+
| P6   | Z pulse                      | DATA 4        | Out       |
+------+------------------------------+---------------+-----------+
| P7   | Z direction                  | DATA 5        | Out       |
+------+------------------------------+---------------+-----------+
| P8   | A Pulse                      | DATA 6        | Out       |
+------+------------------------------+---------------+-----------+
| P9   | A direction                  | DATA 7        | Out       |
+------+------------------------------+---------------+-----------+
| P10  | IN1 connected emergency stop | ACK           | In  *     |
+------+------------------------------+---------------+-----------+
| P11  | IN2 standby                  | BUSY          | In        |
+------+------------------------------+---------------+-----------+
| P12  | IN3 spare                    | PAPER END     | In        |
+------+------------------------------+---------------+-----------+
| P13  | IN4 3-axis limit             | SELECT        | In        |
+------+------------------------------+---------------+-----------+
| P14  | relay port                   | AUTOFEED      | Out *     |
+------+------------------------------+---------------+-----------+
| P15  | IN5 spare                    | ERROR         | In  *     |
+------+------------------------------+---------------+-----------+
| P16  | relay port                   | INIT PRNTR    | Out *     |
+------+------------------------------+---------------+-----------+
| P17  | relay port                   | SELECT IN     | Out       |
+------+------------------------------+---------------+-----------+
| P18 - P25 are Ground                                            |
+------+------------------------------+---------------+-----------+
| * indicates an active low signal                                |
+------+------------------------------+---------------+-----------+

.. image:: images/db25-pinout.png

I reasoned that the usb controller board was really just a parallel port
adapter with some opto-isolator chips. All I needed was a parallel board
with similar features so I ordered this_ one from ebay. Unfortunately, it
would take at least 3 weeks to arrive since it was coming from China!

.. _this: http://www.ebay.com/itm/291620685428?_trksid=p2060353.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT

The next day, my CNC seller got back to me!

.. image: images/msg-from-seller1.png

Not very helpful. The main problem I had was having the wrong controller. I
tried again:

.. image: images/msg-to-seller2.png

And a day later:

.. image: images/msg-from-seller2.png

Ok. Now we're getting somewhere! Not only had I done the right thing by
ordering the parallel port board, but they were giving me permission to open
the controller box.

Inside the Controller Box
~~~~~~~~~~~~~~~~~~~~~~~~~

It would appear that I did, in fact, find the correct USB controller board with
google images.

.. image:: images/controller-board.jpg

More on the controller board later.

Power Supplies
++++++++++++++

There are two power supplies.

Upper Supply
............

The upper one is a variable power supply:

.. image:: images/upper-ps.jpg

+-------+-------+-----+-----+----+--------+--------+
|  V+   |  V+   | G   | G   | FG | L      | N      |
+-------+-------+-----+-----+----+--------+--------+
| 0-46V | 0-46V | Gnd | Gnd | ?  | 110V H | 110V N |
+-------+-------+-----+-----+----+--------+--------+

The voltage is controlled via an externally mounted 4.2K pot.

It powers the spindle and it's output terminals go directly to "Control Output"
pins 35 (+) and 36 (gnd).

Lower Supply
............

The lower power supply is a +24V supply:

+--------+--------+----+-----+-----+------+------+
| L      | N      | FG | G   | G   | V+   | V+   |
+--------+--------+----+-----+-----+------+------+
| 110V H | 110V N | ?  | Gnd | Gnd | +24V | +24V |
+--------+--------+----+-----+-----+------+------+

This supply may also be variable as there is a small pot next to the power
rail.

.. image:: images/small-pot.jpg

The output terminals from this power supply are wired to three identical boards
labeled TX13130. More on these later, but basically these drive the motors and
are controlled by signals from the controller board. There is one of these
boards for each of the three axis of the CNC machine.

Driver Boards
+++++++++++++

The driver boards are labeled TX13130 and
each contains two 4N25 optocouplers and one EL817 photocoupler. On the back
side of each of these boards are an approx 1/2 square IC all of which are
thermally cemented to a single thick piece of alumninum which is server as a
heat sink. In addition there is another small chip back there. I was expecting
a simple H-bridge chip (which I learned about from an instructables_ article)
but this chip is more complicated.

.. _instructables: http://www.instructables.com/id/Controlling-a-Stepper-Motor-with-an-Arduino/

There are five inputs labeled EN, DIR, CLK, NG and +U. EN and NG are not
connected to anything. +U is connected to terminals labelled 5V on the
controller board while DIR and CLK are connected to xD and xP (where x is one
of X, Y, or Z) also on the controller board.

I must say, the Internet is failing me when it comes to learning about this
board. I did find a Reddit post_ which claims the board uses an A3977_
microstepping driver.

.. _post: https://www.reddit.com/r/hobbycnc/comments/4fah3l/so_i_have_a_cheap_3040_and_a_pile_of_parts_to/

.. _A3977: http://www.allegromicro.com/en/Products/Motor-Driver-And-Interface-ICs/Bipolar-Stepper-Motor-Drivers/A3977.aspx

For now I'm just going to have to hope that the people that made my controller
box understood how to use this board and match the wiring they did as best
I can using the chart above to translate xD and xP (x = X, Y, or Z) into ||
port pin numbers.

USB Controller Board
++++++++++++++++++++

Finally we circle back to the controller board. We've already learned a lot
about it.

.. image:: images/usb-controller.jpg

We understand the xD and xP (Direction and Pulse) connections.

There are a series of INx (x=1-4) and OUTx (x=1-4) terminals none of which are
connected to anything except IN1 is connected to the emergency stop button. The
other side of the button is connected to a terminal marked AVI-.

Another pair of terminals called COM+ and COM- are connected to the +24V and
GND terminals, respectively, of the 24V power supply. I don't know why those
are needed. The do not power the board as even with the box turned on the
+V terminals float. The board itself must be powered from the usb port.

When I plug in the USB port, a red led flashes on the board and the +V
terminals are now showing a steady 4.84V. Here is a chart of everything
connected on the board:

+------+-----------------------------------------------+
| Term | Connection                                    |
+------+-----------------------------------------------+
| COM+ | +24V                                          |
+------+-----------------------------------------------+
| COM- | GND of 24V PS (not connected to board ground) |
+------+-----------------------------------------------+
| IN1  | Emergency Stop Switch
+------+-----------------------------------------------+
| AVI- | Emergency Stop Switch                         |
+------+-----------------------------------------------+
| 5V   | +U on driver boards                           |
+------+-----------------------------------------------+
| xP   | CLK on driver boards                          |
+------+-----------------------------------------------+
| xD   | DIR on driver boards                          |
+------+-----------------------------------------------+

While I plan to replace this board, I have discovered via a post_ that one
can use this board with Mach3 using a dll called
:download:`RnRMotion.dll <RnRMotion.dll>`

.. _post: https://www.tapatalk.com/topic/11158-cnczone-com/326812-help-id-this-controller-in-my-chinese-3040

I plan to use LinuxCNC_ which is adamantly opposed to USB controller boards
on the grounds that the USB does not offer good enough timing control, which is
why I plan on replacing the board.

.. _LinuxCNC: http://linuxcnc.org/

Parallel Controller Board
~~~~~~~~~~~~~~~~~~~~~~~~~

I purchased a parallel breakout board_ from Ebay.

.. _board: http://www.ebay.com/itm/291620685428?_trksid=p2060353.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT

The board has three sets of terminals which are fairly self-explanatory with
some exceptions. I also found an image that helps with things.

.. image:: images/parallel-board-info.jpg

The board also contains a "USB PWM Spindle" circuit. I'm assuming tha tPWM

Right Terminal Block
++++++++++++++++++++

The left terminal block has terminals labelled IN1-IN5, GND, and 5V.

.. image:: images/right-terminal-block.jpg

Clearly, IN1 should be connected to the emergency stop switch but it is not obvious
what is the equivalent, on the new board, of AVI- on the USB board (the USB
board also has a terminal labelled AVI+). Using the printer pinout table
above, it is easy to see how these are connected. what isn't clear is whether
the board converts the active low signal ports to normal high signal or not.
I will have to do some testing to determine that.

Note that the 5V terminal is *not* powered by the usb connector. The image
describes it as 5V power output, but I know know from where it gets it's
power. From the 24V input maybe?

Left Terminal Block
+++++++++++++++++++

The left terminal block has terminals labelled in chinese characters followed
by 1, 2 or 3.

.. image:: images/left-terminal-block.jpg

There are three blocks with 1, three with 2, and three with 3. Using a
contininuity tester and by examining the traces it was easy to see that the
terminals work as follows:

+------+--------+-------+
| Left | Center | Right |
+------+--------+-------+
| NO   | C      | NC    |
+------+--------+-------+
| EC   | C      | EO    |
+------+--------+-------+
| NO = Normally Open    |
| NC = Normally Closed  |
| EO = Energized Open   |
| EC = Energized Closed |
+------+--------+-------+

This block also has a pair of terminals labeled 24V and GND. I am guessing
that power applied to this terminal is used to power the relays on the board.
One of these relays could be used to turn the spindle motor on and off. With
the current controller, that operation is performed manually.

Center Terminal Block
+++++++++++++++++++++

The center terminal block is self explanatory except for the two pairs of
terminals labeled in Chinese. These turn out to be GND and +5V as provided
by the USB port.

P1 - P9, P14, P16, and P17 are outputs as expected. Presumably, P14, P16,
and P17 also operate the relays if power is provided to the 24V terminal
on the left block. Also, it is again unclear whether terminals P14 and P16
operate in active low state, or if they are inverted to act like the data
outputs. Testing will be needed once I get a computer set up.

The 0-10V output is presumably the the USB PWM Spindle output. The image makes
it look like the USB board only provides power, but the name USB PWM Spindle
in the board description sounds like the USB port provides this. Alternately,
it might be driven by the pulse width applied to pin P1. This will also need
experimentation.

Computer
~~~~~~~~

I have an old Dell Pentium 4 computer with an onboard parallel port(!) and
Fedora Linux on it that my daughters used before I bought them laptops.
My plan is to install LinuxCNC on it, but first I need to save all of my
daughter's files off of it because the Lord knows they would never do a
backup.


Screw Pitch
+++++++++++

76 screw turns over 6 inches
