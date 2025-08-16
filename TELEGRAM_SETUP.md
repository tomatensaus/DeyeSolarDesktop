Boilerplate config and automations to integrate into your own Telegram bot.

NEW: please note that you can now setup your bot from Settings >> Devices and Services >> Add Integration >> Telegram (Once installed restart HA)
The above setup might replace the config needed in the [packages/telegram.yaml](./packages/telegram.yaml).  
The automation will still be needed to action telegram messages and responses

What do we need to achieve
1. You need to register with Telegram BotFather (A bot on telegram, see walkthrough below)
2. You need to find your chatID, this is a number such as 123221211 assigned to your telegram user. (This is done with an automation or looking in the logs)
3. You need to register this ChatID with the HA telegram plugin to allow HA to received and send messages to this user
4. The same applies when adding your Bot to a group (the group has a chatID)
5. Every user that wants to send or receive messages need to be added to you HA configuration


Old Steps:
Edit your [configuration.yaml](./configuration.yaml) and add the 2 lines that enable packages folder to be read, create a packages folder and copy the [packages/telegram.yaml](./packages/telegram.yaml) there.
```
homeassistant:
  packages: !include_dir_named packages
```
You only need to register your own bot on Telegram and give the bot additional permissions to (read your/send you) messages.
Then supply the api KEY in the config file in [packages/telegram.yaml](./packages/telegram.yaml) 

Input your bot's api key under "api_key" as supplied by the "BotFather_BOT" (walkrhtough below)
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
Then fill this in on [packages/telegram.yaml](./packages/telegram.yaml)
The under "allowed_chat_ids"
and "chat_id"
repeat the process for your groups if so desired (You can setup a chat group and then simply add users to the group)
restart home assistant again to make it aware of the "allowed_chat_ids" that it may respond to

If everything works the automation [packages/telegram_automation.yaml](./packages/telegram_automation.yaml) 
"Telegram debug automation to see chatIDs" also looks for the text "command1" to which it will respond
"command1 was understood and I will action it now", you can add another action that could switch on your hot water geyser, turn off lights etc. This was added as a simple "command" that you can expand on your own to your needs
PS: The contents of this automation file needs to be in your automations.yaml file (if you place it in packages it will not be editable via the UI)



Message notifications of a power outage/loadshedding to warn you and report the battery SOC:
[packages/telegram_automation.yaml](./packages/telegram_automation.yaml) 
"Telegram Loadshedding annoucement" when the grid frequency drops below 48Hz then send a telegram that the grid is down and report the batter state of charge. Similarly when the grid returns then notify over telegram
Example message :"Loadshedding started with battery SOC: 98%"

Note:
```
- service: telegram_bot.send_message
  data:
    message: 'Loadshedding finished with battery SOC: {{states("sensor.deyeinverter_battery_soc")}}%'
    target: -12333321
```
the "target" should be the user_id/group_id where you want the message to be sent to


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
copy your chatID into your [packages/telegram.yaml], there are 2 places I documented where it should be placed
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
I got a message from chatID:#yourChatID this is the group chatID, copy this to the [packages/telegram.yaml], under the place documented for the group
```
Restart Home Assistant

Go to your automations about the loadshedding and update the chatID so messages can go to your group by default, the hardcoded "target" is not valid. The next loadshedding event your home assistant service will let you know via telegram what the state of the grid is and also the battery charge

You can also send your bot/group a command. I have added the command1 as an example to be modified and customised. 
I use mine to remotely tell me what temperature my water heater is at, I can also trigger the heating of water by switching on the heatpump.

Now it is up to you to expand this into something useful that serves your purpose.
