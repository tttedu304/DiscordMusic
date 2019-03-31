# MyBot Music

Un npm enfocado directamente a la comunidad de MyBot, para que los usuarios puedan crear un sistema de música de una manera muy sencilla, disfruten, por parte de su amigo tttedu304#7823 y Aiden#1326

![Online Members](https://discordapp.com/api/guilds/312846399731662850/embed.png)
![Version](https://img.shields.io/npm/v/mybot-music.svg?maxAge=3600)
![Download](https://img.shields.io/npm/dt/mybot-music.svg)
![License](https://img.shields.io/npm/l/mybot-music.svg)
![Dependencies](https://david-dm.org/tttedu304/mybot-music.svg)
![Build](https://api.travis-ci.org/tttedu304/mybot-music.svg)

## COMO USAR?
##### DESCARGAR PACKAGE

```
npm i mybot-music
```

##### DEFINIR PACKAGE
```javascript
let Music = require("mybot-music");
let Discord = require("discord.js");
let client = new Discord.Client();
```

##### USANDO EL PACKAGE

```javascript
/* Dentro del evento ready */
client.music = new Music.session();
```

### COMANDOS
##### Play
```javascript
/* DENTRO DEL EVENTO MESSAGE */
if(message.content.startsWith("/play")) {
	try {

		let song = await Music.play(client, message, args);
		/*Un texto de ejemplo para conseguir informacion del video
		La funcion play devuelve este objeto
		vid: id del video,
		tmp: duracion del video
		tit: titulo del video
		sec: segundos que dura el video
		cid: el que pidio la cancion
		addedAs: como fue agregada la cancion, esto es para la funcion lyrics
		 */
		let embed = new Discord.RichEmbed()
		.setDescription(`Titulo de la cancion: ${song.title}, Duracion: ${song.tmp}, Pedido por: <@${song.cid}>`)
		message.channel.send(embed);
	} catch (err) {
		
		console.log(err)
		message.channel.send("Un error ha ocurrido")
		
	}
}
```
##### Pause
```javascript
/* DENTRO DEL EVENTO MESSAGE */
if(message.content.startsWith("/pause")){
	try{
		await Music.pausar(client, message)
	}catch(err){
		console.log(err)
		message.channel.send("Ocurrio un error")
	}
}

```
##### Skip
```javascript
/* DENTRO DEL EVENTO MESSAGE */
if(message.content.startsWith("/skip")){
	try {
		await Music.skip(client, message)
	}catch(err){
		console.log(err)
		message.channel.send("Ocurrio un error")
	}
}
```
##### Lyrics
```javascript
/* DENTRO DEL EVENTO MESSAGE */
if(message.content.startsWith("/lyrics")){
	try {
		if(!args[0] && client.music[message.guild.id].rep){
			args = client.music[message.guild.id].queue[0].addedAs.split(/ +/g)
		}
		let song = await Music.lyrics(client, args, "Llave de acceso de Weez")
		//Esto devuelve un objeto song el cual tiene los siguientes valores:
		/*
		song.letra <-- Lyrics de la cancion
		song.imagen <-- Link de la imagen
		Ejemplo de uso:
		*/
		let lyricsEmbed = new Discord.RichEmbed()
		.setDescription(song.letra)
		.setThumbnail(song.imagen);
		message.channel.send(lyricsEmbed)
	}catch(err){
		console.log(err)
		message.channel.send("Ocurrio un error")
	}
}
```
##### Leave
```javascript
/* DENTRO DEL EVENTO MESSAGE*/
if(message.content.startsWith("/leave")){
	try {
		await Music.leave(client, message)
	}catch(err){
		console.log(err)
		message.channel.send("Ocurrio un error")
	}
}
```
##### Resume
```javascript
/* DENTRO DEL EVENTO MESSAGE*/
if(message.content.startsWith("/resumir")){
	try {
		await Music.resume(client, message)
	}catch(err){
		console.log(err)
		message.channel.send("Ocurrio un error")
	}
}
```
##### Queue
```javascript
if(message.content.startsWith("/queue")) {
	try {
		let queue = await Music.queue(client, message);
		let str = "";
		for(let i = 0; i < queue.length; i++) {
			let x = queue[i];
			str += `\n\nNombre De La Cancion: ${x.tit}, Duracion: ${x.tmp}, Pedido por ${client.users.get(x.cid).username}, [Url](https://www.youtube.com/watch?v=${x.vid})`
		}
		let embed = new Discord.RichEmbed()
			.setDescription(str);
		message.channel.send(embed)
	} catch (err) {
		console.log(err)
		message.channel.send("Ocurrio un error")
	}
}
```
##### Np 
```javascript
if(message.content.startsWith("/np")){
	try{
		let np = await Music.np(client, message)
		let npEmbed = new Discord.RichEmbed()
			.setTitle(np.tit)
			.setDescription(`Se esta reproduciendo ${np.tit} pedido por <@${np.cid}>`)
			.setFooter(np.tmp);
		message.channel.send(npEmbed)
	}catch(err){
		console.log(err)
		message.channel.send("Ocurrio un error")
	}
}
```
#### Se agregaran más comandos y funciones progresivamente, de momento, esto es la fase beta, Siguiente objetivo: Conseguir la informacion de los videos de las canciones para asi tener un embed
### Si necesitan la llave de acceso y no saben conseguirla, [Click Me](https://weez.pw/panel)
# Si necesitan ayuda no duden en preguntar en [MyBOT Team](https://discord.gg/g6ssSmK)

