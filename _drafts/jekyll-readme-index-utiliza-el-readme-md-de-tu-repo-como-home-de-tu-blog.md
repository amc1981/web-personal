---
layout: post
title: 'jekyll-readme-index: utiliza el README.md de tu repo como home de tu blog'
date: 2023-07-30 01:51 +0200
description: Este plugin te permite utilizar la información que muestres en el fichero README.md del repo como página de inicio de tu blog. 
image: /assets/img/blog/index-page-detail.png
category: blogging
tags: [how-to, jekyll-plugins]
author: Antonio
---
- Tabla de contenidos
{:toc large-only}

- [1. Instalación y configuración](#1-instalación-y-configuración)
- [2. Confección del fichero README.md](#2-confección-del-fichero-readmemd)
- [3. Recursos](#3-recursos)


Citando textualmente la documentación del plugin [jekyll-readme-index](https://github.com/benbalter/jekyll-readme-index#jekyll-readme-index){:target="_blank"}:

> A Jekyll plugin to render a project's README as the site's index.

Es decir, un plugin para renderizar el fichero README.md del repositorio de GitHub donde albergamos nuestra web como el index o el home de la misma.

Digamos que tienes un repositorio de GitHub con un fichero `README.md` que te gustaría utilizar como página principal de una web alojada en GitHub Pages. Podrías renombrar el fichero como `index.md`, pero entondes dejaría de ser renderizado en GitHub.com. Podrías añadir un front matter de YAML con el valor `permalink: /` en el README, pero ¿Porqué forzar a un humano a hacer aquello que Jekyll puede automatizar?

Si tienes un fichero README, y tu web no tendría una mejor página principal, este plugin indica a Jekyll la manera de utilizar el README.md como index del sitio web. Nada más, nade menos

## 1. Instalación y configuración

1. Añade lo siguiente a al fichero `Gemfile` de tu proyecto Jekyll.

```ruby
# file: "Gemfile"
gem "jekyll-readme-index"
```

2. Añade lo siguiente en el fichero `_config.yml`

```yaml
# file: "_config.yaml"
plugins:
  - jekyll-readme-index
```

3. Por último, para que los cambios tengan validez en nuestro entorno local deberemos ejecutar el comando: `bundle`

Existen configuraciones adicionales que se especifican en la [documentación oficial del plugin](https://github.com/benbalter/jekyll-readme-index#configuration), en nuestro caso no aplican.

## 2. Confección del fichero README.md

Realmente el fichero `README.md` del repositorio donde estoy alojando la web no decía mucho. Unos pocos encabezados y algún link hacia el propio blog. 

Unos días antes estuve configurando el `README.md` de mi [perfil de GitHub](https://github.com/amc1981/){:target="_blank"}, y la verdad quedé bastante contento con el resultado. Lo que hice fue seguir esta [guía](https://www.sitepoint.com/github-profile-readme/){:target="_blank"} y adaptarla a mi gusto. 

Por lo tanto ya tenía la mitad del trabajo hecho. Para el `README.md` del proyecto del blog. Cogí el de mi perfil de GitHub y lo simplifiqué un poco más además de traducirlo al castellano. Puedes ver el contenido del fichero a continuación.

{% gist af9ce11cb1a1c58c66a5ee50fb3542e6 README.md %}

Detalle del código utilizado en el fichero README.md
{:.figcaption} 

[Aquí](https://gist.github.com/amc1981/af9ce11cb1a1c58c66a5ee50fb3542e6/raw/1dd7c1256ebf26882eaf7d7f66479e22719e5b8d/README.md){:target="_blank"} puedes ver el código markdown y html que han sido utilizados en el fichero `README.md`

## 3. Recursos

Documentación oficial del plugin: [jekyll-readme-index](https://rubygems.org/gems/jekyll-readme-index){:target="_blank"}.

[Guía completa](https://www.sitepoint.com/github-profile-readme/){:target="_blank"} para hacer un `README.md` molón en tu perfil de GitHub.