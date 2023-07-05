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
