client.on('guildCreate', async guild => {
  const girismesaj = [
    'Botum sunucunuza eklendi.',
    'Bu bot **X** tarafından geliştirilmektedir.',
    'Yazı-1',
    'Yazı-2',
    'Yazı-3',
    'Yazı-4',
  ]
  guild.owner.send(girismesaj)
  console.log(`LOG: ${guild.name}. sunucuya katıldım!`);
})