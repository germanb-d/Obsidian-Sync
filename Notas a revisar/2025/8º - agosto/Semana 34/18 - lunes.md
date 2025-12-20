---
journal: Calendario
Diario-Fecha: 2025-08-18
---

# Modelo Lógico Y Físico

## Modelo Conceptual - > Modelo Lógico

#Parcial

Hacer modelo conceptual, pasar a lógico y físico.

No abra datos derivados

### Datos Derivados

Datos Derivados -> Se obtienen con lógica a partir de otros datos (como sacar la edad con la fecha de nacimiento). **Debemos estar al tanto de cuantos y cuáles son nuestros datos derivados.**

#### Ventaja

Es más fácil saber cuanto debo en la cuenta o la tarjeta si tengo un dato de `SaldoActual` a tener que procesar todas las [[Transacciones]] para averiguar el saldo. Si digo que tengo la cuenta hace 20 años, esto implicaría trabajar con millones de cálculos algebraicos para determinar el saldo.

#### Desventaja

Estos datos son **redundantes**: Produce inconsistencias, o sea, que actualicen uno y no el otro. Esencialmente, aquellos datos que solo están para evitar cálculos básicos, como guardar la `fechaNac` y `edad`, cuando la operación es solo una resta.

### Que Se Debe Hacer Al Pasarlo

#### Obligatorias

- **Eliminación de atributos con cardinalidad > 1 (Polivalentes)**
	- Paso el atributo `(1,N) Telefonos` a una entidad `Telefonos` con cardinalidad (1, N) del lado de la persona y del lado del teléfono puede ser (1, N) siguiendo la regla de la generalidad para no equivocarnos u otra cardinalidad si tenemos la información necesaria.
- **Eliminación de atributos compuestos**
	- Separar los atributos. De `Direccion` (Calle - Número) a `Calle` y `Numero`.
	- Unir los atributos. De `Direccion` (Calle - Número) a (Calle y Número).
	- Pasar a una entidad. Entidad `Direccion` con atributos `Calle` y `Numero`.
	  **Siempre se usa este en atributos compuestos polivalentes.**
		- Cardinalidades:
			- Del lado de la identidad original queda la misma cardinalidad que habia.
			- Del lado de la nueva identidad queda (1, X) puede ser 1,2,3..... N depende el caso
- **Eliminación de Jerarquías de Generalización**
	- Guardar todo en la [[Clase]] padre. Genera muchos atributos y relaciones opcionales, más un atributo `Tipo`.  En caso de jerarquías parciales también necesitaría un `TipoAmbos` o separar en `Hijo1` e `Hijo2` los atributos.
	- Eliminar al padre y quedarme con los hijos. Se repiten los atributos y las relaciones en todos los hijos. `[!!info|La relación debe ser total|var(--color-orange-rgb)]`. Si la relación además es superpuesta, puedo generar inconsistencias al tener datos redundantes.
	- Relacionar `Padre` con los hijos con Es Un. Abajo (del lado del hijo) siempre es 1;1 y arriba (del lado del padre) siempre es 0; 1. Siempre tendrá una clave totalmente externa en la relación. La clave es necesaria para saber cuál es el padre del hijo.

#### No Obligatorias

- Partición de Entidades  
	- Caso 1: Si yo hago una entidad `Persona` en vez de dos entidades `Profesor` y `Alumnos`, habría muchos atributos y relaciones opcionales.
	  Caso 2: Una entidad separada para cada tipo de `Profesor` (titular, pasante, etc.) haría que se repitieran muchos datos, sería preferible que el tipo sea un atributo.
- Partición de Interrelaciones
- #Revisar
