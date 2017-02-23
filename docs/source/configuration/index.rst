LinuxCNC
--------

For installation media, I chose an 8GB WINTEC filemate USB drive I had lying
around and then I downloaded the latest LinuxCNC ISO file_ to my MacBook. I
used good old "dd" to write the ISO to the USB drive.

*Before* plugging in the USB drive:

$ ls /dev/disk*
/dev/disk0   /dev/disk0s2 /dev/disk0s4 /dev/disk0s6
/dev/disk0s1 /dev/disk0s3 /dev/disk0s5 /dev/disk1

*After* plugging in the USB drive:

$ ls /dev/disk*
/dev/disk0   /dev/disk0s2 /dev/disk0s4 /dev/disk0s6 /dev/disk3
/dev/disk0s1 /dev/disk0s3 /dev/disk0s5 /dev/disk1   /dev/disk3s1

So my USB drive shows as /dev/disk3. Next I issued the following "dd" command.
*WARNING:* This command will erase whatever crap you have on your USB drive.
It won't warn you. It won't hold your hand. It will scrape your files off the
drive like they're dog crap on a shoe. YOU HAVE BEEN WARNED!

$ sudo dd if=~/Downloads/linuxcnc-2.7-wheezy.iso of=/dev/disk3

This same command will work on Linux or any other unix-like operating system
although the hard drive device names will be different. For example, modern
Linux kernels will refer to the drives as /dev/sda, /dev/sdb, etc. To get the
device name of your USB drive in linux, you can plug in the drive and then
type "dmesg" in a terminal. This will print a butt-load of information.
Near the bottom you will see the device assigned to the drive.

What's that you say? You are using a Windows computer? Well I'm sure Windows
has some wonderful crapware available for writing ISO files to a USB drive.
Use one of those. Actually, if you already have a Windows computer with a
parallel port and a couple hundred bucks lying around, maybe you should just
get Mach3_.

.. _Mach3: http://www.machsupport.com/shop/mach3/

Next I set my computer's BIOS to allow booting from it from USB.
Newer compouters have UEFI instead of BIOS which can be a pain,
but I recommend you get your hands on an older computer anyways because newer
computers also don't have built-in parallel ports, so then you have to buy a
parallel port card for it.

Some computers will let you press the F10 or F12 button to enter
a boot menu and you can choose to boot from your USB media that way without
messing with BIOS.

I booted my media to the Linux GRUB menu and choose graphical installation. I
am very sorry that I didn't take pictures along the way, but the installation
was very easy.  The only real decision I had to make was about hard drive
partitioning. I choose to use the entire drive and to use LVM. LVM, in case
you don't know, is Logical Volume Management. Installing with this now will
allow me to add another hard drive in the future and then extend my partition
across the drive and treat both drives as one single hard drive.

Once the installation process is done, the 



problem with pip installing flatcam
+++++++++++++++++++++++++++++++++++
MARKER_EXPR = originalTextFor(MARKER_EXPR())("marker")

line 59 in /usr/local/lib/python2.7/dist-packages/packaging-16.8-py2.7.egg/packaging/requirements.py

should be
MARKER_EXPR = originalTextFor(MARKER_EXPR(""))("marker")

then you can pip install --upgrade pip and everything is fixed.

Screw Pitch
+++++++++++

76 screw turns over 6 inches

