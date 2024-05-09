This is the guide to setup your own octopus Flux Dashbord for import/Export
=============================================================================
- complete with automations
- charges the battery 02:00 - 05:00  (configurable)
- discharges the battery 16:00 - 19:00 (configurable)
- auto-Calculating both the charge rate and discharge rate to ensure that we do not use more current than needed (full code available in the yaml files)

This Guide goes along with a Youtube video
[![Watch the video](https://img.youtube.com/vi/hrFTqnmWWso/0.jpg)](https://www.youtube.com/watch?v=hrFTqnmWWso)

## You will need:
1. Deye/Sunsunk hybrid inverter
2. Home Assistant Server
3. [SmartDeyeDongle](./SmartDeyeDongle.md) + Dashboard setup (It relies some of the other components)
4. The right plan from Octopus energy  
You can support me by signing up with Octopus using my UK friend's Octopus referal code
[https://share.octopus.energy/witty-ibis-586]

## Step 1: Backup your configuration before you start, Full Backup + download it locally

## HACS Plugins Needed:
1. All the plugins from the Standard Dashboard [JustGrabbingSomeIdeas.md](./JustGrabbingSomeIdeas.md)
2. Solcast PV Solar
3. Octopus Energy

Note that both of these require you to register for API Keys.
Solcast has a free plan.
Octopus energy you need the API Key and Account ID

## Steps:
1. Install the Dashboard [octopusflux_dashboard_importexport.yaml](./packages/octopusflux_dashboard_importexport.yaml) Create empty dashboard and do raw copy.
2. Create the packages folder and copy the octopusflux.yaml file to packages [octopusflux.yaml](./packages/octopusflux.yaml)
3. Copy the contents of the octopusflux_automations.yaml to your automations.yaml file [octopusflux_automations.yaml](./packages/octopusflux_automations.yaml)
4. Copy the lines from configuration.yaml "homeassistant: packages: !include_dir_named packages" to your configuration.yaml
[configuration.yaml](./configuration.yaml)
5. Restart Home Assistant, make sure the configuration Changes are good before restarting

## Final Configuration:
- Disable all octopus flux automations while we setup the items below
- Setup your Inverter with the config items
- Times for TimeZone1 (2:00 - 5:00)
- Times for TimeZone4 (16:00 - 19:00)
- Setup your desired State of Charge in TimeZone 1 for Charging
- Setup your desired State of Charge in TimeZone 4 for Discharging
- Setup a desired reserve percentage for discharging
- When everything is ready then enable the automations again. Be sure to monitor it closely
- Fix the dashboard graphs to point to your own octopus meter numbers
