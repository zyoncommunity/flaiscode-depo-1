const Discord = require('discord.js');
const ayarlar = require('../ayarlar.json');
var Jimp = require('jimp');

let using = false;

exports.run = (client, message, params) => {
  if(using) return message.channel.send('Bu komudu şu an başkası kullanıyor. Lütfen daha sonra tekrar deneyin.');
  if(params[0]) if(params[0] === 'sunucu-ikon'){
    if(!message.guild) return message.channel.send('Bu sadece sunucularda kullanılabilir.');
    if(!message.guild.iconURL) return message.channel.send('Bu sunucunun ikonu yok.');
    using = true;
    Jimp.read(message.guild.iconURL, function (err, image){
        if(err) return message.channel.send('Bir hata oluştu: ``'+err+'``\n Lütfen yapımcıya bildirin.');
        image.invert().write('foto.png');
        setTimeout(() => {
          message.channel.sendFile('foto.png');
          using = false;
        }, 500);
    });
    return;
  }
  if(message.mentions.users.first()) {
      using = true;
      Jimp.read(message.mentions.users.first().avatarURL, function (err, image){
          if(err) return message.channel.send('Bir hata oluştu: ``'+err+'``\n Lütfen yapımcıya bildirin.');
          image.invert().write('foto.png');
          setTimeout(() => {
            message.channel.sendFile('foto.png');
            using = false;
          }, 500);
      });
  } else{
    using = true;
    Jimp.read(message.author.avatarURL, function (err, image){
        if(err) return message.channel.send('Bir hata oluştu: ``'+err+'``\n Lütfen yapımcıya bildirin.');
        image.invert().write('foto.png');
        message.channel.sendFile('foto.png');
        using = false;
    });
  }
};

exports.conf = {
  enabled: true,
  guildOnly: false,
  aliases: [],
  permLevel: 0
};

exports.help = {
  name: 'invert',
  description: 'Avatarın renklerini ters çevirir.',
  usage: 'invert [@<kişi ismi>]'
};