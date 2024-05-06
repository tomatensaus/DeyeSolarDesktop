# How to copy this desktop to your existing Home Assistant
* This is for people that bought the [SmartDeyeDongle](./SmartDeyeDongle.yaml) with an exsting home assistant server.
* This is for anyone with anyone looking to copy some bits and pieces of this desktop for their own solar setup

## Consult this youtube video I made (especially if you are new to home assistant)
[![Watch the video](https://img.youtube.com/vi/Cqktgvu0ob0/0.jpg)](https://www.youtube.com/watch?v=Cqktgvu0ob0)

## UI Layout and Display
Please consult the yaml file [solarDesktop.yaml](./solarDesktop.yaml) that contains all the UI tabs provided in the screenshots, you could just create a new empty desktop and copy the whole contents.

## Integrations needed:
* Terminal server
* Studio code server
* [HACS download] (https://hacs.xyz/docs/setup/download/)
* ha-eskom-loadshedding (https://github.com/wernerhp/ha.integration.load_shedding) or also (https://github.com/swartjean/ha-eskom-loadshedding) You will need to register on sepush (https://eskomsepush.gumroad.com/l/api) for a free account if you are not a business

## HACS Plugins that you will need:
* Mushroom
* slider-entity-row
* layout-card
* Flexible Horseshoe Card
* Plotly Graph Card
* ApexCharts
* Atomic Calendar Revive
* Sunsynk Power Flow Card  (Note that this is now available in HACS, the video shows it still as a custom plugin to be manually added, just search and install)

## Config files
Configuration.yaml needed [configuration.yaml](./configuration.yaml)
and also copy the [template.yaml](./template.yaml)

# Automations:
Here [automations.yaml](automations.yaml)

Automations: Needed for the time of use configuration (that will copy the values from the inverter to dateTime objects(in home assistant), and when the user edits the time, it will convert the time to the format the inverter expects and update the inverter values via the smartDeyeDongle

Look out for these automations:
 1. InverterConfig send update to inverter
 2. InverterConfig send values to  HA time objects
