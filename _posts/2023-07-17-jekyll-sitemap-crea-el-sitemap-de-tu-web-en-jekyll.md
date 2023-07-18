---
layout: post
title: 'jekyll-sitemap: Crea el sitemap de tu web en Jekyll'
date: 2023-07-17 20:19 +0200
description:
image:
category: blogging
tags:
- jekyll
- jekyll-plugins
- tutoriales
author: Antonio
---
1. Tabla de contenidos
{:toc}

jekyll-sitemap es un plugin que genera un fichero `sitemap.xml` a partir de los artículos y páginas creados en el blog.

## Instalación

1. Como de costumbre, añadimos la línea referenciando a la gema correspondiente en nuestro `Gemfile` y posteriormente ejecutamos el comando `bundle`

~~~Gemfile
gem 'jekyll-sitemap'
~~~

Podemos realizar la siguiente comprobación para ver si la gema se ha instalado correctamente en nuestro entorno local.

~~~bash
$ bundle info jekyll-sitemap
  * jekyll-sitemap (1.4.0)
        Summary: Automatically generate a sitemap.xml for your Jekyll site.
        Homepage: https://github.com/jekyll/jekyll-sitemap
        Path: C:/Ruby32-x64/lib/ruby/gems/3.2.0/gems/jekyll-sitemap-1.4.0
        Reverse Dependencies:
                github-pages (228) depends on jekyll-sitemap (= 1.4.0)
~~~

2. Añadimos el plugin en la colección de plugins de nuestro fichero de configuración `_config.yaml`

## Exclusiones

Podemos decidir qué partes de nuestro sitio web son excluidas del fichero `sitemap.xml` generado por defecto en este plugin. Para ello debemos dirigirnos a la sección `defaults:` de nuestro fichero de configuración y aquellas secciones que queramos excluir deben tener el campo `sitemap: false` 

Para que lo veamos con un ejemplo lo haremos en este blog con la sección `featured_tags`, dejando así excluidas todas las etiquetas de nuestro blog:

~~~yaml
defaults:
  -
    scope:
      path: ""
      type: featured_tags
    values:
      layout: blog_by_tag
      sitemap: false
~~~

Dentro de values, añadimos la línea antes indicada: `sitemap: false`.

## Recursos

[Documentación oficial de jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap){:target="_blank"}