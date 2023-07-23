---
layout: post
title: Creando tus propias colleciones en Jekyll
date: 2023-07-22 01:43 +0200
description: Guía detallada de como se ha creado la colección "Cursos" en esta web.
image: "/assets/img/blog/when-to-use-a-collection.png"
category: blogging
tags:
- tutoriales
- jekyll
author: Antonio
---
- Table of content
{:toc}

- [1. Introducción](#1-introducción)
- [2. Configuración](#2-configuración)
- [3. Añadir contenido](#3-añadir-contenido)
- [4. Salida](#4-salida)
- [5. Permalinks](#5-permalinks)
- [6. Ordenación de documentos ad hoc](#6-ordenación-de-documentos-ad-hoc)
  - [6.1. Ordenación por claves del Front Matter](#61-ordenación-por-claves-del-front-matter)
  - [6.2. Ordenación manual](#62-ordenación-manual)
- [7. Atributos Liquid](#7-atributos-liquid)
  - [7.1. Colecciones](#71-colecciones)
  - [7.2. Documentos](#72-documentos)
- [8. blog\_by\_curso.html](#8-blog_by_cursohtml)
  - [8.1. El código](#81-el-código)
  - [8.2. La explicación](#82-la-explicación)
- [9. Recursos](#9-recursos)




## 1. Introducción

En ocasiones se da la necesidad de organizar algunos posts, además por las clasificaciones clásicas de `categorías` y `etiquetas`, por otro tipo de ordenación. 

Es el caso que cubriré en este artículo. Tenemos la etiqueta `Apuntes` definida. Bajo ella iremos añadiendo entradas en las que haremos guías rápidas o tutoriales extensos sobre temas que sean de mi interés en aquellos cursos que vaya haciendo. Por tanto crearé una colleción de Jekyll llamada `cursos` donde incluiré un elemento a la colección para cada curso nuevo.

La idea es que a medida que vaya completando lecciones surgan nuevos temas sobre los que documentar para alcanzar una mayor comprensión. Esta clasificación de `posts por curso` me permitirá tener en una sola página toda la información acumulada en este blog que tenga relación con cada curso en cuestión.

Además creaemos una página justo un nivel superior que será un índice con enlaces a cada uno de los cursos y como tal será un elemento de la colección. 

La clasificación sería alog así: `Blog>Cursos>[nombre del curso]>[Artículos del blogrelacionados]` 

Investigando para crear esta colección encontré esta [web](https://ben.balter.com/2015/02/20/jekyll-collections/){:target="_blank"} , en la que añaden este esquema que ayuda a decidir cuándo es buena idea crear una colección:


[![Esquema para decidir cuándo crear una collección](/assets/img/blog/when-to-use-a-collection.png "Sigue el flujo")](https://ben.balter.com/2015/02/20/jekyll-collections/#when-to-use-a-post-a-page-or-a-collection){:target="_blank"}

Sigue el flujo
{:.figcaption}

En nuestro caso en un mix entre coleciones y artículos. A priori cualquier publicación es un post, pero como decíamos más arriba algunas pueden ser parte de la categoría `Apuntes` y por tanto clasificables dentro de un curso en particular. Por otro lado en la página específica de cada curso se añadirá información relativa al curso, además de una lista de posts relacionados con el mismo. 

## 2. Configuración

En el [primer post](http://blog.antoniomuniz.com/blogging/2023/07/10/Crea-tu-primer-post-en-Jekyll/#crear-categor%C3%ADas-o-tags){:target="_blank"} ya cubrimos parte de lo que vamos a mencionar en las siguientes secciones cuando hablamos de crear las colecciones de `categorías` y `etiquetas`. Nos repetiremos un poco sólo por dar contexto dentro de éste artículo y también por que hay pequeñas diferencias al ser esta colección de `cursos` una colección ad hoc, mientras que las de categorías y etiquetas están integradas en Jekyll por ser clasificaciones típicas de los blogs. 

Por tanto, primer paso. Declarar en el fichero de configuración de nuestro proyecto Jekyll que vamos a tener una nueva colección llamada `cursos`. Vamos al fichero `_config.yml` del proyecto y donde ya teníamos creadas las colecciones `featured_tags` y `featured_categories` añadimos la nueva:

```yaml
# file: "_config.yaml"

collections:
  featured_categories:
    permalink:         /blog/categories/:name/
    output:            true
  featured_tags:
    permalink:         /blog/tags/:name/
    output:            true
  cursos:
    permalink: /blog/:collection/:name
    output: true
```

Detalle sobre cómo queda nuestro fichero de configuración
{:.figcaption}

Importante definir el campo `permalink` que será la base sobre la que se montará la url de cada página de cada curso de la colección y también el campo `output` que permite a Jekyll identificar que esta colección generará una página por cada elemento de la colección existente. 

En la [documentación oficial de Jekyll](https://jekyllrb.com/docs/collections/#setup){:target="_blank"} se dan más detalles respecto al setup.
{:.note title="Más sobre colecciones"}

## 3. Añadir contenido

Ahora que Jekyll sabe de la existencia de nuestra nueva colección, tenemos que darle una ubicación y añadir elementos a la misma. 

Para lo primero crearemos una carpeta en la raíz de nuestro proyecto con el mismo nombre que hayamos dado en el `_config.yaml` para nuestra colección. En nuestro caso la carpeta se llamará `/_cursos`. Importante el guión bajo al principio del nombre para que Jekyll haga la relación entre lo que dice la configuración y las carpetas que tiene en el proyecto. 

El siguiente paso es crear los elementos que compondrán la colección. Eso se hace creando un fichero con extensión .md por cada elemento. Nosotros hemos creado cuatro ficheros.

![Detalle de la carpeta cursos con los cuatro ficheros iniciales](/assets/img/blog/elements-in-cursos.png "Cuatro primeros cursos")

Cuatro primeros cursos
{:.figcaption}

Ahora tenemos que definir la información que tendrá cada uno de los ficheros. 

```yaml
# file: "kubernetes-for-beginners.md"

---
name:  Kubernetes for begginers
slug:   kubernetes-for-beginners
link: https://www.udemy.com/course/learn-kubernetes/
description: >
  Aprenda Kubernetes de una manera simple, fácil y divertida con ejercicios prácticos de codificación. Para principiantes en DevOps.
---
```

Es importante la elección de los campos que definimos en el `Front Matter` puesto que luego los tendremos que referenciar para la programación que haremos en el layout llamado `blog_boy_curso.html`. Nosotros hemos elegido los siguientes campos por los siguientes motivos:

- **name**: El nombre que se utilizará como título cuando referenciemos la variable `curso.name`.
- **slug**: Al igual que en otros elementos el slug será igual al nombre pero sustituiremos los espacios por guiones.
- **link**: Como vamos a añadir enlaces externos a los cursos en sus correspondientes plataformas, damos aquí de manera única el enlace y luego sólo tendremos que referenciarlo mediante la variable `curso.link`.
- **description**: Igual que la anterior. En la página de cada curso se añadirá una pequeña descripción del mismo (En principio pondremos la misma que tenga en la plataforma en la que esté publicado).

## 4. Salida

Como definimos en la configuración los campos `permalink: /blog/:collection/:name` y `output: true` significa que Jekyll nos va a crear una página por cada elemento de la colección. Como tenemos cuatro cursos creados, tendremos las siguientes cuatro url's disponibles:

```sh
http://blog.antoniomuniz.com/blog/cursos/certified-kubernetes-administration
http://blog.antoniomuniz.com/blog/cursos/kubernetes-for-beginners
http://blog.antoniomuniz.com/blog/cursos/the-complete-devops-bootcamp
http://blog.antoniomuniz.com/blog/cursos/vim-profesional
```

Procedemos pues a crear un índice para estas páginas. En nuestra carpeta `/blog` del proyecto crearemos el fichero `cursos.html`. En la versión actual hemos escrito el siguiente código:

{% raw %}
```html
<!-- file: "/blog/cursos.html" -->
---
layout: page
title: Apuntes
name: cursos
slug: cursos
description: >
  Relación de apuntes tomados en cursos que voy haciendo, sobre conceptos clave que necesito entender mejor.
---
<ul>
    {% for curso in site.cursos %}
      <li>
        <h2><a href="/blog/cursos/{{ curso.slug }}">{{ curso.name }}</a></h2>
        <p><q>{{ curso.description }}</q> ->  <a href="{{ curso.link }}" Target="_blank">Enlace al curso</a></p>
        <hr>
      </li>
    {% endfor %}
  </ul>
```
{% endraw %}

Empezamos a ver aquí el potencial de Jekyll + Liquid. Estamos iterando la variable de Jekyll `site.cursos` de modo que recorremos los cuatro ficheros que definiamos antes con los nombres de cada curso y creamos un título `h2` por cada uno para ello usamos las variables `curso.slug` en el link y `curso.name` en el texto del enlace.

Para completar éste índice añadimos un párrafo en el que añadimos un cita -etiqueta <q> en html- con la descripción del curso, `curso.description` y por último un enlace en una nueva pestaña -`target="_blank"` dentro de la etiqueta <a>- invocando a la variable `curso.link`

Por tanto hacemos uso de todos los campos del `Front Matter` de cada fichero que habíamos definido en el [punto anterior](#2-añadir-contenido).

## 5. Permalinks

Un detalle a destacar respecto a los permalinks es que existen variables específicas en Jekyll para referenciarlas a nivel de archivo de configuración. Como vimos en el punto [1](#1-configuracion), el lo definimos así: `permalink: /blog/:collection/:name`

Es decir, en nuestro navegador saldrá una url con este esquema: `http://[dominio]/blog/[colección]/[slug del curso]`

Vemos aquí el efecto del permalink definido, que se monta tras el dominio. En nuestro caso los valores de `:collection` es cursos y el de `:name`, será el slug que hayamos puesto en cada uno de los ficheros `.md` de cada curso.

## 6. Ordenación de documentos ad hoc

Como se observa en la [documentación oficial](https://jekyllrb.com/docs/collections/#custom-sorting-of-documents){:target="_blank"}:

> Por defecto, dos documentos en una colección son ordenados por el atributo `date`cuando lo tengan definido en el front matter. Sin embargo si uno o ninguno de los documentos tiene definido el campo fecha, serán ordenados por sus respectivos paths.
> 
> Puedees controlar la ordenació mediante la metadata de las colecciones.
{:.lead}

Explicaremos ambas a continuación.

### 6.1. Ordenación por claves del Front Matter

Aprovechando las capacidades que nos brinda Jekyll, podemos definir un campo ad hoc para la ordenación de nuestros artículos. En nuestro caso al tratarse de tutoriales/apuntes vinculados a cursos, podemos definir que cada artículo sea una lección. De modo que en el fichero `_config.yaml` además de las entradas para permalinks y output, añadiremos ahora el campo `sort_by` cuyo valor será `lesson`. Cuando definamos el front matter de los posts que queramos añadir al curso, añadiremos el campo `lesson` y le asignaremos el número entero que corresponda al orden que queremos darle.

Por tanto son necesarias dos operaciones. Añadir el nuevo campo `sort_by` bajo la colección en el fichero de configuración y en cada nuevo post añadir campo `lesson` y darle el valor que corresponda.

```yaml
# file: "_config.yaml"

collections:
  cursos:
    permalink: /blog/:collection/:name
    output: true
    sort_by: lesson
```

Un ejemplo del front matter de nuestro primer artículo perteneciente a un curso sería este:

```yaml
...
title: Fundamentos sobre comunicaciones en Kubernetes
curso: kubernetes-for-beginners
lesson: 1
...
```

Si comenzamos a asignar un orden pero dejamos de hacerlo, lo que pasará es que los artículos con orden definido aparecerán primero en el listado pero los que no mantendrán el orden por defecto, es decir por fecha o path del artículo. 
{:.note title="Atención"}

### 6.2. Ordenación manual

Otra opción es dar un orden manual desde el propio fichero de configuración, pero en lugar de `sort_by` utilizaremos la palabra clave `order`. Ponemos un ejemplo copiado de la documentación oficial, porque en este proyecto no hemos elegido esta opción manual pero la referenciamos igualmente para su mayor comprensión.

```yaml
# file: "example.yaml"
collections:
  tutorials:
    order:
      - hello-world.md
      - introduction.md
      - basic-concepts.md
      - advanced-concepts.md
```

## 7. Atributos Liquid

Para programar acciones sobre las colecciones en el lenguaje `Liquid`, Jekyll tiene predefinidos algunos atributos al respecto de colecciones y documentos. Adjuntamos a continuación los enlaces específicos en cada caso. Posteriormente en la explicación del código en el archivo `/layouts/blog_by_curso.html` explicaremos en profundidad aquellos atributos que finalmente hemos utilizado.

### 7.1. Colecciones

[Atributos Liquid para colecciones](https://jekyllrb.com/docs/collections/#collections){:target="_blank"}

### 7.2. Documentos

[Atributos Liquid para documentos](https://jekyllrb.com/docs/collections/#documents){:target="_blank"}

## 8. blog_by_curso.html

Hemos definido la colección, los elementos que la componen, incluso tenemos un índice de los cursos en la ruta `/blog/cursos.html` con enlaces a cada uno de ellos. Pero ¿Que vemos al seguir dichos enlaces? ¿Cómo podemos asignar automáticamente los posts que vayamos etiquetando a cada curso y con el orden que definamos en los front matter?

Liquid es la respuesta. 

Pongamos en práctica todo lo aprendido hasta ahora. 

### 8.1. El código

Añadimos a continuación el código de la primera versión funcional del archivo `/layouts/blog_by_curso.html`

{% raw %}
```html
<!-- file: "/layouts/blog_by_curso.html" -->
---
layout: default
---
{% assign num_filtered_posts = site.posts | where: 'curso', page.slug | size  %}
{% assign filtered_posts = site.posts | where: 'curso', page.slug   %}

{% for cursos in site.cursos %}
  {% if cursos.slug == page.slug %}

    {% assign curso_link = cursos.link %}
  {% endif %}
{% endfor %}
 
<p><a href="{{ curso_link }}" target="_blank">Enlace al curso</a></p>
<hr>

{% if num_filtered_posts > 0 %} 

  {% for post in filtered_posts %} 
    <ul>
      <li>
       <h3><a href="{{ post.url }}">{{ post.title }}</a>  </h3>
       <p>Etiquetas: / {% for tag in post.tags %}<a href="/blog/tags/{{ tag }}"> {{ tag }} </a>/{% endfor %} - {{ post.date | date_to_string}}</p>
       <hr>
       </li>
     </ul>
  {% endfor %}

{% else %}

<p>Aún no existen artículos para este curso</p>

{% endif %}

```
{% endraw %}

### 8.2. La explicación

Comenzamos la página definiendo dos variables:

{% raw %}
```liquid
{% assign num_filtered_posts = site.posts | where: 'curso', page.slug | size  %}
{% assign filtered_posts = site.posts | where: 'curso', page.slug   %}
```
{% endraw %}

La primera, `num_filtered_posts` es el número de posts que cumplen la condición de que el valor del campo `curso` de su front matter es exactamente igual al valor del `slug` de la página en la que nos encontramos. 

La segunda, `filered_posts` es un array con todos los posts que cumplan la misma condición que la variable anterior.

Ahora podemos definir el flujo. Comenzamos por un `if` que se pregunta si el valor de `num_filtered_posts` es mayor de cero. Si no existen artículos aún para el curso en el que estemos, se irá a la cláusula `else` y mostrará el siguiente mensaje en pantalla: "Aún no existen artículos para este curso"

Pero si se cumple la condición, empieza lo divertido.

Lanzaremos un bucle `for` que recorrerá el array `filtered posts` y obtendrá información suficiente para generar una lista desordenada de los títulos de los posts, la url y los tags asociados al mismo, que también serán vinculados. 

Adjunto enlace al [commit](https://github.com/amc1981/web-personal/commit/71d6cb23ffea4ead5ea97667a9036ec59e8f28a7?diff=split){:target="_blank"} final por si quieres echar un vistazo y revisar las versiones anteriores que fueron deshechadas.

El resultado final será algo parecido a esto:

![Detalle del resultado del código de blog_by_curso.html](/assets/img/blog/blog_by_curso_output.png "Resultado final para las páginas de cada curso")

Resultado final para las páginas de cada curso
{:.figcaption}

## 9. Recursos

[Explain like I’m five: Jekyll collections](https://ben.balter.com/2015/02/20/jekyll-collections/){:target="_blank"}

[Documentación oficial sobre colecciónes en Jekyll](https://jekyllrb.com/docs/collections/){:target="_blank"}

[Documentación oficial Liquid](https://shopify.github.io/liquid/){:target="_blank"}