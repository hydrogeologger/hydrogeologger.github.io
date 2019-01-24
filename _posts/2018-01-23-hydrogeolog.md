---
layout: post
title: hydrogeolog update
---

## learning from TMA9548 i2c multiplexer

it is found that if all the sensors connected to 9548 are not powered at the same time,
9548 may become disfunctional if it attempts to read from sensors. such disfunctional phenomenon persists even if arduino is restarted. the only way to recover is to power off 9548 and back on.
the way of getting around this is switch on all the sensors before reading, and switched them off all once. one could also connect reset (5v) to downside switch, or simply do a power control


## wish list form V2
   a.more holes for support the board
   b.reset arduino
   c.reverse switch for pi
   d.more nikkel area for the terminal block
   e.switch for voltage in switch
   f.more detail comments for pin holes
   g.reduce size
   h.commeing bolck to affiliated to anything on default
   i.reduce the width of the leads
   j.

## voltage divide for battery level. TO180914
   we have configured a thrid divider (2000 ohm and 1000 ohm resis). by then voltage was 13.56 on the battery. in between the battery the voltage was 4.18, which gives 1024 from arduino analog 1024 (which is strange as it is supposed to give 1024 when power is 5v)
nevertheless 4.18\*3 is 12.54, which is not 13.56 anyway. it is not clear for now why this had happened but as a power divider, one should use a quiter divide ratehr than a third for arduino.

## power consumption list

TO180530

logger + pi zero + rasbian stretch +onboard wifi to eduroam

 peak power consumption is 0.114A\*12.7V  = 1.448W 

 idle power consumption is 0.087A\*12.7V  = 1.104W 
 


TO181113

logger + pi zero + rasbian stretch +external 3g dongle+wifi thethering

 idle power consumption is 0.17A\*12.7V  = 2.1W 

TO181113

logger + pi zero + rasbian stretch +external waterproof antenna wifi (black) to eduroam

 peak power consumption is 0.229A\*12.7V  = 2.9W 

waterproof antenna is the power consumpition most item

TO181113

logger +PI3B+  raspbian stretch +wifi antenna 


