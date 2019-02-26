---
layout: post
title:hacked arlec RC210/213 poweroutlets which are bought from Bunnings
---

# this is tittle
We use Arduino mega, a sparkfun 434MHz receiver and transmitter, some wires. Using sparkfun RF link 434 MHz receiver to receive signal from remote and transmitter to send signal to RC 213 power outlets. The library RC-switch allows you to copy and clone
the binary code from RC213 sent out and received by power outlet sockets.   
   
    -Use the sample simple receiver sketch get details of the code your existing transmitter is sending.
    -Use this library and the sample send the sketch to recreate a transmission that is a copy of the signal sent by the original transmitter.
    -Once this is working you can use this as the basis for home automation. E.g. using Node-Red, OpenHAS, Alexa etc

It's found that Arlec RC 213 remote uses 32 data bits + 2 sync bits, but fortunately one of the sync bits is formatted like a data bit so you can send 33 data bits + 1 sync bit. We didn't succussfully decode binary code sent out from the remote by using 
sparkfun RF Link Receiver - 4800bps (434MHz), but we found that 8 existing codes from other projects online which are working well for our power outlets.The following two sets of binary codes are to turn the switches on and off, the last one if to turn 
all switches on and off.

Set 1:

    A(on): 011101101101100000001111100111100
    A(off):011101101101100000001110100111110

    B(on): 011101101101100000001101100111000
    B(off):011101101101100000001100100111010

    C(on): 011101101101100000001011100110100
    C(off):011101101101100000001010100110110

    D(on): 011101101101100000000111100101100
    D(off):011101101101100000000110100101110

    All(on): 011101101101100000000100100101010

For the first set, you will need to add this protocol in library (RCSwitch.cpp):

{ 385, { 1, 17 }, { 1, 2 }, { 2, 1 }, false }

Find out what codes your remote is sending, and hash the example codes for other types' switches in SendDemo.ino and then to modify pulselength by the following code:

```bash
mySwitch.setProtocol(1);
mySwitch.setPulseLength(306); #set pulse length
mySwitch.setRepeatTransmit(7); #set repeat counts
mySwitch.send("011101101101100000001111100111100"); #to switch A on
delay(1000); 
mySwitch.send("011101101101100000001110100111110"); #to switch A off
delay(1000);
```
Uploading the transmit code (SendDemo.ino) through arduino when the power socket turns into setup mode (plug in and led is flashing)

More details see https://github.com/sui77/rc-switch/wiki

Set 2:

    01000011000010000000111001000010    ' A off  ARLEC RC210
    01000011000010000000111101000011    ' A on
    
    01000011000010000000110001000000    ' B off  ARLEC RC210
    01000011000010000000110101000001    ' B on
    
    01000011000010000000101001000100    ' C off  ARLEC RC210
    01000011000010000000101101000101    ' C on
    
    01000011000010000000011001001100    ' D off  ARLEC RC210
    01000011000010000000011101001101    ' D on
    
    01000011000010000000100001000111    ' ALL off  for 10 secs to reset
    01000011000010000000010001001111    ' ALL on

```bash
mySwitch.setProtocol(1);
mySwitch.setPulseLength(270); #set pulse length
mySwitch.setRepeatTransmit(7); #set repeat counts
mySwitch.send("01000011000010000000111101000011"); #to switch A on
delay(1000);
mySwitch.send("01000011000010000000111001000010"); #to switch A off
delay(1000);
```
More details see https://www.thebackshed.com/forum/printer_friendly_posts.asp?FID=16&TID=9382
Hardware connection can be found here https://www.sparkfun.com/datasheets/RF/KLP_Walkthrough.pdf
