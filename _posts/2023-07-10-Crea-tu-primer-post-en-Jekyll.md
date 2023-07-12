---
layout: post
author: Antonio
tags: [Tutoriales, Blogging]
---
- Tabla de contenidos
{:toc}

En este artículo recogemos todos los pasos necesarios para crear nuestra primera publicación en un blog que está en Jekyll.
{:.lead}

## Crear carpeta "_posts"

En el raiz de nuestro proyecto crearemos la carpeta `_posts`, que es donde se almacenarán todos los artículos que vayamos creando en el post.

### Crear nuestro primer artículo

Dentro de la carpeta `_posts` crearemos un fichero con el siguiente formato:

```
[año]-[mes]-[día]-[Título del artículo].md
```

Para que veamos el ejemplo de este mismo artículo, sería algo así:

```
2023-07-10-Crear-tu-primer-post-en-Jekyll.md
```

## Listado de posts

Por defecto, este tema muestra los posts en la carpeta `/blog`, siempre y cuando tengamos dentro un fichero index.html con el siguiente código en el Front Matter
```yaml
---
layout: default
title: Blog
description: >
  Blog de Antonio Muñiz. Apuntes, aprendizajes y divagaciones.
---

```

## Crear categorías o tags. 

Según la documentación de Jekyll podemos organizar la información a través de colecciones. 

### Configuración

Primero de todo debemos indicarle a Jekyll de la existencia de nuestra nueva colección. Esto se hace en el fichero `_config.yaml`.

Dado que lo que queremos es crear dos tipos de agrupaciones: categorías y etiquetas, añadiremos el siguiente texto al fichero yaml.

~~~yaml
file: '_config.yml'
---
collections:
  featured_categories:
    permalink:         /:name/
    output:            true
  featured_tags:
    permalink:         /tag-:name/
    output:            true
~~~

### Añadir elementos a cada colección

Tenemos dos colecciones: `featured_categories` y `featured_tags`, como se observa en el bloque anterior. Debemos crear una carpeta por cada una de dichas colecciones en el directorio raíz de nuestro proyecto Jekyll y dentro crearemos un fichero markdown por cada una de las categorías y etiquetas que queramos incluir en nuestro blog.

En la imagen se ve el ejemplo de las dos primeras categorías y etiquetas de este blog.

![image](/assets/img/blog/category-tag-folders.png){:.lead width="100" height="25" loading="lazy"}

Dentro de cada fichero podemos crear un Front Matter como el que ponemos a continuación de ejemplo:

~~~yaml
---
layout: list
title:  Jekyll
slug:   jekyll
menu: true
description: >
  Artículos relacionados con la herramienta Jekyll
---
~~~

### Página de categorías y de etiquetas

Ahora tenemos que poder acceder a todos los posts relacionados con una categoría, pero para ello debemos crear una página de categorías y otra de etiquetas en la raíz de nuestro proyecto. 




## Recursos

Documentación oficial de [Jekyll](https://jekyllrb.com/docs/step-by-step/08-blogging/){:target="_blank"}

Documentación del theme [hydejack](https://hydecorp.github.io/hydejack-starter-kit/docs/basics/#adding-a-category-or-tag){:target="_blank"}

Crear [tags](https://github.com/hydecorp/hydejack-site/blob/1e1b648b39ac1b698157a904174afa99c84777fa/hydejack/_posts/2016-03-08-introducing-hydejack.md?plain=1#L88){:target="_blank"}

Añadir [categorías o tags](https://hydecorp.github.io/hydejack-starter-kit/docs/basics/#adding-a-category-or-tag){:target="_blank"}

[Blog](https://tseknet.com/blog/){:target="_blank"} en el que me he "inspirado"
