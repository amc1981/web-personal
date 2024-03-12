---
layout: post
title: Guía rápida Jekyll
description:
image:
category: blogging
tags: 
 - how-to 
 - jekyll
author: Antonio
---
* Table of contents
{:toc}

## Arrancar servidor Jekyll en local

Para poder ver los cambios que vamos generando necesitamos levantar Jekyll en nuestro entorno local. 

```bash
$ bundle exec jekyll serve --trace --drafts
Configuration file: C:/Users/Antonio/PROYECTOS/Web-Personal/web-personal/_config.yml
To use retry middleware with Faraday v2.0+, install `faraday-retry` gem
            Source: C:/Users/Antonio/PROYECTOS/Web-Personal/web-personal
       Destination: C:/Users/Antonio/PROYECTOS/Web-Personal/web-personal/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
      Remote Theme: Using theme hydecorp/hydejack
       Jekyll Feed: Generating feed for posts
                    done in 13.81 seconds.
 Auto-regeneration: enabled for 'C:/Users/Antonio/PROYECTOS/Web-Personal/web-personal'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
      Regenerating: 1 file(s) changed at 2023-09-21 20:00:14
                    _drafts/guía-rápida-jekyll.md
      Remote Theme: Using theme hydecorp/hydejack
       Jekyll Feed: Generating feed for posts
                    ...done in 19.0671832 seconds.
```

Como indica en la salida del comando el servidor se levanta y podemos ver el resultado de nuestra web en la url: `http://127.0.0.1:4000/`

## Creación de nuevo borrador

Cuando queremos crear rápidamente un nuevo fichero con extensión markdown dentro de la carpeta `_drafts` de nuestro proyecto Jekyll ejecutaremos el siguiente comando:

```bash
$ bundle exec jekyll draft "Guía rápida Jekyll"
Configuration file: C:/Users/Antonio/PROYECTOS/Web-Personal/web-personal/_config.yml
New draft created at _drafts/guía-rápida-jekyll.md 
```

## Publicar un post desde un borrador

