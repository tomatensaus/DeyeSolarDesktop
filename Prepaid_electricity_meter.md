##Some notes to integrate the prepaid meter:

## This Guide goes along with a Youtube video
TODO, still need to make a video

This config stores the config files in "Packages"

## Steps:
1. Install the Dashboard [prepaidmeter_dashboard.yaml](./packages/prepaidmeter_dashboard.yaml) Create empty dashboard and do raw copy.
2. Create the packages folder and copy the prepaidmeter.yaml file to packages [prepaidmeter.yaml](./packages/prepaidmeter.yaml)
3. Copy the contents of the prepaidmeter_automations.yaml to your automations.yaml file [prepaidmeter_automations.yaml](./packages/prepaidmeter_automations.yaml)
4. Copy the lines from configuration.yaml "homeassistant: packages: !include_dir_named packages" to your configuration.yaml
[configuration.yaml](./configuration.yaml)
5. Restart Home Assistant, make sure the configuration Changes are good before restarting
6. Look at your prepaid meter and enter the amount of units shown on "Prepaid meter Recharge Units"
7. Add notifications via Telegram to notify yourself when your prepaid electricity is nearly depleted