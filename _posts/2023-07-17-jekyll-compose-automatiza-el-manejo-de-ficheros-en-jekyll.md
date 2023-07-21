---
layout: post
title: 'jekyll-compose: Automatiza el manejo de ficheros en Jekyll'
date: 2023-07-16 17:44 +0200
author: Antonio
description: Optimice su escritura en Jekyll con estos comandos. Crear, publicar y renombrar posts y borradores a través de la línea de comandos.
category: blogging
tags:
- jekyll
- how-to
- jekyll-plugins
---
1. Table of contents
{:toc}

jekyll-compose es un plugin que nos facilita labor de creación de borradores, publicación de los mismos y creación de páginas en nuestro proyecto de Jekyll. Otra utilidad es el renombrado de los ficheros y a su vez del título de nuestras entradas en el blog. 

## Instalación

Varía un poco con respecto a la [documentación oficial](https://github.com/jekyll/jekyll-compose){:target="_blank"}

Modificamos el fichero `Gemfile`, como se indica en la documentación:

~~~bash
$ gem 'jekyll-compose', group: [:jekyll_plugins]
~~~

Pero el segundo paso de la instalación, no es suficiente con el comando `bundle` en nuestro local. Acabamos instalando directamente así:

~~~bash
$ gem install jekyll-compose
~~~

## Configuración

Tenemos que hacer dos cosas: abrir automáticamente los nuevos borradores o posts que creemos y configurar los campos que se creareán automáticamente en el `Front-matter` de nuestros archivos.

### Abrir automáticamente los ficheros

Tenemos  que añadir estas líneas en nuestro `_config.yaml`

~~~yaml
  jekyll_compose:
    auto_open: true
~~~

Tenemos que configurar también la variable de entorno JEKYLL_EDITOR en nuestro entorno. En Git bash ejecutaremos:

~~~bash
$ export JEKYLL_EDITOR=vscode
~~~

### Configurar los campos por defecto en el `Front Matter` de cada nuevo fichero

Añadiremos los siguiente en el `_config.yaml`

~~~yaml
jekyll_compose:
  default_front_matter:
    drafts:
      description:
      image:
      category:
      tags:
    posts:
      description:
      image:
      category:
      tags:
      published: false
      sitemap: false
~~~

Rellenaremos cada valor una vez empezemos a editar el post.

## Principales usos

Según la documentación la lista es más extensa, pero aquí lo utilizaremos principalmente para los siguientes cometidos: crear y renombrar borradores, publicar dichos borradores en la carpeta `_posts` y crear nuevas páginas.

### Crear nuevo borrador

Empezaremos creando un borrador. Hay varios métodos pero el ejemplo de hoy usaremos el siguiente:

~~~bash
$ bundle exec jekyll compose "My new draft" --draft
Configuration file: C:/Users/Antonio/PROYECTOS/Web-Personal/web-personal/_config.yml
New draft created at _drafts/my-new-draft.md
~~~

Esto crea un fichero llamado `my-new-draft.md` en la carpeta `_drafts`. El contenido inicial del fichero estará condicionado por la configuración que hayamos definido en el fichero `_config.yaml` al respecto de los campos por defecto en el Front Matter. En nuestro caso aparece lo siguiente:

<img src="/assets/img/blog/front-matter-on-first-draft.png" title="" alt="Detail of default front matter">

Como se ve en la imagen, el título que lo hemos dado en los parámetros del comando, la plantilla `post` y la fecha de creación que se generan automáticamente ya están rellenos. Nos queda por rellenar el resto de campos por defecto.

#### Renombrar un borrador o un post

Usando el subcomando `rename` le pasaremos como argumentos la ubicación y al nombre del fichero actual y seguido, entre comillas el nuevo nombre del mismo.

~~~bash
$ bundle exec jekyll rename _drafts/utilizando-jekyll-compose.md "Aprendiendo a manejar Jekyll compose"
Configuration file: C:/Users/Antonio/PROYECTOS/Web-Personal/web-personal/_config.yml
Draft _drafts/utilizando-jekyll-compose.md was moved to _drafts/aprendiendo-a-manejar-jekyll-compose.md
~~~

Estamos por tanto cambiando el nombre del fichero y el campo `title` en el `Front Matter` del mismo.


### Publicar borrador

El último paso con respecto a los borradores y los posts sería la publicación. Es decir, mover el fichero de la carpeta `_drafts` a la carpeta de publicación `_posts`. Para ello ejecutaremos el subcomando `publish` de la siguiente manera:

~~~bash
bundle exec jekyll publish _drafts/aprendiendo-a-manejar-jekyll-compose.md
Configuration file: C:/Users/Antonio/PROYECTOS/Web-Personal/web-personal/_config.yml
Draft _drafts/aprendiendo-a-manejar-jekyll-compose.md was moved to _posts/2023-07-17-aprendiendo-a-manejar-jekyll-compose.md 
~~~

Se puede observar en la salida del comando que se ha añadido como sufijo la fecha en la que se ha ejecutado el mismo en formato `AAAA-MM-DD`, dando así el formato estandar para el nombre de los posts en Jekyll.

Existen variaciones de este mismo comando, añadiendo el parámetro `--date`, y con el mismo formato que vemos en este ejemplo, pondríamos la fecha de publicación que deseamos que aparezca, evitando así que nos auto asigne la fecha del día en curso.

### Crear nueva página

Usaremos el ejemplo de la página `courses.html` que en un futuro albergará un listado de posts referidos a la colección del mismo nombre. 

~~~bash
$ bundle exec jekyll page -s "./blog" "courses" -x html
Configuration file: none
New page created at ./blog/courses.html 
~~~

El comando necesita 3 parámetros:

- `-s` o `--source`, que indicará la carpeta donde queremos que se cree el fichero
- El nombre del fichero entre comillas.
- `-x` o `--extension`, que indicará la extensión del fichero a crear




## Recursos:

[Proyecto jekyll-compose en Github](https://github.com/jekyll/jekyll-compose){:target="_blank"}

