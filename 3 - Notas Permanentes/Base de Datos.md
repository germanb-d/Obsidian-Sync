---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - "#BaseDeDatos"
  - "#Teoria"
  - "#Definicion"
---

# Definición

> Conjunto de información almacenada y consultada sistemáticamente.

*Sistemáticamente*: **Que sigue o se ajusta a un sistema**.
Por lo cual yo no almacenaré y consultaré al azar, será mediante la utilización de sistemas predefinidos.

## DBMS

Se maneja mediante el uso de un [[Data Base Management System (DBMS)]]:

![[Data Base Management System (DBMS)#^hvgbgt]]

> [!important] DBMS != BD
> Muchas veces se utiliza Base de Datos como sinonimo de Data Base Management System, pero son dos cosas DISTINTAS.

# Manejo De Datos

## Nivel Físico (archivos)

En este nivel, **todo se guarda como [[Archivo]]** en disco: binarios, de texto, secuenciales, con índices, etc.

Se trabaja con estructuras de almacenamiento como:

- Registros
- Campos
- Accesos directos/secuenciales
- Organización de bloques
- Espacios libres, etc.

## Nivel Lógico (modelado)

- Acá ya hablamos de entidades, relaciones, tablas, claves primarias, atributos... y no pensamos tanto en archivos, sino en **estructuras de datos**.

## Nivel Externo (usuario)

- El usuario ve pantallas, formularios, resultados de consultas, etc.
- No sabe ni necesita saber que por detrás hay archivos.

> [!note]
> - Pero, al final, **todo se traduce en archivos físicos**.
