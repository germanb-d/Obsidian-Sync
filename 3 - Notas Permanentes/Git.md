---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

![[git-github-desktop-tutorial-guide.pdf]]

# Git + GitHub

Git es un **sistema de control de versiones** que permite registrar y administrar los cambios realizados sobre archivos (generalmente de código), facilitando el trabajo individual y colaborativo.

## ¿Por Qué Es Importante?

- Permite **volver atrás** a versiones anteriores.
- Facilita **ordenar y organizar** la evolución de un proyecto.
- Es esencial para el **trabajo en equipo**, ya que coordina cambios sin sobrescribir el trabajo de otros.
- GitHub (y GitHub Desktop) ofrecen una **plataforma y herramientas gráficas** para manejar Git sin necesidad de la terminal.

## Conceptos Clave

- **Repositorio**:
	- Espacio donde se almacena el proyecto (archivos, historial de cambios, ramas). Puede ser **local** (en tu PC) o **remoto** (en GitHub).
- **Commit**:
	- Una “captura” o registro de los cambios realizados. Cada commit tiene un mensaje que describe la modificación.
- **Rama (Branch)**:
    - Línea de desarrollo independiente.
        - `main` o `master`: rama principal.
        - `dev`: rama de desarrollo.
    - Otras ramas pueden crearse para **features** (nuevas funciones) o **testing**. Al terminar una rama, se pueden fusionar sus cambios en otra (merge).
- **Merge**:
	- Combinar los cambios de una rama en otra.
- **Fetch**:
	- Descarga información del repositorio remoto sin aplicarla todavía al proyecto local.
- **Pull**:
	- Actualiza el repositorio local trayendo los cambios del remoto. (Se recomienda hacerlo antes de commitear y pushear para evitar conflictos).
- **Push**:
	- Envía los commits locales al repositorio remoto (subir cambios a GitHub).
- **Git Add**:
    - Selecciona qué cambios se van a incluir en el próximo commit.
    - `git add .` → agrega todos los cambios.

---

## ¿Cómo Funciona?

1. **Guardado en File System**:​
	1. Cada vez que modificás un archivo, los cambios se guardan en tu computadora.
2. **Commit**:
	1. Los cambios pasan al historial de Git (quedan en la “pila” de commits, apuntada por el **HEAD**).
3. **Push**:
	1. Los cambios se envían al repositorio remoto (GitHub).
4. **Flujo típico**:
    - `Pull` (para traer cambios remotos).
    - `Add` (seleccionar archivos a versionar).
    - `Commit` (guardar cambios en local).
    - `Push` (subirlos a remoto).
---

### Ejempo De Ramas

![[Git-1758927994906.webp]]

- **Master/Main**: Azul.
- **Dev**: Morada.

---

# GitHub Desktop

- Aplicación gráfica que permite usar Git de manera intuitiva, sin comandos.
- Permite **clonar repositorios**, **crear commits**, **manejar ramas** y **hacer merge** fácilmente.
- Ideal para aprender Git y trabajar en equipo en proyectos reales.
