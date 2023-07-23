---
layout: post
title: 'vim: referencia comandos (I)'
date: 2023-07-24 00:58 +0200
description: Guía rápida de comandos básicos para vi/vim
image:
category: devops
tags: [tutoriales, apuntes, how-to]
curso: vim-profesional
lesson: 1
author: Antonio
---
{:toc .large-only}

- [1. Salir sin grabar](#1-salir-sin-grabar)
- [2. Grabar y cerrar en un sólo comando](#2-grabar-y-cerrar-en-un-sólo-comando)
- [3. Grabar archivo sin nombrar](#3-grabar-archivo-sin-nombrar)
- [4. Modos](#4-modos)
  - [4.1. Modo Insertar](#41-modo-insertar)
  - [4.2. Modo Normal](#42-modo-normal)
  - [4.3. Modo Visual](#43-modo-visual)
  - [4.4. Modo Comando](#44-modo-comando)
  - [4.5. Modo reemplazo](#45-modo-reemplazo)
- [5. Navegar en los archivos](#5-navegar-en-los-archivos)
  - [5.1. Básicos](#51-básicos)
  - [5.2. Avanzados](#52-avanzados)
- [6. Modo inserción](#6-modo-inserción)
- [7. Navegar entre palabras](#7-navegar-entre-palabras)
- [8. Inserar en nuevar líneas](#8-inserar-en-nuevar-líneas)
- [9. Eliminar líneas](#9-eliminar-líneas)
- [10. Remplazo](#10-remplazo)
- [11. Sustitución](#11-sustitución)
- [12. Supimir caracteres](#12-supimir-caracteres)
- [13. Undo y Redo](#13-undo-y-redo)
- [14. Saltar al principio y final de una línea](#14-saltar-al-principio-y-final-de-una-línea)
- [15. Delete Avanzado](#15-delete-avanzado)
- [16. Remplazo Avanzado](#16-remplazo-avanzado)
- [17. Copiar y pegar](#17-copiar-y-pegar)
- [18. Ejecutar comandos](#18-ejecutar-comandos)
- [19. Buscar](#19-buscar)


## 1. Salir sin grabar

```bash
:q!

ZQ
```

## 2. Grabar y cerrar en un sólo comando 

```bash
:wq

:X

ZZ
```

## 3. Grabar archivo sin nombrar

```bash 

:w hola.java

:x hola.java

```
## 4. Modos 

### 4.1. Modo Insertar 

con "i"

### 4.2. Modo Normal

Pulsando ESC

### 4.3. Modo Visual

con "v"

### 4.4. Modo Comando

Al pulsar ":" 

### 4.5. Modo reemplazo

con "R"

## 5. Navegar en los archivos

### 5.1. Básicos
En modo Normal
```
Arriba: "k"
Abajo: "j"
Derecha: "l"
Derecha: "j"
``` 

### 5.2. Avanzados
```bash
Final de palabra: "e"
Inicio de palabra: "b"
```
## 6. Modo inserción

```bash 
Insertar en el inicio de la línea: "I"
Insertar en el siguiente carácter: "a"
Insertar en el final de la línea: "A"
```

## 7. Navegar entre palabras
```bash
Para ir de inicio de cada palabra hacia adelante: "w"
```

## 8. Inserar en nuevar líneas 

```bash 
Agregar nueva línea abajo: "o"
Agregar nueva línea arriba: "O"
```

## 9. Eliminar líneas

```bash 
Borrar línea completa: "dd"

```
## 10. Remplazo

```bash
Reemplazar sólo un carácter: "r"
```

## 11. Sustitución

```bash
Sobre un carácter: "s"
Toda la línea : "S" ; Mejora el dd, borrando la línea pero entrando en inserción.
```
## 12. Supimir caracteres

```bash
Borrar caracter uno a uno hacia adelante: "x"
Borrar caracter uno a uno hacia atrás: "X"

```

## 13. Undo y Redo

```bash
Deshacer: "u"
Rehacer: "ctrl + r" o "U"
```

## 14. Saltar al principio y final de una línea

```bash
Ir a final de línea: "$" ; Símbolo del Dollar
Ir al principio de línea: "0" ; Número cero
```


## 15. Delete Avanzado

```bash
Borrar sólo una palabra: "dw"  
Borrar sólo un caracter hacia adelante: "dl"
Borrar desde un caracter en la línea hasta el final de línea: "d$"
Borrar desde un caracter en la línea hasta el inicio de línea: "d0"
```
## 16. Remplazo Avanzado

```bash
Remplazar sólo una palabra: "cw"  
Remplazar sólo un caracter hacia adelante: "cl"
Remplazar desde un caracter en la línea hasta el final de línea: "c$"
Remplazar desde un caracter en la línea hasta el inicio de línea: "c0"
```

## 17. Copiar y pegar

```bash
copiar: "yy"
pegar hacia abajo: "p"
pegar hacia arriba: "P"
```

Copiado Avanzado:


```bash
Copiar sólo una palabra: "yw"  
Copiar sólo un caracter hacia adelante: "yl"
Copiar desde un caracter en la línea hasta el final de línea: "y$"
Copiar desde un caracter en la línea hasta el inicio de línea: "y0"
```

## 18. Ejecutar comandos

```bash
Vamos a modo comando y añadimos "!"

:! python hola.py
```

## 19. Buscar 

```bash
Vamos a modo comando y añadimos "/"

:/saludo

```
Buscará desde donde tenemos el cursor.
