Boilerplate config and automations to integrate into your own Telegram bot.

If you restored this desktop from a backup all the configuration should be in the config files

You only need to register your own bot on Telegram and give the bot additional permissions to see your messages.
Then supply the api KEY in the config file
in [https://github.com/tomatensaus/DeyeSolarDesktop/configuration.yaml]
Input your bot's api key under "api_key" as supplied by the "BotFather_BOT"
Restart home assistant:
Now /start your bot and send it a some text, we will see the automation will log this event.

Home Assistant > Settings > Automations & Scenes > "Telegram debug automation to see chatIDs"
Right top corner click traces
Click the first cicle > Click "Changed variables" and look for:
```
trigger:
  id: Unknown
  idx: '10'
  alias: null
  platform: event
  event:
    event_type: telegram_text
    data:
      id: 4196
      chat_id: 123456789   #This be your chat_ID, also works for group so copy these to your config file
```  
Then fill this in on [https://github.com/tomatensaus/DeyeSolarDesktop/configuration.yaml]
The under "allowed_chat_ids"
and "chat_id"
repeat the process for your groups is so desired
restart home assistant again to make it aware of the "allowed_chat_ids" that it may respond to

If everything works the automation [https://github.com/tomatensaus/DeyeSolarDesktop/automation.yaml]
"Telegram debug automation to see chatIDs" also looks for the text "command1" to which it will respond
"command1 was understood and I will action it now", you can add another action that could switch on your hot water geyser, turn off lights etc. This was added as a simple "command" that you can expand on your own to your needs  


Message notifications of a power outage/loadshedding to warn you and report the battery SOC:
[https://github.com/tomatensaus/DeyeSolarDesktop/automation.yaml]
"Telegram Loadshedding annoucement" when the grid frequency drops below 48Hz then send a telegram that the grid is down and report the batter state of charge. Similarly when the grid returns then notify over telegram
Example message :"Loadshedding started with battery SOC: 98%"

Note:
```
- service: telegram_bot.send_message
  data:
    message: 'Loadshedding finished with battery SOC: {{states("sensor.deyeinverter_battery_soc")}}%'
    target: -12333321
```
the target should be the group id where you want the message to be sent to
