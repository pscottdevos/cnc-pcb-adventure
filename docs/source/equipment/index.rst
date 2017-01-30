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
so I don't want to open it up and risk losing my warranty. By peering through
the vent openings in the side, I can make out that the USB card is red with
green terminal blocks along the left and back edges and a 10-pin header along
the right edge. A search with Google images (and a *lot* of scrolling) brought
me to the card_ shown below.

.. _card: https://www.aliexpress.com/item/Free-shipping-CNC-MACH3-USB-4-Axis-100KHz-USB-CNC-Smooth-Stepper-Motion-Controller-card-breakout/32704620352.html?spm=2114.01010208.3.22.3YCsJn&ws_ab_test=searchweb0_0,searchweb201602_3_10065_10068_10000009_10084_10083_10080_10082_10081_10060_10062_10056_10055_503_10054_10059_10099_10078_501_10079_426_10103_10073_10102_10096_10052_10053_10050_10107_10051_10106,searchweb201603_2,afswitch_5&btsid=10818071-d18a-498f-a232-8224931290e0

.. image:: images/usb-controller-card.png

Somewhere, and don't ask, because I don't remmber where, I came accross the
following chart showing parallel port pinout assignments:

  Port / Description
 
  P2 / X pulse
 
  P3 / X direction
 
  P4 / Y pulse
 
  P5 / Y direction
 
  P6 / Z pulse
 
  P7 / Z direction
 
  P8 / A Pulse
 
  P9 / A direction
 
  P14 / relay port
 
  P16 / relay port
 
  P17 / relay port


  P10 / IN1 connected emergency stop

  P11 / IN2 standby

  P12 / IN3 spare

  P13 / IN4 3-axis limit

  P15 / IN5 spare

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
the controller box!

Inside the Controller Box
~~~~~~~~~~~~~~~~~~~~~~~~~

It would appear that I did, in fact, find the correct USB controller board with
google images.


