---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
  - Practico
Fecha de Entrega: 2025-09-30
Terminado: false
---

# Ejercicios

1. Ejercicio 1: Uso de Set a.
	1. En la implementación de la [[Clase]] `MemoryApi` las entidades del dominio deberán almacenarse en [[Colecciones]] (utilice `Set` y `List`). Por ej.:
		1. `{[[Java]]}Set<E> coleccionSet = new HashSet();`
		2. `{java}List<E> coleccionList = new ArrayList(); `
	2. Para el caso de una definición de HashSet, cambie la construcción del objeto por un TreeSet y vuelva a ejecutar. ¿qué observa?

# Desarrollo

1) .
	1)  Funciona todo.
	2)   Salta el error `Rol cannot be cast to class [[Java]].lang.Comparable` porque `TreeSet` requiere que sus elementos utilicen la interfaz `Comparable`
