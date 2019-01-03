const Discord = require("discord.js");

module.exports.run = async (bot, message, args) => {
  
   const snekfetch = require('snekfetch');
    if (!args.slice(0).join(' ')) return message.channel.send('Geçerli bir yazı gir!')
        
    snekfetch.post('https://hastebin.com/documents')
        .send(args.slice(0)
            .join(' '))
        .then(body => {
            message.channel.send({embed: { description: "Yazını hastebine yükledim Link: \nhttps://hastebin.com/" + body.body.key, color: 0x1D82B6}});
        });

}
module.exports.help = {
  name: "hastebin",
 usage: "hastebin",
 description: "hastebin komutu"
}