A Simple dashboard use cheap grid power during winter days (Built for European customers)

Enable your inverter to fill the battery during the cheapest hours 
Run from the battery power during the expensive hours 

Be sure to setup a packages folder in your Home Assistant config folder and include this reference in your [configuration.yaml](./configuration.yaml)
To learn how to setup dashboards/automations/config please look at the installation section on my octupus flux video (forward to the install section)
You will also need to install the HACS component to supply the rates for your country. TODO: Include links for each country

Steps all relevant to the country sections below:
1. Create Empty Dashboard and do a raw copy of the relevant dashboard (described in the youtube video)
2. copy the configiration file contents to the packages folder with a yaml extension
3. copy the contents of the automations to your automations.yaml making sure to keep the indentation the same
4. Install the energy provider HACS component supplying the rates for your country
5. Developer Tools >> Check the config. If all good restart you home assistant.

For Countries using Nordpool as energy provider (built using country LT)
* Dashboard [Norpool Dashboard](./packages/nordpool_dashboard.yaml)  
* Nordpool configuration in packages folder [packages/nordpoool.yaml](./packages/nordpoool.yaml)
* Automations [automations.yaml](./packages/nordpool_automation.yaml)

Poland using TSE Rates
* Dashboard [Polish Dashboard](./packages/polish_tge_dashboard.yaml)  
* TGE configuration in packages folder [packages/polish_tge.yaml](./packages/polish_tge.yaml)
* Automations [automations.yaml](./packages/polish_tge_automations.yaml)

(my home server had a disk failure so my test HA is currently offline. As soon as I can get it replaced I will test the files I have)
Netherlands using Tiber (coming soon)  
* Dashboard
* Configuration
* Automations



