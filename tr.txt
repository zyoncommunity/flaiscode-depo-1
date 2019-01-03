if (command === "tr") {
        var user = message.mentions.users.first() || message.author;
        if (!message.guild) user = message.author;
        message.channel.send(`:timer:  | Fotoğraf işleniyor, lütfen bekleyin.`).then(m => m.delete(3000));

        Jimp.read(user.avatarURL, (err, image) => {
            image.resize(295, 295)
        
            Jimp.read("http://bilgitivi.com/wp-content/uploads/2017/01/maxresdefault-4.jpg", (err, avatar) => {
                avatar.resize(295, 295)
                avatar.opacity(0.3);
                image.composite(avatar, 1, 0).write(`./img/wasted/${client.user.id}-${user.id}.png`);
                setTimeout(function() {
                    message.channel.send(new Discord.Attachment(`./img/wasted/${client.user.id}-${user.id}.png`));
                }, 1000);
            });
        });
    }  