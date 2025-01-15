The SmartDeyeDongle contains all the decoding logic for the inverter and will give you a seamless integration into Home Assistant and the DeyeSolarDesktop

The new SmartDeyeDongle V4 has passed tests.
![image](./SmartDeyeDongle.jpg)


### What you need to have already:
* You need to be running a single/split phase Deye/Sunsynk hybrid inverter (Master & Slave also supported).
* 3Phase Low Voltage is now suported. (Master & Slave also supported)
* 3Phase High Voltage is also supported. (Master & Slave also supported)
* String inverters and micro inverters are not currently supported

  ### Models supported
* Single/Split phase Low Voltage (40-60V Battery) 16kW/15kW/14kW/12kW/10kW/8kW/6kW/5kW/3.6kW/3kW
* 3 Phase Low Voltage (40-60V Battery) 20kW/18kW/16kW/15kW/14kW/12kW/10kW/8kW/6kW/5kW/4kW/3kW
* 3 Phase High Voltage (200-800V Battery) 80kW/75kW/70kW/60kW/50kW/40kW/35kW/30kW/25kW/20kW/15kW/12kW/10kW/8kW/6kW/5kW

* You need to run your own home assistant (https://www.home-assistant.io/installation/) on an old PC/VM/Laptop/Rasp Pi or similar must support 64bit.
* You need to have a 2.4GHz wifi network at the inverter with reasonable network coverage.

#### Not included (must supply your own):
Either
* You need to have an old micro-USB (type B) phone charger to supply power, even if it is a slo-o-o-ow charger, 500mA it is fine. These are still common even today for most electronic devices
OR Alternatively
* The SmartDeyeDongle V4 also supports input from 5V-16V so we can actually power it directly from the inverter 12V power supply (pin 11&12 on my 8kW marked as RST, consult your inverter documentation) **Note that the 3.6/5/6kW does not have this output. Use a an old phone charger with micro-USB

### Cost
I have an online store at https://smarthomeintegrations.co.za where you can order the SmartDeyeDongle. My contact details are on the website if you need to contact me.

Shipping R100 via The Courier Guy (3-4 business days economy, but most of the times they deliver the next day)
I added a few international options, I can ship limited numbers and items (for now only the Dongle & ESP32)
My website now includes an online flasher to allow anyone to purchase and flash the firmware.
This will open up up possibilities for international sales.


### 3D printed designs
The Official 3D Print design is available for sale on the website. Designed by an Engineering student to help pay for his university tuituion.

Thanks to mrfrikkie on carbonite these designs were shared for free. They might need some tweaking to get them perfect
[Base stl](./SmartDeyeDongle-Base.stl)
[Lid stl](./SmartDeyeDongle-Lid.stl)
