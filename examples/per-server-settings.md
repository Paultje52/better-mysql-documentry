---
description: Per Discord server settings using better-MySQL and discord.js
---

# Per server settings

Oke, let's start with making the file `firstrun.js`. In this file, set this content.

{% code-tabs %}
{% code-tabs-item title="If you can make databases" %}
```javascript
// First, require the module.
const mysql = require("better-mysql");
// Then login to the mysql service
let client = new mysql.client({
  host: "HOST",
  user: "YOURUSERNAME",
  pass: "YOURPASSWORD123"
});
// Now, create the database "better-mysql-bot", but you can rename it to whatever you want.
client.createDatabase("better-mysql-bot").then(async (database) => {
  let table = await client.createTable("guildsettings", ["Guild", "Settings"]);
});
```
{% endcode-tabs-item %}

{% code-tabs-item title="If you can\'t make databases" %}
```javascript
// First, require the module.
const mysql = require("better-mysql");
// Then login to the mysql service
let client = new mysql.client({
  host: "HOST",
  user: "YOURUSERNAME",
  pass: "YOURPASSWORD123"
});
// Now, load the database that you have.
client.loadDatabase("allready-existing-database").then(async (database) => {
  let table = await client.createTable("guildsettings", ["Guild", "Settings"]);
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now the `bot.js`.

```javascript
// Better-mysql
const betterMysql = require("./client/index.js");
let mysqlClient = new betterMysql({
  host: "db4free.net",
  user: "paul52",
  pass: "Paul12345"
});
let database;
let guilds;
let guildSettings = {};
mysqlClient.loadDatabase("hosting123").then(async (db) => {
  console.log("Database is loaded!");
  database = db;
  guilds = await database.loadTable("guildsettings");
  console.log("Database and table are loaded!");
});

// SQL event
mysqlClient.on("sql", (a, place, func, part) => {
  if (part) func = `${func}.${part}`;
  console.log(`Running to mysql database function ${func} (in ${place})`);
});


// Discord.js
const Discord = require("discord.js");
let client = new Discord.Client();
client.login("NDA3NTM5NzgyOTU3MjY4OTky.Ds82tA.MbG4aMYiXk-KHhYbzdSBFxYv2Z0");

// Ready event
client.on("ready", () => {
  console.log("Loading...");
  let interval = setInterval(() => {
    if (typeof database !== "object" || typeof guilds !== "object") return;
    console.log("I'm online!");
    clearInterval(interval);
  }, 100);
});

// Message event
client.on("message", async (message) => {
  // Checking
  if (!message.guild) return;
  if (message.author.bot) return;
  if (typeof database !== "object" || typeof guilds !== "object") return;

  // Making or loading the guild functions
  let filter = new mysqlClient.filter();
  filter.add("Guild", message.guild.id);
  if (!guildSettings[message.guild.id]) {
    guildSettings[message.guild.id] = await guilds.ensure(filter, [message.guild.id, {
      prefix: "!"
    }])[0];
  }
  let settings = guildSettings[message.guild.id].Settings;

  // Making the command and arguments
  if (!message.content.toLowerCase().startsWith(settings.prefix)) return;
  const args = message.content.slice(settings.prefix.length).trim().split(/ +/g);
  const command = args.shift().toLowerCase();

  // The setprefix command
  if (command === "setprefix") {
    if (!args[0]) return message.reply(`The prefix now is **${settings.prefix}**.`);
    if (args[0].length > 5) return message.reply("A prefix can't be more than 5 characters.");
    settings.prefix = args[0].toLowerCase();
    guildSettings[message.guild.id] = settings;
    await guilds.update(filter, settings);
    message.reply(`Prefix chanced to **${settings.prefix}**.`);
  }

  // Add here more commands
});
```

