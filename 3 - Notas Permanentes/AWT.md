---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
  - Java
  - "#UI"
---

Abstract Window Toolkit (AWT): Es un conjunto de [[Clase|clases]] que provee [[Java|java]] para escribir programas con [[GUI]]

La explicacion del codigo esta directamente desarrollada en [[Swing]]

Excelente pregunta sobre la historia de las [[Interfaces]] gráficas en [[Java]]. Te explico las **limitaciones de AWT** que llevaron a crear [[Swing]]:

# Problemas Principales De AWT:

## 1. **Dependencia Del Sistema Operativo (heavyweight)**

```java
// AWT
Button botonAWT = new Button("Click");
// ↑ Usa el botón nativo del sistema operativo
// En Windows: botón de Windows
// En Linux: botón de Linux
// En Mac: botón de Mac
```

**Problema**: Cada componente AWT era un componente REAL del sistema operativo, lo que causaba:

- Comportamiento inconsistente entre plataformas
- Apariencia diferente en cada SO
- Rendimiento pesado (heavyweight components)

## 2. **Look And Feel inconsistente**

- Una aplicación se veía completamente diferente en Windows vs Mac vs Linux
- Imposible mantener una identidad visual consistente
- Los usuarios tenían experiencias diferentes según su SO

## 3. **Componentes limitados**

AWT solo tenía los componentes básicos que existían en TODOS los sistemas operativos:

- Button, Label, TextField, TextArea, Choice, List, Checkbox
- **No había**: JTable, JTree, JTabbedPane, etc.

## 4. **Bugs Específicos De plataforma**

Como dependía del SO, los bugs eran diferentes en cada sistema y difíciles de corregir.
