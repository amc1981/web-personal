---
layout: post
title: Servicios en Linux
date: 2023-08-08 00:51 +0200
description:
image: "/assets/img/blog/linux-services-detail.png"
category: devops
tags:
- apuntes
- linux
curso: the-complete-devops-bootcamp
author: Antonio
---
* Table fo content
{:toc}

Los **servicios** en Linux son programas y/o herramientas diseñados para correr
24x7 en nuestros servidores. Queremos que estos programas se arranquen con
el inicio del servidor y que en caso de caída del programa o del
servidor, se recuperen automáticamente, además suelen ser ser arrancados en orden concreto por tener
a veces dependencias unos de otros.

## Manejo básico de los servicios

Disponemos de dos comandos, el genérico `service` y el mejorado
`systemctl`. En realidad `service` está utilizando `systemctl` por
debajo. En este documento utilizaremos este último, pero son
intercambiables (Cada uno con su sintáxis específica).

```bash
# Arrancar un servicio (httpd sería un Servidor Apache)
$ systemctl start httpd 

# Parar un servicio
$ systemctl stop httpd 

# Chequear el estado de un servicio
$ systemctl status httpd 

# Habilitar un servicio para que arranque en el inicio del servidor
$ systemctl enable httpd 

# Deshabilitar un servicio para que NO arranque en el inicio del servidor
$ systemctl disable httpd 
```

## Crear un servicio

En ocasiones tendremos que configurar manualmente los servicios, otras
veces se configuran automáticamente en la instalación del software. Aquí
explicaremos la configuración manual de servicios.

Digamos que tenemos un sencillo servidor web escrito en python en la
ruta `/opt/code/my_app.py`, de modo que si lo arrancamos con el
interprete de *Pyton*(`/usr/bin/python3`) y hacemos un
`curl http//localhost:5000`, nos debe devolver un HTTP Response 200.

Con esta premisa vamos a configurarlo como un servicio para que se
arranque en el inicio del servidor y la gestión de parada y arranques
manuales sean tan sencillas como ejecutar:

```bash
$ systemctl start my_app
$ systemctl stop my_app
```

Como vimos al principio el comando `systemctl` se emplea para manejar
los servicios del sistema, así pues debemos configurar nuestro programa
como un servicio más.

Por lo general los ficheros de los servicios están almacenados en la
ruta `/etc/systemd/system`. En dicha ruta crearemos nuestro fichero con
el nombre que queramos darle a nuestro servicio, en nuestro caso será
`my-app` y la extensión del fichero debe ser `.service`. Veamos como
queda el fichero por dentro:

```bash
# file: "my-app.service"
[Service]
ExecStart=/usr/bin/python3 /opt/code/my-app.py
```

- `ExecStart` es el comando que ejecutaríamos en el *CLI* para
    arrancar el programa normalmente.

Con esto tendríamos nuestro servicio configurado. Ahora debemos ejecutar
`systemctl daemon-reload` para hacer que el sistema incorpore este nuevo
fichero como servicio del sistema. Ya podemos manejarlo como un servicio
más en nuestro sistema:

```bash
$ systemctl start my-app
$ systemctl status my-app
$ systemctl stop my-app
```

## Configurar un servicio para arrancar al inicio del sistema

Ya tenemos el servicio configurado y corriendo. Ahora queremos que se
levante automáticamente en el inicio del sistema. Para ello debemos
añadir una nueva sección en nuestro fichero `my-app.service`, llamada
`[Install]`. Contendrá lo siguiente:

```bash
# file: "my-app.service"
[Service]
ExecStart=/usr/bin/python3 /opt/code/my-app.py

[Install]
WantedBy=multi-user.target
```

### Configuraciones adicionales

Podemos definir en el fichero `my-app.service` otras configuraciones
tales como: definición del servicio, dependencias con otros servicios o
si queremos que se reinicie automáticamente en caso de caida del mismo.

Añadimos estas líneas a nuestro fichero y posteriormente explicamos los
nuevos campos.

```bash
# file: "my-app.service"
[Unit]
Description=My python web application

[Service]
ExecStart=/usr/bin/python3 /opt/code/my-app.py
ExecStartPre=/opt/code/configure_db.sh
ExecStartPost=/opt/code/email_status.sh
Restart=Always

[Install]
WantedBy=multi-user.target
```

- *Description*: Dentro de la sección `[Unit]`, añadimos este campo
    para añadir una breve descripción de lo que hace el servicio. Será
    mostrada cuando hagamos un `systemctl status my-app`.

- *ExecStartPre*: Dependencias que deben cumplirse antes de que
    nuestro servicio arranque. En este caso debe haberse ejecutado el
    script `configur_db.sh`.

- *ExecStartPost*: Programas que se ejecutarán tras el arranque
    correcto de nuestro serivicio. En el ejemplo `email_status.sh`.

- *Restart*: Si queremos que nuestro servicio se reinicie
    automáticamente en caso de caída del mismo tenemos que definir este
    campo con `Always`.

Estas son algunas de las configuraciones básicas que podemos incluir en
nuestros servicios. Por lo general con otros programas y herramientas
suelen ser fichero mucho más extensos y con muchos más campos. Pero para
entender el funcionamiento básico de los servicios en Linux es
suficiente con este ejemplo.

