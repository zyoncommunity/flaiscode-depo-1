client.on('message', msg => {
if (msg.content.toLowerCase() === prefix + "ping") {
msg.channel.send('Olm ölçmedimki dur ölçim')
.then(nmsg => nmsg.edit(`Ping: ${Math.round(client.ping)}ms!`));
}
});