# Entorno-de-desarrollo

## S.O. - Ubuntu 14.04.02 LTS

```cmd
sudo apt update && upgrade
sudo apt-get install nautilus-open-terminal
sudo apt-get install build-essential
```

## Componentes

- [Vivaldi](https://vivaldi.com)

vivaldi_TP4.1.0.219.50-1_amd64.deb

- [Atom.io](https://atom.io)

atom-amd64.deb

- [node.js](https://nodejs.org)

node-v0.12.7.tar.gz

```cmd
./config
make
sudo make install
```
o
```cmdnder
add-apt-repository ppa:richarvey/nodejs
apt-get update
apt-get install nodejs npm
```

- [COLT](http://codeorchestra.com)

colt-linux.tar.gz

- [Yeoman](http://yeoman.io/), [bower](http://bower.io/), [grunt](http://gruntjs.com/)

```cmd
npm install -g yo bower grunt-cli gulp
```

- [MongoDB](MongoDB.md)

- [robomongo](http://robomongo.org/)

robomongo-0.8.5-x86_64.deb

- [RethinkDB](http://rethinkdb.com)

```cmd
echo "deb http://download.rethinkdb.com/apt `lsb_release -cs` main" | sudo tee /etc/apt/sources.list.d/rethinkdb.list
wget -qO- http://download.rethinkdb.com/apt/pubkey.gpg | sudo apt-key add -
sudo apt-get update
sudo apt-get install rethinkdb
```

Navegador: [http://localhost:8080/](http://localhost:8080/)

- [genymotion](https://www.genymotion.com)

genymotion-2.5.2_x64.bin

Requisito:
Instalar virtualbox y [registrarse](https://www.genymotion.com/#!/auth/signin)

```cmd
sudo apt-get install virtualbox
```

vamos a abrir la terminal y a mover el archivo de la carpeta donde se haya descargado a la carpeta opt:


```
# mv genymotion-2.2.2_x64.bin /opt/
```

Le damos permisos de ejecución:

```cmd
# chmod +x genymotion-2.2.2_x64.bin
```

Lo ejecutamos:

```cmd
# ./genymotion-2.2.2_x64.bin
```

Nos sale el siguiente mensaje:

```
Installing to folder [/opt/genymotion]. Are you sure [y/n] ?
```
Aceptamos (y) y listo. Comenzará la instalación y en cuestión de segundos estará todo listo.


-----

## Generadores

- [node-webkit](https://github.com/Dica-Developer/generator-node-webkit)

```cmd
npm install -g generator-node-webkit
```

- [electron](https://github.com/sindresorhus/generator-electron)

```cmd
npm install --global generator-electron
```
