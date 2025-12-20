---
Categoria: Sistemas
Materia: Orientación a Objetos
tags:
  - LenguajeDeProgramación
  - POO
banner: "[[Obsidian-Sync/1 - Archivos Adjuntos/Imagenes/Java-1756082056080.webp]]"
---

# Descripción

Java es un lenguaje de [[POO - Programación Orientada a Objetos]] , creado por Sun Microsystems en 1995 (hoy propiedad de Oracle).

Su principal característica es que es **portátil**: el código se compila a _bytecode_, que puede ejecutarse en cualquier dispositivo que tenga una **Java Virtual Machine (JVM)**, bajo la filosofía “*Write once, run anywhere*”.

# Funcionamiento

## JVM

Un programa escrito en Java se compila a un [[Lenguaje de Maquina|lenguaje de máquina]] de una computadora virtual, llamada Máquina Virtual Java (JVM). El lenguaje de máquina de la JVM se llama código de bytes Java (en inglés java bytecodes).

## Como Funciona

En java, el código fuente es escrito en archivos con texto plano con extensión .java. Esos archivos son posteriormente compilados en archivos con extensión `.class` por el compilador java (`javac.exe`).

Un [[Archivo|archivo]] `.class` no contiene código nativo/específico para un procesador determinado, sino que contiene bytecodes (el lenguaje de la máquina virtual de java).

![[Java-1756081156930.webp]]

El `java.exe` es un programa que viene con la plataforma java, que permite ejecutar los bytecodes, es el [[intérprete]] de java que permite que un programa Java compilado, pueda ejecutarse sobre cualquier plataforma que disponga de una JVM.

Existen diferentes Máquinas Virtuales Java para los diferentes sistemas operativos. Los mismos archivos `.class` pueden ejecutar en los distintos sistemas operativos, como Windows, Solaris, Linux o Mac, sin ninguna compilación previa.

![[Java-1756081373360.webp]]

![[Java-1756082056080.webp]]

# División

## JDK - Java Development Kit (Plataforma De Desarrollo)

Es la plataforma básica para desarrollo de programas Java. Actualmente, el nombre oficial es **Java SE** o **JSE** (Java Standar Edition). Incluye herramientas tales como un compilador, un intérprete, un depurador, un documentador, un empaquetador de clases, etc. Estas herramientas se usan desde la línea de comando.  

## JRE - Java Runtime Environment (Plataforma De Ejecución)

Provee todas las componentes necesarias para ejecutar programas escritos para JSE (programas de escritorio o applets). La **JVM** es parte del **JRE**. Los programas Java se ejecutan sobre la máquina de software llamada **JVM**.

---

# Material De Estudio

> [!info]- MoureDev - Guia
> ![[ekxJtlNOQMWIBHiIa3Y4_guia_fundamentos_java_mouredevpro.pdf]]

> [!info]- Guia de Introducción - UNI
> ![[Guia de Introducción a Java v1.1 - OOI UNRN.pdf]]
