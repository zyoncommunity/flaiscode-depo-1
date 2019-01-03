const Discord = require("discord.js");
var Jimp = require('jimp');

exports.run = async (client, message, args) => {
    var user = message.mentions.users.first() || message.author;
    if (!message.guild) user = message.author;
    const load = (client.emojis.find("name", "ORALETloading").toString())
    message.channel.send(`${load} | Fotoğraf işleniyor, lütfen bekleyin.`).then(m => m.delete(1000));

Jimp.read('https://www.mailce.com/wp-content/uploads/2013/02/Kasl%C4%B1-erkek-9.jpg', (err, image) => {
    image.resize(310, 325)
    //image.greyscale()
    //image.gaussian(3)
    Jimp.read(user.avatarURL, (err, avatar) => {
        avatar.resize(100, 100)
        image.composite(avatar, 95, 5).write(`./img/snip/${client.user.id}-${user.id}.png`);
        setTimeout(function() {
            message.channel.send(new Discord.Attachment(`./img/snip/${client.user.id}-${user.id}.png`));
        }, 1000);
    });

});
}
exports.conf = {
 enabled: true,
 guildOnly: false,
 aliases: [],
 permLevel: 0
};

exports.help = {
 name: 'kaslı',
 description: 'masıyosun broteini buf buf',
 usage: 'kaslı'
};