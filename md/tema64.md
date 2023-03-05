![Logo Pure-FTP](img/pure-ftpd.png)

# Instalación

Primeramente, actualizaremos los repositorios del sistema con el comando:

```console
sudo apt update
```

Ahora actualizamos los paquetes con:

```console
sudo apt upgrade
```

Después de actualizar, utilizamos el siguiente comando para instalar el servicio Pure-FTP.

```console
sudo apt install pure-ftpd
```

# Usuario anónimo

Para añadir un usuario anónimo, utilizamos el siguiente comando:

> sudo adduser ftp --shell /sbin/nologin --home /var/ftp

Para permitir el inicio de sesión de usuarios anónimos, hay que cambiar una directiva que se encuentra en el directorio */etc/pure-ftpd/conf/*.

Tenemos las siguientes directivas:

La directiva a cambiar es *NoAnonymous*. Para ello usamos el siguiente comando:

```console
sudo nano /etc/pure-ftpd/conf/NoAnoymous
```

Seguidamente, establecemos su valor en *no*.

Después, creamos la directiva *AnonymousCantUpload* para que los usuarios anónimos no puedan escribir, pero sí leer. Para ello, usamos el siguiente comando:

```console
sudo nano /etc/pure-ftpd/conf/AnonymousCantUpload
```

Y establecemos su valor en *yes*.

Por último, reiniciamos el servicio con el siguiente comando:

!!!warning "Para aplicar los cambios reiniciamos el servicio"
    sudo systemctl restart pure-ftpd

# Usuarios locales

Para permitir el inicio de sesión de los usuarios locales, abrimos la directiva *PAMAuthentication* con el siguiente comando:

```console
sudo nano /etc/pure-ftpd/conf/PAMAuthentication
```

Seguidamente, establecemos su valor en *yes*.

Después, reiniciamos el servicio con el siguiente comando:

!!!warning "Para aplicar los cambios reiniciamos el servicio"
    sudo systemctl restart pure-ftpd

# Usuarios virtuales

Para crear usuarios virtuales, necesitamos un usuario local que haga de intermediario entre el sistema y los usuarios virtuales. Para ello, añadimos un grupo de usuarios y lo nombramos, por ejemplo, *virtualesftp*. Usaremos el siguiente comando:

```console
sudo groupadd virtualesftp
```

Seguidamente añadimos el usuario, al que vamos a nombrar *virtualftp*, con el siguiente comando:

```console
sudo useradd -g virtualesftp -d /dev/null -s /sbin/nologin virtualftp
```

Ahora, crearemos el directorio del usuario virtual con el siguiente comando:

```console
sudo mkdir /home/virtualesftp
sudo mkdir /home/virtualesftp/esteban
```

Después, creamos el usuario virtual con el siguiente comando:

```console
sudo pure-pw useradd esteban -u virtualftp -d /home/virtualesftp/esteban
```

Seguidamente, generamos la base de datos de Pure con el siguiente comando:

```console
sudo pure-pw mkdb
```

Creamos los accesos directos a los ficheros generados con los siguientes comandos:

```console
sudo ln -s /etc/pure-ftpd/pureftpd.passwd /etc/pureftpd.passwd
sudo ln -s /etc/pure-ftpd/pureftpd.pdb /etc/pureftpd.pdb
sudo ln -s /etc/pure-fptd/conf/PureDB /etc/pure-ftpd/auth/PureDB
```

Por último, cambiamos el propietario de los directorios de los usuarios virtuales y reiniciamos el servicio con los siguientes comandos:

```console
sudo chown -hR virtualftp:virtualesftp /home/virtualesftp/
```

!!!warning "Para aplicar los cambios reiniciamos el servicio"
    sudo systemctl restart pure-ftpd


# Mensajes

Si se desea crear un mensaje personalizado para cada usuario, crearemos el fichero *.banner* dentro de su directorio por defecto. En este fichero escribimos el mensaje que desea mostrar. Por ejemplo, si deseamos crear un mensaje para el usuario local *pedro*, usamos el siguiente comando:

```console
sudo nano /home/pedro/.banner
```

Dentro de este fichero, escribiremos, por ejemplo: *Bienvenido al servidor FTP, Pedro*.

