---
Categoria: Sistemas
Materia: 
tags:
  - Teoria
  - Definicion
---

# Definición

La fragmentación interna y externa son dos tipos de problemas que ocurren en la gestión de memoria en sistemas operativos y sistemas de almacenamiento. Te explico cada una:

![[Fragmentación-1751424836004.webp]]

## Fragmentación Interna

Sucede cuando se asigna más memoria de la que realmente necesita un proceso, desperdiciando el espacio sobrante dentro del [[bloque]] asignado.

**Características:**

- El desperdicio ocurre dentro de las particiones asignadas
- Común en sistemas de particiones fijas
- El espacio desperdiciado no puede ser utilizado por otros procesos

**Ejemplo:** Si el sistema asigna bloques de 64 KB y un proceso solo necesita 10 KB, se desperdician 54 KB que quedan inutilizables.

**Soluciones:**

- Usar particiones de tamaño variable
- Implementar paginación con páginas más pequeñas
- Algoritmos de asignación más eficientes

![[Fragmentación-1751424843901.webp]]

## Fragmentación Externa

Ocurre cuando hay suficiente memoria libre total en el sistema, pero está dispersa en bloques pequeños no contiguos que no pueden satisfacer una solicitud de memoria de mayor tamaño.

**Características:**

- El espacio libre existe, pero está "fragmentado" en pedazos pequeños
- Los bloques libres están intercalados entre bloques ocupados
- Puede hacer que una solicitud de memoria falle aunque haya espacio suficiente en total

**Ejemplo:** Si tienes 100 KB libres repartidos en bloques de 10 KB cada uno, no podrás asignar un proceso que necesite 50 KB contiguos.

**Soluciones:**

- Compactación: reorganizar la memoria para juntar los espacios libres
- Algoritmos de asignación como "best fit" o "worst fit"
- Segmentación con paginación

## Diferencias Clave

La fragmentación externa afecta el espacio entre bloques asignados, mientras que la interna afecta el espacio dentro de los bloques asignados. Ambas reducen la eficiencia del uso de memoria, pero requieren estrategias diferentes para su solución.
