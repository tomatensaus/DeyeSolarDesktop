A Simple dashboard use cheap grid power during winter days (Built for European customers)

Enable your inverter to fill the battery during the cheapest hours 
Run from the battery power during the expensive hours 

These dashboards follow the same pattern
Be sure to setup a packages folder in your Home Assistant config folder and include this reference in your [configuration.yaml](./configuration.yaml)
To learn how to setup dashboards/automations/config please look at the installation section on my octupus flux video (forward to the install section)
You will also need to install the HACS component to supply the rates for your country.

For Countries using Nordpool as energy provider (built using country LT)
* Dashboard [Norpool Dashboard](./packages/nordpool_dashboard.yaml)  
* Nordpool configuration in packages folder [packages/nordpoool.yaml](./packages/nordpoool.yaml)
* Automations [automations.yaml](./packages/nordpool_automation.yaml)

Poland using TSE Rates
* Dashboard [Polish Dashboard](./packages/polish_tge_dashboard.yaml)  
* TGE configuration in packages folder [packages/polish_tge.yaml](./packages/polish_tge.yaml)
* Automations [automations.yaml](./packages/polish_tge_automations.yaml)

Netherlands using Tiber (coming soon)  
* Dashboard
* Configuration
* Automations
my home server had a disk failure so my test HA is currently offline. As soon as I can get it replaced I will test the files contributed


