---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - BaseDeDatos
  - Definicion
  - Teoria
---

# Definición

Número relativo de [[Registro]] (NRR): indica la posición relativa con respecto al principio del [[Archivo]]

- Con reg. de long. variable (la lectura sigue siendo secuencial, o sea de O(n))
- Con reg. long. fija. Posibilita el acceso directo (se traduce el NRR calculando la distancia en bytes) para acceder al [[Registro]] buscado

## ¿Para Qué Sirve?

- Para **acceso directo** a registros sin tener que leer todo el [[Archivo]].
- Muy útil en **archivos secuenciales con acceso relativo**.

# Uso Depende El Tipo De Registro

En registros de longitud fija la fórmula es: **Dirección física (en bytes) = NRR × tamaño del [[Registro]]**

> [!example] Ejemplo: [[Registro]] de Longitud Fija
> Si un [[Archivo]] tiene registros de 100 bytes y querés acceder al **[[Registro]] número 5** (NRR = 5):
> La posición en bytes dentro del [[Archivo]] será:   **5 × 100 = 500 bytes** desde el inicio del [[Archivo]].

En registros de **longitud variable**, **no se puede calcular directamente en qué byte comienza el [[Registro]] NRR "n"**.  
¿Por qué? Porque **no sabés cuánto ocupan los registros anteriores**.

> [!example] Ejemplo: [[Registro]] de Longitud Variable
> Si queremos entrar el [[Registro]] 3 de un [[Archivo]], como no sabemos dónde empieza el [[Registro]] 3 (porque los anteriores son variables), el sistema tiene que hacer esto:
> 1. Leer [[Registro]] 0 → 25 bytes
> 2. Leer [[Registro]] 1 → 22 bytes
> 3. Leer [[Registro]] 2 → 23 bytes
> 4. Ahora sí: llegamos al **[[Registro]] 3**
