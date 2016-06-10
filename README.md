# Greenbot REST API

This is a REST API for **[Greenbot](https://github.com/green-bot/greenbot-core)**.

Greenbot is a bot server - a piece of middleware that connects different sorts of bots to different messaging networks. For more information on Greenbot, visit the project site.

## Overview
This REST API covers three of major collections that power Greenbot: Bots, Scripts and Sessions.
The Greenbot Core runs on MongoDB, and each of these collections is represented by a
collection in mongo.  This REST API mirrors those collections.

## Installation

Assuming greenbot-core is successfully installed, and MongoDB is installed and running.

```
git clone https://github.com/green-bot/greenbot-restapi
cd greenbot-restapi
npm install
npm start
```
## Collections
* **Bots** - The actual implementation of a bot; that unique thing that will answer the message. Configuration such as network connections and prompt configurations, are described in the Bots collection.
* **Scripts** - A single kind of bot. Every bot is an instance of a script. When we install a new kind of bot into the greenbot-core, we are adding another element into this collection. How a type of bot runs, such as the actual program that needs to run, or the default settings for this kind of bot, are described in the Scripts collection.
* **Sessions** - Each conversation completed by a bot is saved in the Sessions collection. The transcript, the participants, and the collected data are all saved in this collection.

The Network, user and NetworkHandle collections are not exposed through this API.


## Bot Resource Description
Field | Description
----- |  -----------
_id | The objectId of the bot. Corresponds to the MongoDB id
accountId | The ID of the account that owns this bot.
description | The description of this bot
name | The human name of the bot.
scriptId | The ID of the script that this bot is an instance of.
settings | An array of configuration options for the bot. Each element defines the name of the option, the actual value used in the bot, and type of configuration item it is.
passcode | A passcode to allow the user to administer the bot.
notificationEmails | Comma separated list of recipients to send emails to when session is complete.
notificationEmailSubject | The subject of the email sent to the list in notificationEmails
postConversationWebhook | A URL to post Session objects to at the end of the conversation
addresses | An array of elements describing the network addresses that will trigger this bot. For a complete description of how these addresses work, please see _____. Each element defines a networkHandleId, used to track network porting requests, networkHandleName, a construct of the network name and the identifier (think twitter::@howethomas), an array of keywords that will trigger the start of this bot, and the actual network name of the address.
ownerHandles | An array of network names (such as ['twitter::@howethomas', 'nexmo::16175551212']) that should be treated as owners of the bot. Some scripts have one executable for owners, and a different one for non-owners.  This controls the list of owners.

## Script Resource Description
Field | Description
----- |  -----------
_id | The objectId of the bot. Corresponds to the MongoDB id
default_cmd | The command to run to start bots made from this script. Example 'npm start --loglevel silent'
default_path | The cwd bots based on this script. Example './node_modules/not-available-bot'
default_settings | An array of configuration options for the bots made from this script. Each element defines the name of the option, the actual value used in the bot, and type of configuration item it is.
desc | The description of this bot. Example: 'A simple bot to tell the visitor that there isnt a bot to talk to, except this one, and it aint talking.'
name | The human name of the bot.
icon_class | The font-awesome icon to use when displaying bots based on this script. Example: 'information'
owner_cmd | The command to run when owners message into sbots made from this script. Example 'bundle exec ruby owner.rb'
short_desc | A shorter desc for summary display. Example: 'An under-construction bot'
repo_link | A git repo where this script lives. Example:  "https://github.com/green-bot/not-available-bot"
npm_pkg_name | The name in NPM for this script. Example: "not-available-bot"
npm_pkg_location | The installation location for this script. Example: "./node_modules/not-available-bot"
