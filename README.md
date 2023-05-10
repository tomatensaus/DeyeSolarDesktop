# DeyeSolarDesktop

If you are new to home assistant then the DeyeSolarDesktop Home Assistant backup is a quick and sure way to get your solar monitoring up and running. Initially this will be very focussed on the South African market where power outages are common occurences.

This desktop was built to proved plug and play integration with the smartDeyeDongle which can be purchased seperately (available towards end of June 2023)
The smartDeyeDongle contains all the decoding logic for the inverter and will give you a seamless integration into Home Assistant

Compatible hardware: This desktop was built for Deye inverters (which includes all the rebranded inverters Sunsynk/Sol-Ark etc). First relase is focussed on 5/8 KW single phase inverters.

The backup file should contain all the home assistant plugins and integrations pre-configured to get you started plus the DeyeSolarDesktop
Steps:
1. Install your own Home Assistant server
2. Restore the backup file (found in releases)
3. Login with user: solar password: solar123 (be sure to delete this user once done)
4. Plug in your smartDeyeDongle, connect to the hot-spot it provides and configure your wifi network details, once saved it will reboot and join your network
5. Home Assistant will detect a new device called Deye inverter, click configure and your desktop will start recording data (Some parts like eg. graphs will only populate once there is enough data)
6. Modify and delete what does not suit you, it is your desktop after all. Feel free to suggest improvements and fix wrong values


In the case that you already have Home Assistant server, do not install the backup.
You can pick and choose sections of the desktop to build your own

Integrations needed:
HACS
Terminal server
Studio code server

Plugins that you will need:
Mushroom
slider-entity-row
layout-card
Flexible Horseshoe Card
Plotly Graph Card
ApexCharts

Configuration.yaml needed
```
sensor:
  - platform: statistics
    name: "min_soc_battery"
    entity_id: sensor.deyeinverter_battery_soc
    state_characteristic: value_min
    max_age:
      hours: 12
    sampling_size: 144

input_datetime:
  timezone1_time:
    name: Timezone 1 Time
    has_date: false
    has_time: true
  timezone2_time:
    name: Timezone 2 Time
    has_date: false
    has_time: true
  timezone3_time:
    name: Timezone 3 Time
    has_date: false
    has_time: true
  timezone4_time:
    name: Timezone 4 Time
    has_date: false
    has_time: true
  timezone5_time:
    name: Timezone 5 Time
    has_date: false
    has_time: true
  timezone6_time:
    name: Timezone 6 Time
    has_date: false
    has_time: true

template:
  sensor:
  - name: "deyeinverter_solar_power_used"
    state: "{{ (states('sensor.deyeinverter_summary_day_pv_energy') | float(0) - states('sensor.deyeinverter_summary_day_battery_charge') | float(0)) |round(1) }}"
    unit_of_measurement: "kWh"
    device_class: energy

  - name: "deyeinverter_essential_load"
    state: "{{ (states('sensor.deyeinverter_inverter_output_power') |float(0)  + (states('sensor.deyeinverter_grid_load') |float(0) - states('sensor.deyeinverter_aux_output_power') |float(0) )) | round(0)}}"
    unit_of_measurement: "W"
    device_class: power

  - name: "deyeinverter_non_essential_load"
    state: "{{ (states('sensor.deyeinverter_grid_external_power') |float(0)  - (states('sensor.deyeinverter_grid_load') |float(0))) | round(0)}}"
    unit_of_measurement: "W"
    device_class: power
```

Automations: Needed for the time of use configuration (that will copy the values from the inverter to dateTime objects(in home assistant), and when the user edits the time, it will convert the time to the format the inverter expects and update the inverter values via the smartDeyeDongle

    ```
    alias: InverterConfig send update to inverter
    description: ""
    trigger:
      - platform: state
        entity_id:
          - input_datetime.timezone1_time
          - input_datetime.timezone2_time
          - input_datetime.timezone3_time
          - input_datetime.timezone4_time
          - input_datetime.timezone5_time
          - input_datetime.timezone6_time
    condition:
      - condition: template
        value_template: "{{ trigger.to_state.state != 'unavailable' }}"
    action:
      - service: number.set_value
        target:
          entity_id: number.deyeinverter_timezone1_time
        data:
          value: >-
            {{state_attr('input_datetime.timezone1_time', 'timestamp') |
            timestamp_custom("%H%M", false) | float}}
      - service: number.set_value
        target:
          entity_id: number.deyeinverter_timezone2_time
        data:
          value: >-
            {{state_attr('input_datetime.timezone2_time', 'timestamp') |
            timestamp_custom("%H%M", false) | float}}
      - service: number.set_value
        target:
          entity_id: number.deyeinverter_timezone3_time
        data:
          value: >-
            {{state_attr('input_datetime.timezone3_time', 'timestamp') |
            timestamp_custom("%H%M", false) | float}}
      - service: number.set_value
        target:
          entity_id: number.deyeinverter_timezone4_time
        data:
          value: >-
            {{state_attr('input_datetime.timezone4_time', 'timestamp') |
            timestamp_custom("%H%M", false) | float}}
      - service: number.set_value
        target:
          entity_id: number.deyeinverter_timezone5_time
        data:
          value: >-
            {{state_attr('input_datetime.timezone5_time', 'timestamp') |
            timestamp_custom("%H%M", false) | float}}
      - service: number.set_value
        target:
          entity_id: number.deyeinverter_timezone6_time
        data:
          value: >-
            {{state_attr('input_datetime.timezone6_time', 'timestamp') |
            timestamp_custom("%H%M", false) | float}}
    mode: single

    ```


    ```
    alias: InverterConfig send values to  HA time objects
    description: ""
    trigger:
      - platform: state
        entity_id:
          - number.deyeinverter_timezone1_time
          - number.deyeinverter_timezone2_time
          - number.deyeinverter_timezone3_time
          - number.deyeinverter_timezone4_time
          - number.deyeinverter_timezone5_time
          - number.deyeinverter_timezone6_time
    condition:
      - condition: template
        value_template: "{{ trigger.to_state.state != 'unavailable' }}"
    action:
      - service: input_datetime.set_datetime
        target:
          entity_id: input_datetime.timezone1_time
        data:
          time: >-
            {% set min = ((states('number.deyeinverter_timezone1_time') | int) %
            100) %} {% set hour = ((states('number.deyeinverter_timezone1_time') |
            int) // 100) %} {{hour|format('02d')}}:{{min|format('02d')}}:00
      - service: input_datetime.set_datetime
        target:
          entity_id: input_datetime.timezone2_time
        data:
          time: >-
            {% set min = ((states('number.deyeinverter_timezone2_time') | int) %
            100) %} {% set hour = ((states('number.deyeinverter_timezone2_time') |
            int) // 100) %} {{hour|format('02d')}}:{{min|format('02d')}}:00
      - service: input_datetime.set_datetime
        target:
          entity_id: input_datetime.timezone3_time
        data:
          time: >-
            {% set min = ((states('number.deyeinverter_timezone3_time') | int) %
            100) %} {% set hour = ((states('number.deyeinverter_timezone3_time') |
            int) // 100) %} {{hour|format('02d')}}:{{min|format('02d')}}:00
      - service: input_datetime.set_datetime
        target:
          entity_id: input_datetime.timezone4_time
        data:
          time: >-
            {% set min = ((states('number.deyeinverter_timezone4_time') | int) %
            100) %} {% set hour = ((states('number.deyeinverter_timezone4_time') |
            int) // 100) %} {{hour|format('02d')}}:{{min|format('02d')}}:00
      - service: input_datetime.set_datetime
        target:
          entity_id: input_datetime.timezone5_time
        data:
          time: >-
            {% set min = ((states('number.deyeinverter_timezone5_time') | int) %
            100) %} {% set hour = ((states('number.deyeinverter_timezone5_time') |
            int) // 100) %} {{hour|format('02d')}}:{{min|format('02d')}}:00
      - service: input_datetime.set_datetime
        target:
          entity_id: input_datetime.timezone6_time
        data:
          time: >-
            {% set min = ((states('number.deyeinverter_timezone6_time') | int) %
            100) %} {% set hour = ((states('number.deyeinverter_timezone6_time') |
            int) // 100) %} {{hour|format('02d')}}:{{min|format('02d')}}:00
    mode: single

    ```

Special mentions:
https://github.com/slipx06 for sharing a large portion of the desktop and the brilliant power flow card

You do not need to buy the smartDeyeDongle, there are other options:
https://github.com/kellerza/sunsynk You need to buy an USB to RS485 cable and connect to your Home Assistant server, you will also need to map entities from this project as the names differ
https://github.com/StephanJoubert/home_assistant_solarman Pull the values from the solarman dongle (delayed 5-10 minutes) it is not ideal for integrations but it could work for those simply wanting to view values at the end of the day. Once again you will need to map all the entity names.

Coming Soon:
Boilerplate config and automations to integrate into your own Telegram bot. Once a power outage/loadshedding starts you need to receive a message to warn you and tell you the SOC of the battery.

Why this project:
I believe that knowledge is power. Once you understand your power usage you will be able to optimise it. We are rapidly moving towards a future where there is a need to have a smart home with smart power usage. Since the platform allows automations that is the next logical step towards a greener future. If this project can enable every house to save just 5% of power sourced from dirty generation (such as coal) and replace it with power from panels already installed we have achieved our goal. Now if that saves the user money that can be seen as a bonus. We are well on our way to a more sustainable future.
