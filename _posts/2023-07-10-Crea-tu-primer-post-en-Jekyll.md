---
layout: post
author: Antonio
image: /assets/img/blog/category-tag-folders.png
description: Guía para crear tu primera publicación en tu blog de Jekyll. Paso a paso incluyendo manejo de etiquetas y categorías.
category: blogging
tags: [tutoriales, jekyll]
---
* Tabla de contenidos
{:toc}

En este artículo recogemos todos los pasos necesarios para crear nuestra primera publicación en un blog que está en Jekyll.
{:.lead}

## 1. Crear carpeta "_posts"

En el raiz de nuestro proyecto crearemos la carpeta `_posts`, que es donde se almacenarán todos los artículos que vayamos creando en el post.

### 1.1. Crear nuestro primer artículo

Dentro de la carpeta `_posts` crearemos un fichero con el siguiente formato:

```
[año]-[mes]-[día]-[Título del artículo].md
```

Para que veamos el ejemplo de este mismo artículo, sería algo así:

```
2023-07-10-Crear-tu-primer-post-en-Jekyll.md
```

## 2. Listado de posts

Por defecto, este tema muestra los posts en la carpeta `/blog`, siempre y cuando tengamos dentro un fichero index.html con el siguiente código en el Front Matter
```yaml
# file: "blog.html"
---
layout: default
title: Blog
description: >
  Blog de Antonio Muñiz. Apuntes, aprendizajes y divagaciones.
---

```

## 3. Crear categorías o tags. 

Según la documentación de Jekyll podemos organizar la información a través de colecciones. 

### 3.1. Configuración

Primero de todo debemos indicarle a Jekyll de la existencia de nuestra nueva colección. Esto se hace en el fichero `_config.yaml`.

Dado que lo que queremos es crear dos tipos de agrupaciones: categorías y etiquetas, añadiremos el siguiente texto al fichero yaml.

~~~yaml
file: "_config.yml"
---
collections:
  featured_categories:
    permalink:         /blog/category/:name/
    output:            true
  featured_tags:
    permalink:         /blog/tags/:name/
    output:            true
~~~

### 3.2. Añadir elementos a cada colección

Tenemos dos colecciones: `featured_categories` y `featured_tags`, como se observa en el bloque anterior. Debemos crear una carpeta por cada una de dichas colecciones en el directorio raíz de nuestro proyecto Jekyll y dentro crearemos un fichero markdown por cada una de las categorías y etiquetas que queramos incluir en nuestro blog.

En la imagen se ve el ejemplo de las dos primeras categorías y etiquetas de este blog.

<img src="/assets/img/blog/category-tag-folders.png" title="" alt="Tag and category folders">

Dentro de cada fichero podemos crear un Front Matter como el que ponemos a continuación de ejemplo:

~~~yaml
# file: "jekyll.md"
---
name:  Jekyll
slug:   jekyll
description: >
  Posts sobre Jekyll...
---
~~~

Podemos observar que no hemos definido ningún `layout`. Esto es por que lo hemos definido a nivel global dentro del fichero `_config.yml` bajo la sección `defaults`.

~~~yaml
# file: "_config.yaml"
defaults:
  -
    scope:
      path: ""
      type: pages
    values:
      layout: page
  -
    scope:
      path: ""
      type: posts
    values:
      layout: post
  -
    scope:
      path: ""
      type: featured_categories
    values:
      layout: blog_by_category
  -
    scope:
      path: ""
      type: featured_tags
    values:
      layout: blog_by_tag
~~~

Como podemos ver en los dós últimos bloques de `scope`, estamos referenciando a las carpetas `featured_tags` y `featured_categories`, indicando que el layout que aplica a todos los ficheros englobados en dichas carpetas serán `blog_by_tag` y `blog_by_category` respectivamente.

De este modo, en cuando se renderize nuestro sitio, se creará una página automática para cada etiqueta o categoría. En los layouts o plantillas de  `blog_by_tag` y `blog_by_category` explicaremos más adelante el código utilizado para que nos muestre las entradas del blog relacionadas con cada etiqueta o categoría. 

### 3.3. Página de etiquetas

También tenemos que una página de etiquteas en la raíz de nuestro proyecto o en la carpeta blog, donde ya habíamos creado el index.html del blog (no confundir con el index.html de la raíz del proyecto donde está la Home de la web).

Introduciremos el siguiente código en nuestro fichero `tags.html`

{% gist 68b9722b4b084148e92d6f07fa6136ab tags.html %}

Código para crear un índice de etiquetas con sus correspondientes posts relacionados en la ruta `/blog/tags.html`
{:.figcaption}

Lo que estamos haciendo es iterar todos los ficheros que tenemos en la carpeta `_featured_tags`, en el momento de escribir este post son: `Apuntes.md, Blogging.md, y Tutoriales.md`, para crear un título `h4` por cada etiqueta, y para obtener cada post volvemos recorrer cada post con la etiqueta correspondiente y creamos un enlace a dicho post. 

El resultado es el siguiente: 


<img src="/assets/img/blog/tags-page-detail.png" title="" alt="Tag page detail" width="300" height="200" style="border: 1px solid #000;float: center;">

### 3.4. Posts por etiqueta o categoría

Ya sólo nos falta crear las plantillas que nos mostrarán las entradas relacionadas con cada etiqueta o categoría. En este ejemplo sólo vamos a hablar del caso de las etiquetas, pero el de las categorías es exactamente igual sólo hay que cambiar cualquier referencia a `tags` por `categories`.

La guía fundamental que he utilizado el [blog de dsigno](https://dsigno.github.io/Empezando-Jekyll/Usar-tags-y-categorias-en-Jekyll-VI/)

Este sería el código:

{% gist 68b9722b4b084148e92d6f07fa6136ab blog_by_tag.html %}

Código para crear un índice de posts por etiqueta en la ruta `/layouts/blog_by_tag.html`
{:.figcaption}

## 4. Recursos

Documentación oficial de [Jekyll](https://jekyllrb.com/docs/step-by-step/08-blogging/){:target="_blank"}

Documentación del theme [hydejack](https://hydecorp.github.io/hydejack-starter-kit/docs/basics/#adding-a-category-or-tag){:target="_blank"}

Crear [tags](https://github.com/hydecorp/hydejack-site/blob/1e1b648b39ac1b698157a904174afa99c84777fa/hydejack/_posts/2016-03-08-introducing-hydejack.md?plain=1#L88){:target="_blank"}

Añadir [categorías o tags](https://hydecorp.github.io/hydejack-starter-kit/docs/basics/#adding-a-category-or-tag){:target="_blank"}

[Blog](https://tseknet.com/blog/){:target="_blank"} en el que me he "inspirado"

[Guía completa](https://dsigno.github.io/Empezando-Jekyll/Usar-tags-y-categorias-en-Jekyll-I/){:target="_blank"} uso de categorías y etiquetas en Jekyll en castellano

Enlace a los [Github Gists](https://gist.github.com/amc1981/c1d589fb2125f6e0b07097aff79bb092){:target="_blank"} utilizados en este post