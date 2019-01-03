const Discord = require("discord.js");

module.exports.run = async (client, message, args) => {



    let youtube = args.slice(0).join('+');

        let link = `https://www.youtube.com/results?search_query=` + youtube;
        if(!youtube)return message.reply(`Youtubeda Aratmak İStediğini Yazarmısın`)
        if(!link)return message.reply("Error Hata 404")
        let embed = new Discord.RichEmbed()
 
         
     .setColor("RED")
         
          .setTimestamp()
        
          .addField('Aranıyor:', `${args.slice(0).join(' ')}`)

          .addField("Yazı:", `${args.slice(0).join(' ')}`)

          .addField('Link:', `${link}`)
         
          .setFooter("YouTube", message.author.avatarURL);
          
              message.channel.send(embed);
              message.author.send(`YouTube Bulunan ${link} | ${ message.guild.name}`);

        
    
}



exports.conf =
{
  aliases: [""]
}

exports.help =
{
    name: 'youtube',
    description: 'YouTube Search',
    usage: 'youtube'
}