+++
title = "The project comes to an end :: EV Moped Conversion pt. 4"
date = 2019-10-14T18:23:32-07:00
author = "Audrey Xie"
tags = ["EV", "moped"]
showFullContent = false
draft = false
+++

> On a cycle the frame is gone. You're completely in contact with it all. You're in the scene, not just watching it anymore, and the sense of presence is overwhelming. (Robert Pirsig, *Zen and the Art of Motorcycle Maintenance*)

<!--more-->

It’s been quite a while since the last moped update. Partly because of my own tendency to procrastinate, but also because of school obligations and college apps. Anyways, it turns out that the lithium ion trash-can battery is actually able to function after messing with the lock! With the battery, hub motor, and motor controller all sourced and installed, I set about tying up loose ends. The first thing that I fixed was the kickstand. On the original moped, the kickstand was directly attached to the engine and the engine was bolted onto the frame. Since I don’t have many machines/tools available to use, I couldn’t really machine a part that would be bolted into the frame to hold the kickstand. Thus, I decided to gut the engine to reduce its weight and keep it as the kickstand holder. This was quite easy, prying apart two halves of the engine made the internal components readily removeable. 

![](/images/moped/IMG_3556.jpg)

![](/images/moped/IMG_3571.jpg)

![](/images/moped/IMG_3574.jpg)

After wiring up the controller, installing the e-brakes, and swapping the old handle grips for the new one with a throttle, I was ready to test ride the moped. To my surprise, everything worked (this rarely happens). 

![](/images/moped/IMG_3672.jpg)

![](/images/moped/IMG_3671.jpg)

{{< youtube dXZxvsbFJXM >}}

I rode around for a good half an hour before becoming a little too overzealous with the throttle and accelerating way too fast, causing the axle itself to turn and tangle the wire running from the motor to the controller. Soon after that, the moped stopped working. My guess is that the insulation on one of the hall sensor wires and the motor phase wires may have become damaged, exposing the metal wire underneath. And when the wires tangled, the exposed metal may have touched and shorted. The excess current probably permanently damaged the hall sensor. Which would explain the problem that I was having regarding the wheel never turning. I wasn’t about to buy a new hub motor. And after probing with a multimeter I was able to conclude that one of my hall sensors was dead, so I ordered a replacement. I couldn’t find the drawing sheets for this specific hub motor because it was unbranded, but all sources on the Internet indicated that the hall sensors should be found inside the hub motor, on the edge of the stator and embedded in the laminated steel sheets. Since I didn’t have a better idea, I set about taking apart the hub motor to find and replace the hall sensors. The gear puller was particularly handy for this endeavour. Luckily for me, the hall sensors where exactly where the Internet said they would be, unfortunately, they were also epoxied into each of the cavities. With a mallet in one hand and a flathead screwdriver in the other, I spent around an hour chipping out the hall sensors. Yes, hall sensors with a plural because in my rush to fix the hub motor, I forgot to mark which hall sensor I needed to replace. So I replaced all three. I superglued the hall sensors in because I don’t have epoxy, soldered them back onto the board, and screwed the lid back on. After that, I rewired the controller and tested the moped. Thanks the my god-level soldering and problem solving skills, the hub motor now works! I’ve learned my lesson, and will try not to accelerate as much.

![](/images/moped/IMG_3674.jpg)

![](/images/moped/IMG_3687.jpg)

![](/images/moped/IMG_3675.jpg)