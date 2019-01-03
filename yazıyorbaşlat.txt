const Discord = require('discord.js');

module.exports.run = (bot, message , args) => {
      message.channel.startTyping();
   const embed = new Discord.RichEmbed()
  .setColor("#36393F")
   .setDescription('Yazıyor Başladı')
  return message.channel.send(embed);
    }


module.exports.help = {
  name: 'yazıyorbaşlat',
};