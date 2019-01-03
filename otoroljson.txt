const fs = require("fs");
const Discord = require("discord.js");

exports.run = async (client, message, args) => {
    if (!message.member.hasPermission("MANAGE_ROLES")) return message.reply("Bu Komutu Kullanmak İçin `Rolleri Yönet` Yetkisine sahip olmalısın.");
    let otorol = JSON.parse(fs.readFileSync("./sunucuyaözelayarlar/otorol.json", "utf8"));
    if (!args[0]) { 
        otorol[message.guild.id] = {
            role: 0
        };
        fs.writeFile("./sunucuyaözelayarlar/otorol.json", JSON.stringify(otorol), (err) => {
            if (err) console.log(err);
        });
        message.reply("Lütfen bir rol ismi yazın.");
   }
    if (args[0]) { 
        let roles = args.join(" ");
        let role = message.guild.roles.find("name", roles);
        otorol[message.guild.id] = {
            role: role.id
        };
        fs.writeFile("./sunucuyaözelayarlar/otorol.json", JSON.stringify(otorol), (err) => {
            if (err) console.log(err)
        });
        message.reply(`Otorol Ayarlandı: **${role.name}**`);
    }
}

exports.conf = {
 enabled: true,
 guildOnly: false,
 aliases: ['otorol', 'oto-rol', 'oto-rol-ayarla'],
 permLevel: 0
};

exports.help = {
 name: 'Otorol',
 description: '',
 usage: ''
};               

// eklemeyi unutmayın sunucuyaözelayarlar/otorol.json 

// bot.js

client.on("guildMemberAdd", member => {
    let otorol = JSON.parse(fs.readFileSync("./sunucuyaözelayarlar/otorol.json", "utf8"));
  
    var role = otorol[member.guild.id].role;
  const rol = member.guild.roles.find('name', role);
    if (!rol)
    member.addRole(role);
});