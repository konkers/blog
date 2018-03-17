---
title: "Reboot the knes!"
date: 2018-03-16T14:41:07-07:00
tags: [ "verilog" ]
categories: [ "blog", "hardware" ]
series: [ "knes" ]
draft: false
---

So, long story (involving cross stitching, my 3 year old daughter, an a good
kind of crazy coworker short) I've been bitten by the retro gaming bug.  It's a
pretty deep hole to fall into.  In addition to setting up a veritable shrine to
nintendo in the TV room, I've inspired me to dust off my NES in an
FPGA project [knes](https://github.com/konkers/knes).  After quick look I
decided to basically start over.  Why?  I'm glad you asked.

Code Quality
------------
![I'm gonna build my own NES... with comments and unit tests.](./bender.jpg#center)

First lets get this out of the way.  I'm not a digital designer.  I don't even
play one on TV.  So when I took a look at the almost 10 year 
[old code](https://github.com/konkers/knes/tree/pre-reboot), I was horrified. 
At the time, I remember being frustrated by the design.  Looking at it now, 
I can't make sense of it.  There are very few comments describing the design
intent.  The few "unit tests" that did exist, just drove the modules and didn't
test the output.  The one diamond in the rough was the 
[6502 assembly tests](https://github.com/konkers/knes/tree/pre-reboot/6502/tests)
and [instruction set coverage analyzer](https://github.com/konkers/knes/tree/pre-reboot/6502/tests).
Those parts I'll keep.  At least in spirit.

New Shit's Come to Light Man!
-----------------------------
When I was working on knes, [Visual 6502](http://visual6502.org/) was just
getting started.  In the 9 years since. A lot more information about the
internals of the 6502 has been researched and published.  Also, while I was
aware of
[Beregnyei Balazs' Schematic](http://visual6502.org/wiki/index.php?title=Balazs%27_schematic_and_documents)
I was not aware of Donald F. Hanson's excellent [Block Diagram](http://visual6502.org/wiki/index.php?title=Hanson%27s_Block_Diagram).
That diagram gave me great insight into the actual architecture of the 6502

![Block Diagram Preview](./block-diagram-crop.png#center)

A New Hope
----------
Last weekend I started over, this time sticking to the architecture shown in the
Hanson diagram.  I'm trying to comment the code well as well as write good unit
tests for the blocks.  Here's the [state of the code](https://github.com/konkers/knes/tree/c438a224e03b44d4256f3361a4f0aa6ef28d0a52/6502)
at the time of writing this post.

I've also started vectorizing the Hanson diagram and annotating it with the
net names I'm using in the verilog design.
[Check out the current progress](https://github.com/konkers/knes/blob/760cb795e9a7cefa8eab6ffc86e7d137f7570a36/docs/block-diagram.pdf)
(also at the time of writing this post).  Non-gray block are block that are 
implemented.

To Infinity and Beyond
----------------------
Let's see where this takes me!  I'm pretty stoked.