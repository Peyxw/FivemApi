# FivemApi
A small and useful module. You can forward Fivem server information on discord!
# install :
```npm install FivemApiy```<br>
If you need help, you can come to:<br>
https://discord.gg/H6C8ggFfRu<br>
# How-to use :
```const fivem = require("FivemApiy");```<br>
```const server = new fivem.FivemApiy("000.000.00.00:30123");```<br>
Here is an example to display the number of players online on a server.<br>
(default port is 30123)<br>
# Requests :
* host - Hostname or IP of the game server.<br>

* port - Query port for the game server. (default port is 30120)<br>

* getServerStatus - Get server status of the server (online/offline)
<br>
* getPlayers - All players in the server. (array of objects)
<br>
* getPlayersOnline - Number of players online in the server.<br>

* getMaxPlayers - Get the maximum amount of players that are able to join the server.<br>

* getServerResources - Get all resource names of the server resources.<br>

* getServerLocale - The language of the server.<br>

* getServerVersion - Get version od the server.<br>

* getServerTags - Get all tags of the server.<br>

* getLicenseKey - The license key for the server.<br>
# Example :
```
const fivem = require("FivemApiy");
const server = new fivem.FivemApiy("000.000.00.00:30123");



client.on('message', async (message) => {
 if (!message.guild || message.author.bot) return;
 if (message.content === '!stats') {
    server.getPlayers().then((data) => {
      let result  = [];
      let index = 1;
      for (let player of data) {
        result.push(`${index++}. ${player.name} | ${player.id} ID | ${player.ping} ping\n`);
      }
      const playersOnline = await server.getPlayersOnline()
      const embed = new Discord.MessageEmbed()
        .setColor("BLUE")
        .setAuthor("Server is online")
        .setTitle(`Players (${data.length}/${playersOnline})`)
        .setDescription(result.length > 0 ? result : 'No Players Online!')
        .setTimestamp();
      message.channel.send(embed);
    }).catch((err) => {
      const embed = new Discord.MessageEmbed()
      .setColor("RED")
      .setAuthor("Server is offline")
      .setTimestamp();
    message.channel.send(embed);
    });
 }
});
```



