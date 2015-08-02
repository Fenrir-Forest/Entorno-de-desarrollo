Instalar MongoDB en nuestro sistema Ubuntu es muy sencillo y rápido, en aproximadamente dos minutos podremos estar trabajando con nuestros datos.

Quiero recordar que siempre es recomendable realizar la instalación utilizando los paquetes (.deb) del propio repositorio de MongoDB y no los de Ubuntu. El motivo es bien sencillo, al usar los de MongoDB nos aseguramos que son los más actualizados.

¿Qué paquetes componen una distribución?

- mongodb-org – Este paquete instalará automáticamente los paquetes restantes.

- mongodb-org-server – Contiene el demonio mongod, la configuración asociada y scripts de inicialización. Es el proceso que se encarga del funcionamiento de las tareas propias de la base de datos. Estará presente en cada máquina en la que corra la base de datos, ya sea en una máquina aislada o como parte de una Replica Set.

- mongodb-org-mongos – Contiene el demonio mongos. Este proceso será necesario en el caso de que en nuestra instalación tengamos un Sharded Cluster. Es el responsable de enrutar las peticiones del cliente a la máquina que contiene los datos solicitados y, también, de devolverlos. Es capaz, incluso, de realizar algunas operaciones sobre ellos antes de hacerlos llegar al cliente.

- mongodb-org-shell – Paquete que contiene la mongo shell con la que nos conectamos a la base de datos, para tareas administrativas fundamentalmente.

- mongodb-org-tools – Conjunto de utilidades que permiten: exportar pequeñas cantidades de datos a fichero (mongoexport), importar datos desde fichero (mongoimport), hacer backups (mongodump), restaurar backups (mongorestore), comprobar el estado de una instancia (mongod o mongos), etcétera.

Veamos ahora los pasos a seguir para realizar la instalación, son estos:

1. Importamos la clave pública de MongoDB

Esta clave es necesaria para que el gestor de paquetes de Ubuntu compruebe la consistencia y autenticidad requerida a los paquete

```cmd
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
Executing: gpg --ignore-time-conflict --no-options --no-default-keyring --homedir /tmp/tmp.nG6OPIkakq --no-auto-check-trustdb --trust-model always --keyring /etc/apt/trusted.gpg --primary-keyring /etc/apt/trusted.gpg --keyring /etc/apt/trusted.gpg.d/gnome-terminator-ppa.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
gpg: solicitando clave 7F0CEB10 de hkp servidor keyserver.ubuntu.com
gpg: clave 7F0CEB10: clave pública "Richard Kreuter <richard@10gen.com>" importada
gpg: Cantidad total procesada: 1
gpg: importadas: 1 (RSA: 1)
```

2. Generamos un fichero que contendrá la url del repositorio de MongoDB

```cmd
$ echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen
```

3. Refrescamos la base de datos local de paquetes

```cmd
$ sudo apt-get update
```

4. Instalamos la última versión estable de MongoDB, y todos los paquetes necesarios, en nuestro sistema

```cmd
$ sudo apt-get install mongodb-org

Leyendo lista de paquetes... Hecho
Creando árbol de dependencias
Leyendo la información de estado... Hecho
Se instalarán los siguientes paquetes extras:
  mongodb-org-mongos mongodb-org-server mongodb-org-shell mongodb-org-tools
Se instalarán los siguientes paquetes NUEVOS:
  mongodb-org mongodb-org-mongos mongodb-org-server mongodb-org-shell
  mongodb-org-tools
0 actualizados, 5 se instalarán, 0 para eliminar y 11 no actualizados.
Necesito descargar 114 MB de archivos.
Se utilizarán 289 MB de espacio de disco adicional después de esta operación.
¿Desea continuar? [S/n]
```

5. En este momento ya tenemos nuestra instancia local de MongoDB corriendo, podemos comprobarlo de la siguiente manera

```cmd
$ ps -ef | grep mongo
mongodb   1299     1  2 20:36 ?        00:00:01 /usr/bin/mongod --config /etc/mongod.conf
```

¿Cuáles son los directorios donde MongoDB guarda los fuentes, los log y nuestros datos?

- Fuentes: /usr/bin/
- Logs: /var/log/mongodb/mongod.log
- Datos: /var/lib/mongodb/
- Debemos asegurarnos de que el usuario con el que ejecutamos la base de datos tiene acceso a estos directorios.

A través del fichero /etc/mongod.conf, MongoDB nos permite modificar algunos parámetros tales como:

- IP utilizada por defecto: 127.0.0.1
- Puerto en el que escucha MongoDB por defecto: 27017
- Directorio donde guarda los ficheros de datos
- Directorio donde guarda los ficheros de log
- Si utilizamos o no journaling
- Nombre de la Replica Set
- Tamaño del oplog
- Etcétera

¿Cómo compruebo qué versión se ha instalado?

```cmd
$ mongo --version
MongoDB shell version: 2.6.3
```

¿Cómo abrimos una shell de MongoDB?

```cmd
$ mongo
MongoDB shell version: 2.6.3
connecting to: test
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see http://docs.mongodb.org/
Questions? Try the support group http://groups.google.com/group/mongodb-user

>
```

Si lo necesitamos, también podemos instalar una versión concreta de MongoDB. Para ello hemos de especificar uno a uno los distintos paquetes y su versión. Veamos cómo se haría para la versión 2.6.1

```cmd
$ apt-get install mongodb-org=2.6.1 mongodb-org-server=2.6.1 mongodb-org-shell=2.6.1 mongodb-org-mongos=2.6.1 mongodb-org-tools=2.6.1
```

Las versiones pares, en su segundo dígito, son estables ( 2.4.0, 2.4.1,…). Las impares son versiones en desarrollo (2.5.0,…) y no deben usarse en producción. Para entornos de producción siempre elegiremos una versión de 64 bits.

Ahora que ya tenemos instalado MongoDB en nuestro sistema es hora de recordar:

Cómo arrancamos el servicio de mongo

```cmd
$ sudo service mongod start
```

Cómo paramos el servicio

```cmd
$ sudo service mongod stop
```

Cómo refrescamos el servicio

```cmd
$ sudo service mongod restart
```

En el siguiente capítulo mostraremos los conceptos básicos para poder comenzar a utilizar nuestra base de datos.
