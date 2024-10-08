The SmartDeyeDongle contains all the decoding logic for the inverter and will give you a seamless integration into Home Assistant and the DeyeSolarDesktop

The new SmartDeyeDongle V4 has passed tests.
![image](./SmartDeyeDongle.jpg)


### What you need to have already:
* You need to be running a 5/6/8/10/12/14/16kW single/split phase Deye/Sunsynk hybrid inverter (Master & Slave also supported).
* 3Phase 6/8/10/12kW Low Voltage is now suported. (Master & Slave also supported)
* 3Phase 12/20/30/50 Hight Voltage is also supported. (Master & Slave also supported)
* String inverters and micro inverters are not currently supported

* You need to run your own home assistant (https://www.home-assistant.io/installation/) on an old PC/VM/Laptop/Rasp Pi or similar must support 64bit.
* You need to have a 2.4GHz wifi network at the inverter with reasonable network coverage.

#### Not included (must supply your own):
Either
* You need to have an old micro-USB (type B) phone charger to supply power, even if it is a slo-o-o-ow charger, 500mA it is fine. These are still common even today for most electronic devices
OR Alternatively
* The SmartDeyeDongle V4 also supports input from 5V-16V so we can actually power it directly from the inverter 12V power supply (pin 11&12 on my 8kW marked as RST, consult your inverter documentation) **Note that the 5kW might not have this output. There is no mention in any of the documentation

### Cost
I have an online store at https://smarthomeintegrations.co.za where you can order the SmartDeyeDongle. My contact details are on the website if you need to contact me.

Shipping R100 via The Courier Guy (3-4 business days economy, but most of the times they deliver the next day)
I added a few international options, I can ship limited numbers and items (for now only the Dongle & ESP32)
My website now includes an online flasher to allow anyone to purchase and flash the firmware.
This will open up up possibilities for international sales.


### 3D printed designs
The Official 3D Print design is available for sale on the website. Designed by an Engineering student to help pay for his tuituion.

Thanks to mrfrikkie on carbonite these designs were shared for free. They might need some tweaking to get them perfect
[Base stl](./SmartDeyeDongle-Base.stl)
[Lid stl](./SmartDeyeDongle-Lid.stl)
