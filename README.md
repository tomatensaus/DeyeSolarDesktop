# DeyeSolarDesktop

Let's get your desktop up and running, once entities are populating with data it will look like this:

![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/DeyeTab.png)
![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/GraphsTab1.png)
![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/GraphsTab2.png)
![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/InverterValuesTab.png)
![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/ConfigTab.png)
![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/TimeOfUseTab1.png)
![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/TimeOfUseTab2.png)
![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/StandardEnergyDashboard.png)

If you are new to home assistant then the DeyeSolarDesktop Home Assistant backup is a quick and sure way to get your solar monitoring up and running. Initially this will be very focussed on the South African market where power outages are common occurences.

This desktop was built to provide a plug and play integration with the smartDeyeDongle which can be purchased seperately (available towards end of June 2023). But you can still use this desktop without the smartDeyeDongle (Details below).
The smartDeyeDongle contains all the decoding logic for the inverter and will give you a seamless integration into Home Assistant and this desktop

Compatible hardware: This desktop was built for Deye inverters (which includes all the rebranded inverters Sunsynk/Sol-Ark etc). There is no reason why you could not use some of the desktop and integrations for another inverter.

The backup file should contain all the home assistant plugins and integrations pre-configured to get you started plus the DeyeSolarDesktop
Steps:
1. Install your own Home Assistant server  (you need an old PC/rasp pi/VM om your PC)
2. Restore the latest backup file in your new home assistant (found in https://github.com/tomatensaus/DeyeSolarDesktop/releases)
3. Login with user: solar password: solar123 (be sure to delete this user and create your own user)
   ![image](https://raw.githubusercontent.com/tomatensaus/DeyeSolarDesktop/main/EmptyDesktop.png)
   This is what the empty desktop looks like before any solar data is populated from the inverter.
4. Plug in your smartDeyeDongle, connect to the wifi hot-spot it provides and configure your wifi network details, once saved it will reboot and join your wifi network. (alternatively use one of the other methods specified below)
5. Home Assistant will detect a new device called Deye inverter, click "configure" and your desktop will start recording data (Some parts like eg. graphs will only populate once there is enough data)
6. Modify and delete what does not suit you, it is your desktop after all. Feel free to suggest improvements and fix any wrong values
7. You are done, enjoy! Tell your friends! Be sure to report any issues when you find some.


In the case that you already have Home Assistant server, do not restore the backup.
There are some instructions below to guide you towards building your desktop.
Please consult the yaml file (https://github.com/tomatensaus/DeyeSolarDesktop/blob/main/solarDesktop.yaml) that contains all the tabs provided in the screenshots, you could just create a new empty desktop and copy the whole contents.
Delete what you do not like or do not neeed. Build your own

Integrations needed:

* HACS
* Terminal server
* Studio code server
* ha-eskom-loadshedding (https://github.com/wernerhp/ha.integration.load_shedding) or also (https://github.com/swartjean/ha-eskom-loadshedding) You will need to register on sepush (https://eskomsepush.gumroad.com/l/api) for a free account if you are not a business


HACS Plugins that you will need:

* Mushroom
* slider-entity-row
* layout-card
* Flexible Horseshoe Card
* Plotly Graph Card
* ApexCharts


Configuration.yaml needed [https://github.com/tomatensaus/DeyeSolarDesktop/configuration.yaml]

Automations: Needed for the time of use configuration (that will copy the values from the inverter to dateTime objects(in home assistant), and when the user edits the time, it will convert the time to the format the inverter expects and update the inverter values via the smartDeyeDongle

Look out for these automations:
 1. InverterConfig send update to inverter
 2. InverterConfig send values to  HA time objects
Here [https://github.com/tomatensaus/DeyeSolarDesktop/automation.yaml]

Special mentions:
https://github.com/slipx06 for sharing a large portion of the desktop and the brilliant power flow card


Getting the Data from your inverter
* Preferred way is to buy the smartDeyeDongle, it plugs into your inverter and translates all the data to home assistant directly, you can expect real time data updated every 3s and the ability to change settings via the screen or automations.

* You need to buy an USB to RS485 cable and connect to your Home Assistant server, you will also need to map entities from this project as the names differ https://github.com/kellerza/sunsynk  (provides real-time data, works via MQTT)

* Last option is also the cheapest but requires no additional cables to be purchased. You could pull the values from the solarman dongle (delayed 5-10 minutes) it is not ideal for integrations that need to get updates in real time but it could work for for you if you simply want to look at the graphs https://github.com/StephanJoubert/home_assistant_solarman

Telegram integration:
see [https://github.com/tomatensaus/DeyeSolarDesktop/TELEGRAM_SETUP.md]

Why this project:
I believe that knowledge is power. Once you understand your power usage you will be able to optimise it. We are rapidly moving towards a future where there is a need to have a smart home with smart power usage. Since the platform allows automations that is the next logical step towards a greener future. If this project can enable every house to save just 5% of power sourced from dirty generation (such as coal) and replace it with power from panels already installed we have achieved our goal. Now if that saves the user money that can be seen as a bonus. Helping people to move towards a sustainable future
