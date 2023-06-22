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


This is the walkthrough to get your bot talking to your home assistant server
=============================================================================
```
On Telegram search for the Botfather bot
/start
/newbot
select a name for your bot
select username for your bot, this needs to be unique
You will get the API key for your bot
copy paste this into configuration.yaml
/mybots
Select settings
Select Group privacy
Disable privacy mode
I am not strictly sure you need to give all admin rights to your bot but this is what I did
Group Admin rights
Add all the rights
Channel Admin rights
Add all the rights
```
Restart Home Assistant
```
click on the link that telegram provided for your bot t.me/mybot_link
/start
type a message for the bot
Now look in Home Assistant --> settings->System->logs
You should see an error message to say that
"Unauthorized update - neither user id #yourChatID nor chat id #anotherId is in allowed chats:
copy your chatID into configuration.yaml, there are 2 places I documented where it should be placed
```
Restart Home Assistant
```
send your bot any message
Home asssitant will also reply on this message and tell you what chat ID sent it a message
Go to automation "Telegram debug automation to see chatIDs" and look at the debug traces, this is the automation that replied to your message

I got a message from chatID:#yourChatID
Now your home assistant can talk to you and you can give it commands

Personally I like to add a group that I can easily add multiple people or remove them
On Telegram, Add group, be sure to add yourself and also the bot
send a message on the group... your bot will send you a private message:
I got a message from chatID:#yourChatID this is the group chatID, copy this to the configuration.yaml under the place documented for the group
```
Restart Home Assistant

Go to your automations about the loadshedding and update the chatID so messages can go to your group by default, the hardcode id is not valid. The next loadshedding your home assistant service will let you know via telegram what the state of the grid is and also the battery charge

You can also send your bot/group a command. I have added the command1 as an example. I use it to remotely tell me what temperature my water heater is at, I can also trigger the heating of water.

Now it is up to you to expand this into something useful that serves your purpose.
