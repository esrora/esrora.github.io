# Introducción

Es un servicio que usa un protocolo con el mismo nombre, FTP, File Transfer Protocol, protocolo de transferencia de fichero.

Permite transferir ficheros de forma entre servidor y cliente.

Los puertos que usa por defecto son el 20, 21, 22, 69 y mayores del 1024, todos según el tipo FTP, FTPS, SFTP o TFTP.

# TFTP

Trivial File Transfer Protocol es el más simple de todos
- Usa el protocolo UDP, puerto 69.
- No usa autenticación, ni cifrado
- No permite listar contenido de los directorios

Es decir, un servidor abre su puerto 69 por UDP y el cliente solicita un fichero al servidor por ese puerto sin necesidad de usuario y contraseña.

# SFTP

SSH File Transfer Protocol este servicio va ligado al servidor SSH visto en temas anteriores, usa toda la seguridad que ofrece el servicio SSH para la transferencia segura de ficheros entre servidor y cliente.

Usa el protocolo TCP y el puerto 22 al igual que el servicio SSH, las formas de acceso son las mismas que el servicio SSH.

# FTPS

Este caso es la unión entre el protocolo FTP y SSL/TLS, algov parecido a lo que ocurría en el tema anterior con HTTPS.

Usa el puerto 21 y el protocolo TCP para comenzar la comunicación sin protección ninguna (igual que el FTP tradicional) y a partir de ahí pide que se use TLS para el resto de la comunicación.

Es decir, igual que el FTP en todo excepto en la transferencia de información que será cifrada.

# FTP y sus características

Este es el servicio básico en el que nos vamos a centrar por su popularidad, sobretodo en la WWW. Su uso fundamental es la transferencia de los sitios web desde la máquina del desarrollador al servidor web o HTTP.

- Usa el puerto 20, 21 y los mayores al 1024 por TCP.
- Transferencia de datos rápida.
- Multiplataforma, independiente de S.O. o sistema de ficheros.
- Poco seguro, ya que todo se transfiere sin cifrar.