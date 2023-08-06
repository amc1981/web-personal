---
layout: post
title: 'vim: plugins y configuraciones'
date: 2023-08-01 17:26 +0200
description: Segundo y último post de la serie relacionada con el curso "Vim profesional".
  Aquí se recogen los pasos necesarios para configurar vim como IDE de desarrollo.
image: "/assets/img/blog/vimrc-on-snappify.png"
category: devops
tags:
- tutoriales
- apuntes
- how-to
curso: vim-profesional
author: Antonio
---
* Tabla de contenidos
{:toc}

Continuamos con el curso de [vim profesional](/blog/cursos/vim-profesional){:target="_blank"} que iniciamos con esta [guía rápida](https://antoniomuniz.com/devops/2023/07/23/vim-referencia-comandos-i/){:target="_blank"} de comandos de vim y acabará con este post sobre plugins y configuraciones que incluiremos en nuestro fichero `.vimrc`

## Configuraciones

Para el manejo de las configuraciones nativas, plugins y otras funcionalidades como mapeos y abreviaturas en vim, tenemos que escribirlas en el fichero `.vimrc`, que crearemos en el directorio `$HOME` de nuestro usuario.

```powershell
Antonio@WIN10-DESK MINGW64 ~
$ vim .vimrc

/c/Users/Antonio
```

### Configuraciones nativas

Estas configuraciones se pueden aplicar sin necesidad de instalar ningún plugin. Están disponibles con la [instalación básica de `vim`](https://www.vim.org/download.php#pc){:target="_blank"}.

A contiuación añadimos el extracto de `.vimrc` que estamos utilizando para definir estas configuraciones y a continuación una ligera explicación de lo que hace cada una de ellas.

```vim
" file: ".vimrc"
1   " Configuraciones nativas
  1 set number " Añade número de línea en el margen izquierdo
  2 set rnu    " Indica el número de líneas por encima y por debajo de la actual.
  3 set cursorline " Señala la línea en la que estamos
  4 set mouse=a " Habilita interacción de vim con el ratón
  5 set clipboard=unnamed " Permite compartir el clipboard entre vim y el sistema
  6 set laststatus=2 " El buffer de undo y redo que almacenamos, podemos hacerlo mayor
  7 set noshowmode " Activando esto dejamos de mostrar el modo en el que estamos, lo activaremos mas adelante a través del plugin Airline
  8 set showmatch " En la apertura de `(`,`{` o `[` resalta la pareja correspondiente. Si estando encima pulsamos `%` en `modo Normal`, saltamos al carácter que cierra la pareja con el cursor.
  9 set encoding=utf-8 " Seteamos el encoding por defecto de nuestros ficheros.
 10 syntax enabled " Permitimos que se habilite el ensalzado por sintaxis.
```

## Plugins

Para manejar los plugins será necesario instalar un gestor de plugins. Existen varios:

- vundle
- Pathogen
- VAM
- plug

En nuestro caso utilizaremos `plug` por su sencillez de uso.

### vim-plug

Es el gestor de plugins que vamos a utilizar por los siguientes motivos que indican en la página oficial:

- Fácil de configurar: Un simple fichero. No requiere código repetitivo.
- Fácil de usar: Conciso, sintáxis intutiva.
- Instalación/actualización super rápida en paralelo.
- Crea clones superficiales para minimizar el espacion en disco y el tiempo de carga.
- Carga bajo demanda para un tiempo de inicio más rápido.
- Se pueden revisar y revertir actualizaciones
- Soporte de rama/etiqueta/commit.

#### Instalación

Seguiremos la guía que hay en la [documentación oficial](https://github.com/junegunn/vim-plug#unix){:target="_blank"} 

Aunque estemos en un sistema Windows **debemos utilizar el comando indicado en la documentación para sistemas Unix**.

```powershell
Antonio@WIN10-DESK MINGW64 ~ curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

La salida deseada es la siguiente:

```powershell
Antonio@WIN10-DESK MINGW64 ~
$ curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
>     https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 83127  100 83127    0     0   211k      0 --:--:-- --:--:-- --:--:--  211k

Antonio@WIN10-DESK MINGW64 ~
```

Una vez realizada la instalación debemos añadir las siguientes líneas al principio de nuestro fichero `.vimrc`

```vim
" file: ".vimrc"
call plug#begin('~/.vim/autoload')

call plug#end()
```

El valor de la ruta definida en la línea de `begin` viene dado por donde hayamos realizado la instalación con el curl. En nuestro caso dicho valor es `~/.vim/autoload/plug.vim`. Por lo tanto sólo añadimos la ruta, obviando el fichero `plug.vim` en el fichero `.vimrc`

#### Validar la instalación de plug

Una vez que hemos ejecutado los pasos anteriores, accederemos nuevamente al fichero `.vimrc` y en `modo Comando` introduciremos la palabra `:Plug` y tabularemos. Eso hará que aparezcan varias opciones como: Plug, PlugClean, PlugDiff, PlugInstall, PlugSnapshot, PlugStatus, PlugUpdate o PlugUpgrade.

Con esto sería suficiente para dar por buena la instalación de `plug` como nuestro gestor de plugins de vim.

### Themes

Ahora que tenemos `plug` instalado, podemos comenzar a instalar plugins. Empezaremos por los `Themes` o `Temas`, que no es otra cosa que la apariencia que tendrá `vim` en cuanto a combinación de colores de fondo, de letra, de tabline, etc.

Podemos seleccionar alguno de los temas que se ven en esta [lista](https://github.com/rafi/awesome-vim-colorschemes){:target="blank"}

Una vez seleccionemos uno, procederemos a su instalación.

1. Añadiremos la siguiente línea entre los `call` que definimos en el punto anterior.
  ```vim
  " file: ".vimrc"
  call plug#begin('~/.vim/autoload')
  Plug 'rakr/vim-one'
  call plug#end()
  ```

2. Ejecutaremos el comando `:PlugInstall` en `modo Comando` en nuestro fichero `.vimrc`.
3. Añadiremos el `colorscheme` que no indique la documentación de nuestro theme después del `call plug#end()`

Todos las instalaciones de plugins con `vim-plug` siguen el mismo patrón. Si el plugin está publicado en Github tendrá el siguiente esquema de url: `https://github.com/<github-user>/<repository-name>/`. Pues bien, para instalar cualquier plugin tenemos que añadir la línea `Plug '<github-user>/<repository-name>'` dentro el bloque `call plug` de nuestro `.vimrc` y ejecutar `:PlugInstall` después de haber guardado, salido y vuelto a entrar al fichero.
{:.note title="Importante"}

#### Airline y Airline themes

Usaremos este par de plugins para mejorar la línea de estado del fichero o `tabline`, donde se informa el modo en el que estamos, la rama de git en la que se esta editando, la posición del cursor dentro del fichero, etc.

Los enlaces a los repositorios en GitHub de cada unos serían:
- [vim-airline](https://github.com/vim-airline/vim-airline){:target="_blank"}
- [vim-airline-themes](https://github.com/vim-airline/vim-airline-themes){:target="_blank"} 

Para instalar (ambos plugins de una tacada), procedemos como en el caso anterior:

```vim
" file: ".vimrc"
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
```

Ejecutamos `:PlugInstall`. Después fuera del bloque `call` añadiremos las siguientes líneas:

```vim
" file: ".vimrc"
" Config para Airline
let g:airline#extensions#tabline#enabled = 2 " Hace que aprezca el nombre del fichero en la parte superior izquierda del editor.
let g:airline_theme='one'  " Este theme se refiere a airline.
```

La primera como añadimos en el comentario, muestra el nombre del fichero en la esquina superior izquierda de nuestro terminal. La segunda se refiere al theme de Airline seleccionado.

### NERDTree

NERDTree es un gestor de archivos para poder movernos por el arbol de directorios de nuestro sistema sin salirnos del editor `vim`.

#### Instalación

Podemos seguir la guía de la [documentación oficial](https://github.com/preservim/nerdtree){:target="_blank"}  o estos sencillos pasos que añadimos a continuación.

Como venimos haciendo con los anteriores plugin, añadiremos la línea `Plug preservim/nerdtree`. Guardamos, salimos y volvemos a entrar y ejecutamos `:PlugInstall`

#### Uso de NERDTree

De manera manual podemos abrir con el `modo COMANDO` en el fichero, `:NERDTree` y si queremos cerrar el navegador de ficheros que se acaba de abrir, ejecutamos `:NERDTreeToggle`. Pero es un plugin que utilizaremos constantemente, por lo tanto vamos a mapear estos comandos de apertura y cierre en nuestro `.vimrc`

#### Mapeando apertura/cierre de NERDTree

Más adelante veremos más en detalle los mapeos en vim, pero para continuar con el manejo sencillos de NERDTree necesitamos añadir las siguientes líneas en el fichero de configuración.

```vim
" file: ".vimrc"
" Config NERDTree
nnoremap <C-n> :NERDTreeToggle<CR>
```

De este modo hemos mapeado que con la combinación de teclas `<Control> + n` se ejecutará el comando `:NERDTreeToggle`, el cual sirve para abrir y cerrar la funcionalidad de `NERDTree` como explicábamos en el párrafo anterior.

### TMUX/Navigator

Sirve para navegar entre pantallas. De modo que con NERDTree abrimos varios ficheros y TMUX nos ayuda a navegar entre NERDTree y los ficheros que se nos vayan abriendo en distintas pestañas.

#### Instalación

Una vez más, podemos seguir la [documentación oficial](https://github.com/christoome/vim-tmux-navigator){:target="_blank"} , o repetir lo siguiente:

Añariemos la línea `Plug 'christoome/vim-tmux-navigator'`. Guardamos, salimos y volvemos a entrar y ejecutamos `:PlugInstall`.

#### Uso de TMUX

Ahora ya podemos abrir más ficheros desde `NERDTree` con el comando `s` (split a la derecha de NERDTree), y con la combinación `<Control> + l` nos moveremos a la derecha, y con `<Control> + h` hacia la izquierda. Es decir las teclas de dirección del propio `vim`. Lo cual quiere decir que si hacemos split horizontal nos moveremos con `<control>` + `j` o `k` dependiendo si queremos ir hacia abajo o hacia arriba, respectivamente.

### AutoPairs

Este plugin nos permite que al abrir comillas, paréntesis, llaves, corchetes, etc. Se genere automáticamente el par de cierre.

#### Instalación

Añariemos la línea `Plug 'jiangmiao/auto-pairs'`. Guardamos, salimos y volvemos a entrar y ejecutamos `:PlugInstall`

No se requiere manual. Ahora simplemente siempre que abramos una archivo en vim, se autocompletarán las parejas de caracteres como `"`,`[]`,`()`, etc.

[Link al repo en GitHub](https://github.com/jiangmiao/auto-pairs){:target="_blank"} 

### Commentary

Plugin para comentar una o varias líneas con un simple comando.

#### Instalación

Añariemos la línea `Plug 'tpope/vim-commentary'`. Guardamos, salimos y volvemos a entrar y ejecutamos `:PlugInstall`

[Link al repo en GitHub](https://github.com/tpope/vim-commentary){:target="_blank"} 

#### Uso de Commentary

- Comentar/descomentar _una línea_: Nos situamos en la línea a comentar y en `modo Normal` pulsamos -> `gcc`
- Comentar/descomentar _varias líneas_: Seleccionamos el bloque de líneas a comentar con el `modo Visual` de Vim y pulsamos -> `gc`

### Autocompletar código

Para perfilar completamente nuestro IDE con `vim` utilizaremos el plugin `neoclide/coc.vim`

Es el plugin más _pesado_ de los que llevamos instalados hasta el momento. Nos pedirá como requisito tener instalado `nodejs` en nuestro sistema. Más adelante veremos el motivo

#### Instalación

Instalar el plugin pero esta vez añadiremos los siguiente a nuestro `.vimrc`

```vim
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```

Luego salimos y volvemos a entrar para ejecutar en `modo Comando`: `:PlugInstall`

[Link al repo en GitHub](https://github.com/neoclide/coc.nvim){:target="_blank"} 

#### Añadir Language servers

En una sóla línea podemos installar varios servers, en función de los lenguajes que vayamos a utilizar

```vim
:CocInstall coc-json coc-tsserver coc-prettier coc-emmet
```

Hemos añadido los siguientes, además de los del comando anterior:

- Python: coc-pyright
- Markdown: coc-markdownlint
- css: coc-css
- bash: coc-sh

Es en la instalacióin de estos _Language Servers_ donde se hace uso de `nodejs`.

## Anexos

Una vez hemos finalizado con la instalación de plugins y configuraciones nativas en el fichero de configuración, a continuación vamos a explicar otras funcionalidades que podemos añadir a nivel de `.vimrc`.

### Mapeos / atajos de teclado personalizados

Existen distintos tipos de mapeos en función del modo en el que queramos mapear:

- nmap: Mapeo de comandos en `modo Normal`.
- nnoremap: Mapeo de comandos en `modo Normal` y ademas impide que se sobreescriba este mapeo (la adición de _nore_ aplica al resto de modos).
- imap: Mapeo de comandos en modo Interactivo.
- vmap: Mapeo de comandos en `modo Visual`.

Hemos añadido los siguientes mapeos a nuestro `.vimrc`

```vim
" file: ".vimrc"
nmap <C-s> :w<CR> " Guardar sin salir
nmap <C-m> :x<CR> " Guardar y salir
nmap <C-w> :q!<CR> " Salir sin guardar
nmap - dd " Borrar la línea en la que nos encontramos con un sólo `-`
```

### AutoCommands

Utilizaremos la sentencia `autocmd` para configurar comandos que se ejecutan sólos ante ciertos sucesos. Por ejemplo la siguiente lista de auto-comandos lo que hace es aplicar el formato correcto para cada extensión a través del `prettier` que instalamos en el punto en el que hablábamos de los Language servers.

```vim
" file: ".vimrc"
" AutoCommands
autocmd BufWrite *.html :CocCommand prettier.formatFile " formateamos todos los ficheros .html antes de salir
autocmd BufWrite *.js :CocCommand prettier.formatFile " formateamos todos los ficheros .js antes de salir
autocmd BufWrite *.ts :CocCommand prettier.formatFile " formateamos todos los ficheros .ts antes de salir
autocmd BufWrite *.css :CocCommand prettier.formatFile " formateamos todos los ficheros .css antes de salir
autocmd BufWrite *.scss :CocCommand prettier.formatFile " formateamos todos los ficheros .scss antes de salir
autocmd BufWrite *.md :CocCommand prettier.formatFile " formateamos todos los ficheros .md antes de salir
autocmd BufWrite *.py :CocCommand prettier.formatFile " formateamos todos los ficheros .py antes de salir
```

### Navegar entre archivos

Cuando abrimos varios ficheros, se nos genera una pestaña por cada uno de ellos. Para navegar dichas pestañas lo podemos hacer con los siguientes comandos: `:bnext` y `:bprev`. Esto es b de buffer, next para ir al siguiente buffer hacia la derecha y prev si nos queremos mover hacia la izquierda.

Como es bastante tedioso tener que escribir cada vez el comando deseado, cuando nos queramos mover entre archivos, vamos a mapear ambos en nuestro `.vimrc`

```vim
" file: ".vimrc"
nnoremap <C-p> :bprev<CR>
nnoremap <C-o> :bnext<CR>
```

Es decir con `<Control> + p` nos movemos a previo y con la `o` al siguiente.

### Indentación

Hay una manera de indentar líneas de manera rápida. En `modo Normal`, pulsando la combinación de teclas `>>` añade un nivel de indentado a la línea. Para quitar un nivel de indentado usaremos las contrarias: `<<`.

### Sustituciones o abreviaciones

Al igual que con los mapeos con `nmap`, podemos configurar combinaciones de teclas en `modo Insertar` que serán sustituidas por cadenas más grandes con la sentencia `iab`. 

Por ejemplo, cuando queremos que un enlace en `Markdown` se abra en una nueva pestaña debemos añadir a continuación lo siguiente: `{:target="_blank"}`. 

Una manera sencilla de ahorrarnos el tener que recordar esta texto, sería mediante la sustitución.

En nuestro `.vimrc` podemos añadir la siguiente línea:

```vim
" file: ".vimrc"
" Sustituciones iab
iab _tb {:target="_blank"}
```

### Vim en VSCode

Sólo con instalar la [extensión vscodevim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim){:target="_blank"}  aplicará el los mapeos de `.vimrc` que no se utilicen en VSCode de manera nativa, como por ejemplo "`<Control> + c`" para copiar, o "`<Control> + p`" para pegar texto.

## Resultado final

Tras haber aplicado todos estos cambios en nuestra configuración de vim, nos ha quedado el siguiente fichero.

{% gist 5641e9a794f07334fd6f144611c5042a .vimrc %}

Detalle de nuestro `.vimrc` compartido en Gist.
{:.figcaption}

## Recursos

[Enlace al curso](https://www.udemy.com/course/vim-profesional/){:target="_blank"}

[Más sobre sustituciones y abreviaciones](https://www.sromero.org/wiki/linux/aplicaciones/manual_vim#sustituciones_o_abreviaciones){:target="_blank"}


[Lista de temas para vim](https://github.com/rafi/awesome-vim-colorschemes){:target="_blank"} 

**Todos los enlaces a los Plugins**

- Gestor de plugins: [vim-plug](https://github.com/junegunn/vim-plug#unix){:target="_blank"} 
- Tabline: [vim-airline](https://github.com/vim-airline/vim-airline){:target="_blank"} 
- Temas para airline: [vim-airline-themes](https://github.com/vim-airline/vim-airline-themes){:target="_blank"} 
- Explorador de archivos: [NERDTree](https://github.com/preservim/nerdtree){:target="_blank"} 
- Navegador de pestañas/ventanas: [TMUX/Navigator](https://github.com/christoome/vim-tmux-navigator){:target="_blank"} 
- Autocompletar parejas: [auto-pairs](https://github.com/jiangmiao/auto-pairs){:target="_blank"} 
- Añadir comentarios: [commentary](https://github.com/tpope/vim-commentary){:target="_blank"} 
- Ayuda con el ensalzado en diversos lenguajes de programación y marcado: [Coc](https://github.com/neoclide/coc.nvim){:target="_blank"} 