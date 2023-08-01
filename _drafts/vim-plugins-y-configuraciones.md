---
layout: post
title: 'vim: plugins y configuraciones'
date: 2023-08-01 17:26 +0200
description: Segundo y último post de la serie relacionada con el curso "Vim profesional". Aquí se recogen los pasos necesarios para configurar vim como IDE de desarrollo.
image:
category: devops
tags:
- tutoriales
- apuntes
- how-to
curso: vim-profesional
lesson: 2
author: Antonio
---
- Tabla de contenidos
{:toc large-only}

- [1. Configuraciones](#1-configuraciones)
  - [1.1. Configuraciones nativas](#11-configuraciones-nativas)
- [2. Plugins](#2-plugins)
  - [2.1. vim plug](#21-vim-plug)
    - [2.1.1. Instalación](#211-instalación)
      - [2.1.1.1. Validar la instalación de plug](#2111-validar-la-instalación-de-plug)
  - [2.2. Instalar themes](#22-instalar-themes)
    - [2.2.1. Airline y Airline themes](#221-airline-y-airline-themes)
  - [2.3. NERDTree](#23-nerdtree)
    - [2.3.1. Instalación:](#231-instalación)
    - [2.3.2. Uso de NERDTree](#232-uso-de-nerdtree)
    - [2.3.3. Mapeando comandos en vim](#233-mapeando-comandos-en-vim)
  - [2.4. TMUX/Navigator](#24-tmuxnavigator)
    - [2.4.1. Instalación](#241-instalación)
    - [2.4.2. Manejor de TMUX](#242-manejor-de-tmux)
  - [2.5. AutoPairs](#25-autopairs)
    - [2.5.1. Instalación](#251-instalación)
  - [2.6. Commentary](#26-commentary)
    - [2.6.1. Instalación](#261-instalación)
    - [2.6.2. Uso](#262-uso)
  - [2.7. Autocompletar código](#27-autocompletar-código)
    - [2.7.1. Instalación](#271-instalación)
- [3. Anexos](#3-anexos)
  - [3.1. Mapeos / atajos de teclado personalizados](#31-mapeos--atajos-de-teclado-personalizados)
  - [3.2. AutoCommands](#32-autocommands)
  - [3.3. Navegar entre archivos](#33-navegar-entre-archivos)
  - [3.4. Indentación](#34-indentación)
  - [3.5. Vim en VSCode](#35-vim-en-vscode)
  - [3.6. Sustituciones o abreviaciones](#36-sustituciones-o-abreviaciones)
- [4. Recursos](#4-recursos)


## 1. Configuraciones 

Para el manejo de las configuraciones nativas de vim tenemos que configurarlas en el fichero `.vimrc`, que crearemos en el home de nuestro usuario. 

```powershell
Antonio@WIN10-DESK MINGW64 ~
$ vim .vimrc

/c/Users/Antonio
```

### 1.1. Configuraciones nativas

Estas configuraciones se pueden aplicar sin necesidad de instalar ningún plugin. Están disponibles con la instalación básica de `vim`.

```vim
" file: ".vimrc"
1   " Configuraciones nativas
  1 set number " añade número de línea
  2 set rnu    " set relativenumber, respecto a la línea en la que estamos
  3 set cursorline " Señala la línea en la que estamos
  4 set mouse=a " Habilita interacción de vim con el ratón
  5 set clipboard=unnamed " permite compartir el clipboard entre vim y el sistema
  6 set laststatus=2 " el buffer de undo y redo que almacenamos, podemos hacerlo mayor
  7 set noshowmode " activando esto dejamos de mostrar el modo en el que estamos, lo activaremos mas adelante vía plugin
  8 set showmatch " [revisar]
  9 set encoding=utf-8 " seteamos el encoding por defecto de nuestros ficheros
 10 syntax enabled " Permitimos que se habilite el ensalzado por sintaxis.
```

## 2. Plugins

Para manejar los plugins será necesario instalar un gestor de plugins. Existen varios:

- vundle
- Pathogen
- VAM
- plug

En nuestro caso utilizaremos `plug` por su sencillez de uso.

### 2.1. vim plug

Es el gestor de plugins que vamos a utilizar.

#### 2.1.1. [Instalación](https://github.com/junegunn/vim-plug#installation)

Aunque estemos en Windows debemos utilizar el comando indicado en la documentació para sistemas Unix

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

La salida deseada es la siguiente: 

```bash
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

##### 2.1.1.1. Validar la instalación de plug

Una vez que hemos ejecutado los pasos anteriores, accederemos nuevamente al fichero `.vimrc` y en modo comando introduciremos la palabra `Plug` y tabularemos. Eso hará que aparezcan varias opciones como: Plug, PlugClean, PlugDiff, PlugInstall, PlugSnapshot, PlugStatus, PlugUpdate o PlugUpgrade.

Con esto sería suficiente para dar por buena la instalación de `plug` como nuestro gestor de plugins de vim.

### 2.2. Instalar themes

Podemos seleccionar alguno de los temas que se ven en esta [lista](https://github.com/rafi/awesome-vim-colorschemes){:target="blank"}

Una vez seleccionemos uno, procederemos a su instalación. 

1. Añadiremos la siguiente línea entre los `call` que definimos en el punto anterior.
```vim
" file: ".vimrc"
call plug#begin('~/.vim/autoload')
Plug 'nordtheme/vim' 
cal plug#end()
```
2. Ejecutaremos el comando `:PlugInstall` en modo comando en nuestro fichero `.vimrc`.
3. Añadiremos el `colorscheme` que no indique la documentación de nuestro theme después del `call plug#end()`

#### 2.2.1. Airline y Airline themes

Plugins para mejorar la línea de estado donde se informa el modo en el que estamos, la rama de git en la que estamos editando, la posición del cursor dentro del fichero.

Para instalar, procedemos con en el caso anterior:

```vim
" file: ".vimrc"
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
```

Ejecutamos `:PlugInstall`. Después fuera del bloque `call` añadiremos las siguientes líneas:

```vim
" Config para Airline
let g:airline#extensions#tabline#enabled = 2 " Hace que aprezca el nombre del fichero en la parte superior izquierda
let g:airline_theme='onedark'
```

La primera como añadimos en el comentario, muestra el nombre del fichero en la esquina superior izquierda de nuestro terminal. La segunda se refiere al theme de Airline seleccionado.

### 2.3. NERDTree

NERDTree es un gestor de archivos para poder movernos por el arbol de directorios de nuestro sistema sin salirnos del editor `vim`.

#### 2.3.1. Instalación:

Como venimos haciendo con los anteriores plugin, añariemos la línea `Plug preservim/nerdtree`. Guardamos, salimos y volvemos a entrar y ejecutamos `:PlugInstall`

#### 2.3.2. Uso de NERDTree

De manera manual podemos abrir con el modo comando en el fichero, `:NERDTree` y si queremos cerrar el navegador de ficheros que se acaba de abrir, ejecutamos `:NERDTreeToggle`. Pero es un plugin que utilizaremos constantemente, por lo tanto vamos a mapear estos comandos de apertura y cierre en nuestro `.vimrc`

#### 2.3.3. Mapeando comandos en vim

```vim
" file: ".vimrc"
" Config NERDTree
nnoremap <C-n> :NERDTreeToggle<CR>
```

De este modo hemos mapeado que con la combinación de teclas `<Control> + n` se ejecutará el comando `:NERDTreeToggle`, el cual sirve para abrir y cerrar la funcionalidad de `NERDTree` como explicábamos en el párrafo anterior.

### 2.4. TMUX/Navigator

Sirve para navegar entre pantallas. De modo que con NERDTree abrimos varios ficheros y TMUX nos ayuda a navegar entre NERDTree y los ficheros que se nos vayan abriendo en distintas pestañas.

#### 2.4.1. Instalación 

Añariemos la línea `Plug 'christoome/vim-tmux-navigator'`. Guardamos, salimos y volvemos a entrar y ejecutamos `:PlugInstall`

#### 2.4.2. Manejor de TMUX

Ahora ya podemos abrir más ficheros desde `NERDTree` con el comando `s` (split a la derecha de NERDTree), y con la combinación `<Control> + l` nos moveremos a la derecha, y con `<Control> + h` hacia la izquierda. Es decir las teclas de dirección del propio `vim`. Lo cual quiere decir que si hacemos split horizontal nos moveremos con `<control>` + `j` o `k` dependiendo si queremos ir hacia abajo o hacia arriba, respectivamente.

### 2.5. AutoPairs

Este plugin nos permite que al abrir comillas, paréntesis, llaves, corchetes, etc. Se genere automáticamente el par de cierre.

#### 2.5.1. Instalación

Añariemos la línea `Plug 'jiangmiao/auto-pairs'`. Guardamos, salimos y volvemos a entrar y ejecutamos `:PlugInstall`

No se requiere manual. Ahora simplemente siempre que abramos una archivo en vim, se autocompletarán las parejas de caracteres como `"`,`[]`,`()`, etc.

### 2.6. Commentary

Plugin para comentar una o varias líneas con un simple comando.

#### 2.6.1. Instalación

tpope/vim-commentary
Añariemos la línea `Plug 'tpope/vim-commentary'`. Guardamos, salimos y volvemos a entrar y ejecutamos `:PlugInstall`

#### 2.6.2. Uso

- Comentar/descomentar una línea: Nos situamos en la línea a comentar y en modo Normal pulsamos -> `gcc`
- Comentar/descomentar varias líneas: Seleccionamos el bloque de líneas a comentar con el modo Visual de Vim y pulsamos -> `gc`

### 2.7. Autocompletar código

Para perfilar completamente nuestro IDE con `vim` utilizaremos el plugin `neoclide/coc.vim`

Es el plugin más "pesado" de los que llevamos instalados hasta el momento. Nos pedirá como requisito tener instalado `nodejs` en nuestro sistema. Más adelante veremos el motivo

#### 2.7.1. Instalación

1. Instalar el plugin pero esta vez añadiremos los siguiente a nuestro `.vimrc`

```vim
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```

Luego salimos y volvemos a entrar para ejecutar en modo Comando: `:PlugInstall`

2. Añadir Language servers

En una sóla línea podemos installar varios servers, en función de los lenguajes que vayamos a utilizar

```vim
:CocInstall coc-json coc-tsserver coc-prettier coc-emmet 
```

Hemos añadido los siguientes, además de los del comando anterior:
- Python: coc-pyright 
- Markdown: coc-markdownlint
- css: coc-css
- bash: coc-sh

## 3. Anexos

### 3.1. Mapeos / atajos de teclado personalizados

Existen distintos tipos de mapeos en función del modo en el que queramos mapear:

- nmap: Mapeo de comandos en modo Normal
- nnoremap: Mapeo de comandos en modo Normal y ademas impide que se sobreescriba este mapeo
- imap: Mapeo de comandos en modo Interactivo
- vmap: Mapeo de comandos en modo Visual

Hemos añadido los siguientes mapeos a nuestro `.vimrc`
```vim
" file: ".vimrc"
nmap <C-s> :w<CR>
nmap <C-m> :x<CR>
nmap <C-w> :q!<CR>
nmap - dd
```

### 3.2. AutoCommands

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

### 3.3. Navegar entre archivos

Cuando abrimos varios ficheros, se nos genera una pestaña por cada uno de ellos. Para navegar dichas pestañas lo podemos hacer con los siguientes comandos: `bnext` y `bprev`. Esto es b de buffer, next para ir al siguiente buffer hacia la derecha y prev si nos queremos mover hacia la izquierda. 

Como es bastante tedioso tener que escribir cada vez el comando deseado, cuando nos queramos mover entre archivos, vamos a mapear ambos en nuestro `.vimrc`

```vim
" file: ".vimrc"

nnoremap <C-p> :bprev<CR>
nnoremap <C-o> :bnext<CR>

```

Es decir con <Control> + p nos movemos a previo y con la o al siguiente. 

### 3.4. Indentación

Hay una manera de indentar líneas de manera rápida. En modo Normal, pulsando la combinación de teclas `>>` añade un nivel de indentado a la línea. Para quitar un nivel de indentado usaremos las contrarias: `<<`.

### 3.5. Vim en VSCode

Sólo con instalar la extensión `vscodevim`  localizará el los mapeos de `.vimrc` que no se utilicen en VSCode de manera nativa.

Enlace a certificado del curso: [Certificado](https://www.udemy.com/certificate/UC-7a5fe4d5-7e9b-4e73-895c-bf8fb66b15f0/)

### 3.6. Sustituciones o abreviaciones

Al igual que con los mapeos con `nmap`, podemos configurar combinaciones de teclas en modo Insertar que serán sustituidas por cadenas más grandes con `iab`. Por ejemplo, cuando queremos que un enlace en `Markdown` se abra en una nueva pestaña debemos añadir a continuación lo siguiente: `{:target="_blank"}`. Una manera sencilla de ahorrarnos el tener que recordar esta sentencia sería mediante la sustitución. 

En nuestro `.vimrc` podemos añadir la siguiente línea:

```vim
" file: ".vimrc"
" Sustituciones iab
iab _tb {:target="_blank"}
```

## 4. Recursos

[Más sobre sustituciones y abreviaciones](https://www.sromero.org/wiki/linux/aplicaciones/manual_vim#sustituciones_o_abreviaciones){:target="_blank"}

[Enlace al curso](https://www.udemy.com/course/vim-profesional/){:target="_blank"}

