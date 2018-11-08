---
layout: post
title: webpage install try
---
<!---this is comment---> 
# 1. making raspberry pi connecting with arduino using gpio without ftdi
  I have been thinking about this a lot and finally got solution:

![image](/images/rpi_arduino_serial.png)

{% highlight bash %}
npm install -g phant
{% endhighlight %}

more information
  oscar Liang was using 1.6k and 3.3k as voltage divider. while Deanmao was using 10k and 15k. the latter was found ok to receive data but not upload script. the former works perfectly

  1 micro F is found enough to emulate dtx pins, i used a electrolytic capacitor, and found it works on any directions (positive could either be at reset or digital)
  it is also needed to change the avidude file by incorporating autoreset. the reference has a few ones that are usagable
  arduino ide comes with avrdude, it is needed to change the avrdude inside arduino ide
  also it is found that if tx and rx pins on the arduino surface is connected to rpi, it overrides ftdr, meaning ftdr will not receiee any data.  

reference:
http://redhunter.com/blog/2015/01/09/raspberry-pi-arduino-ide-via-gpio/
https://github.com/deanmao/avrdude-rpi
http://www.deanmao.com/2012/08/12/fixing-the-dtr-pin/
https://oscarliang.com/raspberry-pi-and-arduino-connected-serial-gpio/

