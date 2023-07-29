---
layout: post
title: 'jekyll-feed: plugin para crear un fichero de feeds'
date: 2023-07-17 12:35 +0200
description: Un plugin de Jekyll para generar un feed Atom (tipo RSS) de sus publicaciones de Jekyll.
image: /assets/img/blog/blog-on-feedly.png
category: blogging
tags:
- jekyll
- jekyll-plugins
- how-to
author: Antonio
---
1. Tabla de contenidos
{:toc}

jekyll-feed es un plugin que automatiza la generación de un fichero de feed en nuestro proyecto de Jekyll.

## Instalación

Como en ejemplos anteriores de otros plugins, añadimos la gema a nuestro fichero `Gemfile` y ejecutamos el comando `bundle`

~~~ruby
# file: "Gemfile"
gem 'jekyll-feed'
~~~

Posteriormente añadimos a nuestro fichero de configuración `_config.yaml` la correspondiente línea refiriendose al plugin:

~~~yaml
# file: "_config.yml"
plugins:
  - jekyll-feed
~~~

Simplemente con estos dos pasos ya se genera automáticamente un fichero `/feed.xml` colgando del raíz de nuestro proyecto.

## Configuración

Adjuntamos a continuación las líneas referentes a la configuración del plugin en el fichero `_config.yaml`.

~~~yaml
# file: "_config.yml"
# Jekyll-feed configuration

feed:
  path: /blog/feed.xslt.xml
  excerpt_only: true
~~~

Explicaremos ligeramente que hace cada una de ellas.

- *path*: Definimos la ubicación del fichero de feed (/blog), el formato (xslt) y la extensión (xml)
- *excerpt_only*: Al configurarlo como true estamos excluyendo el contenido de los posts de ser expuesto en el feed. Por defecto está a false.

Se podrían definir más configuraciones como las categorías, etiquetas o colecciones que queramos que se tengan en cuenta de cara a la elaboración del fichero. Pero para este blog no vamos a usar ninguna de ellas, no obstante dejamos link a la [documentación oficial](https://github.com/jekyll/jekyll-feed#categories) donde se hace referencia a estas configuraciones.


## Recursos

[Proyecto jekyll-feed en Github](https://github.com/jekyll/jekyll-feed){:target="_blank"}
