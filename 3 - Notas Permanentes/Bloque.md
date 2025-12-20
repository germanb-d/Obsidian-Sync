---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - BaseDeDatos
  - Definicion
  - Teoria
---

Un **bloque** es una porción fija de espacio en disco utilizada para almacenar datos. Los [[Archivo|archivos]] , al guardarse, no se escriben "de corrido", sino que se dividen en **bloques**, que el sistema operativo usa para leer o escribir de manera eficiente.

Varios [[Registro|registros]] pueden entrar dentro de un mismo bloque, o un registro grande puede ocupar más de un bloque.

Casi nunca se mencionan los bloques porque cuando se enseña sobre archivos y bases de datos a nivel **lógico**, se enfoca en:

- cómo se organizan los **datos** (campos, registros),
- no tanto en cómo se almacenan físicamente (**bloques**).
