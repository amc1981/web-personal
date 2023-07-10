---
layout: post
author: Antonio
category: Jekyll
tags: [Turorial, Blogging]
---
1. Crear carpeta "_posts"
{:toc}

En este artículo recogemos todos los pasos necesarios para crear nuestra primera publicación en un blog que está en Jekyll.

## Crear carpeta "_posts"

En el raiz de nuestro proyecto crearemos la carpeta _posts, que es donde se almacenarán todos los artículos que vayamos creando en el post.

### Crear nuestro primer artículo

Dentro de la carpeta _posts crearemos un fichero con el siguiente formato:

```
[año]-[mes]-[día]-[Título del artículo].md
```

Para que veamos el ejemplo de este mismo artículo, sería algo así:

```
2023-07-10-Crear-tu-primer-post-en-Jekyll.md
```

## Listado de posts

Ya tenemos el fichero y su ubicación, pero es inaccesible. Para que podamos ver un listado de posts, tenemos que agregar el siguiente código en un fichero "index.html" dentro de la carpeta blog de nuestro proyecto.

```
---
layout: default
title: Blog
description: >
  El blog de Antonio Muñiz. Apuntes, aprendizajes y divagaciones.
---
<h1>Últimos Posts</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
```


## Recursos

Documentación oficial de [Jekyll](https://jekyllrb.com/docs/step-by-step/08-blogging/){:target="_blank"}

Documentación del theme [hydejack](https://hydecorp.github.io/hydejack-starter-kit/docs/basics/#adding-a-category-or-tag){:target="_blank"}

Crear [tags](https://github.com/hydecorp/hydejack-site/blob/1e1b648b39ac1b698157a904174afa99c84777fa/hydejack/_posts/2016-03-08-introducing-hydejack.md?plain=1#L88)

Añadir [categorías o tags](https://hydecorp.github.io/hydejack-starter-kit/docs/basics/#adding-a-category-or-tag)

