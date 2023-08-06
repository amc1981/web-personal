---
layout: post
title: 'vim: referencia comandos (I)'
date: 2023-07-24 00:58 +0200
description: Guía rápida de comandos básicos para vi/vim
image: "/assets/img/blog/vim-neovim.jpg"
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

##  1. Fundamentos de vim
---
Vim, vi o neovim son tres versiones del editor de texto `vi` ampliamente extendido en los sitemas tipo Unix.

### 1.1. Salir sin grabar

```bash
# file: "Modo Comando"
#Dos opciones, modo comando o pulsando las dos letras Z y Q consecutivamente
:q!

ZQ
```

### 1.2. Grabar y cerrar en un sólo comando 

```bash
# file: "Modo Comando"
# Tenemos estas tres opciones, las dos primeras poniendo ":" para acceder al Modo Comando y la última sirve sólo con pulsar las dos letras "Z" mayúsculas consecutivamente
:wq

:X

ZZ
```

### 1.3. Grabar archivo sin nombrar

Cuando hemos abierto el editor por línea de comandos pero sin facilitar un nombre de archivo, podemos elegir el nombre en el momento de guardar simplemente añadiendo el nombre deseado tras el comando que elijamos.

```bash 
# file: "Modo Comando"

:w hola.java

:x hola.java

```
### 1.4. Modos 

#### 1.4.1. Modo Insertar 

A los ficheros se accede por defecto en modo Normal, si queremos empezar a escribir debemos pulsar la tecla `"i"`.

#### 1.4.2. Modo Normal

Si después de insertar texto queremos volver al modo normal pulsaremos la telca de escape, en el teclado `"ESC"`.

#### 1.4.3. Modo Visual

Hay otros modos, por ejemplo el visual para ver el texto que se selecciona. Tendremos que pulsar `"v"`.

#### 1.4.4. Modo Comando

Tenemos también el modo Comando, estando dentro del fichero si pulsamos `":"` el cursor se irá a la última línea de la pantalla y esperará a que introduzcamos el comando deseado. Mas abajo se dan varios ejemplos de comandos. 

#### 1.4.5. Modo reemplazo

Otro método menos utilizado pero muy útil es el de Reemplazo, al que se accede pulsando `"R"`.

### 1.5. Navegar en los archivos

#### 1.5.1. Básicos

En modo Normal

```bash
# file: "Modo Normal"
k # Arriba
j # Abajo
l # Derecha
h # Izquierda
``` 

#### 1.5.2. Avanzados
```bash
# file: "Modo Normal"
e # Final de palabra
b # Inicio de palabra
```
## 2. Modo inserción
---

### 2.1. Modo inserción

```bash 
# file: "Modo Normal"
I # Insertar en el inicio de la línea
a # Insertar en el siguiente carácter
A # Insertar en el final de la línea
```

### 2.2. Navegar entre palabras

```bash
# file: "Modo Normal"
w # Para ir de inicio de cada palabra hacia adelante
```

### 2.3. Inserar en nuevar líneas 

```bash 
# file: "Modo Normal"
o # Agregar nueva línea abajo
O # Agregar nueva línea arriba
```
## 3. Manipulaciones
---

### 3.1. Eliminar líneas

```bash 
# file: "Modo Normal"
dd # Borrar línea completa
```
### 3.2. Remplazo

```bash
# file: "Modo Normal"
r # Reemplazar sólo un carácter
```

### 3.3. Sustitución

```bash
# file: "Modo Normal"
s # Sobre un carácter
S # Toda la línea; Mejora el dd, borrando la línea pero entrando en inserción.
```
### 3.4. Supimir caracteres

```bash
# file: "Modo Normal"
x # Borrar caracter uno a uno hacia adelante
X # Borrar caracter uno a uno hacia atrás
```

### 3.5. Undo y Redo

```bash
# file: "Modo Normal"
u # Deshacer
U / "ctrl + r" # Rehacer
```

## 4. Manipulaciones avanzadas
---

### 4.1. Saltar al principio y final de una línea

```bash
# file: "Modo Normal"
$ # Ir a final de línea
0 # Ir al principio de línea
```


### 4.2. Delete Avanzado

```bash
# file: "Modo Normal"
dw # Borrar sólo una palabra
dl # Borrar sólo un caracter hacia adelante
d$ # Borrar desde un caracter en la línea hasta el final de línea
d0 # Borrar desde un caracter en la línea hasta el inicio de línea
```
### 4.3. Remplazo Avanzado

```bash
# file: "Modo Normal"
cw # Remplazar sólo una palabra
cl # Remplazar sólo un caracter hacia adelante
c$ # Remplazar desde un caracter en la línea hasta el final de línea
c0 # Remplazar desde un caracter en la línea hasta el inicio de línea
```

### 4.4. Copiar y pegar

Básico:

```bash
# file: "Modo Normal"
yy # Copia la línea donde esté el cursor
p # Pegar hacia abajo
P # Pegar hacia arriba
```

Avanzado:

```bash
# file: "Modo Normal"
yw # Copiar sólo una palabra
yl # Copiar sólo un caracter hacia adelante
y$ # Copiar desde un caracter en la línea hasta el final de línea
y0 # Copiar desde un caracter en la línea hasta el inicio de línea
```

## 5. Comandos y búsquedas
---

### 5.1. Ejecutar comandos

```bash
# file: "Modo Comando"

# Vamos a modo comando y añadimos "! "  y después el comando de CLI que queramos ejecutar.

:! python hola.py
```

### 5.2. Buscar 

```bash
# file: "Modo Comando"

# Vamos a modo comando y añadimos "/"

# Buscará desde donde tenemos el cursor hacia abajo

/saludo

# Si usamos ? buscará desde el final del fichero hacia arriba la cadena 

?saludo
```

### 5.3. Búsqueda avanzada

Aquí introducimos el carácter `\` 
```bash
# file: "Modo Comando"
?\<saludo>\
```
Buscará desde el final del fichero hacia arriba la cadena `<saludo>`

## 6. Más atajos

### 6.1. Replicar cambios

Cualquier comando que ejecutemos en modo normal, por ejemplo `dd` para borrar una línea, lo podemos replicar simplemente pulsanso `.`. Si nos equivocamos podemos deshacer el último cambio con `u`

### 6.2. Principio y fin del archivo

Para ir al principio del archivo, en modo normal: `gg`

Para ir al final del archivo: `G`

Se podría combinar con otros comandos como copiar o borrar:

```bash
# file: "Modo NORMAL"

ygg # Copia desde el cursos hasta el inicio del archivo

dG # Borraremos desde el cursos hasta el final del archivo
```

### 6.3. Agregar números a los atajos

Cualquiera de los comandos que hemos visto hasta aquí pueden ser ejecutados 1 o n veces en cada ejecución. Es decir si hacemos `dd` se borrará la línea en la que está el cursor. Si hacemos `2dd` se borrará la línea en la que está el cursor y la siguiente. 

A continuación añadimos una lista de ejemplos:

```bash
# file: "Modo NORMAL"
2dd # Borra dos líneas, la del cursor y una por debajo

5yy # Copia las 5 líneas la del cursor y cuatro por debajo

8p # Pega por debajo del cursor 8 ocurrencias de lo que tenga copiado en el buffer en última posición.

y5w # Copia 5 palabras desde donde tenemos el cursor

5yw # Copia 5 palabras desde donde tenemos el cursor

```